# How the three workloads work

Open **AdversaryLabAI-architecture.drawio** in diagrams.net. It contains five editable pages:

| Page | Walkthrough | Preview |
| --- | --- | --- |
| 1 · Overview | What each workload does and how collection differs. | [PNG](AdversaryLabAI-architecture.png) · [SVG](AdversaryLabAI-architecture.svg) |
| 2 · RAG | Sign-in, filtered retrieval, context selection and model response. | [PNG](AdversaryLabAI-rag.png) · [SVG](AdversaryLabAI-rag.svg) |
| 3 · Customer agent | Employee identity, model handoff, Gateway policy and record access. | [PNG](AdversaryLabAI-agent.png) · [SVG](AdversaryLabAI-agent.svg) |
| 4 · MCP | Discovery, model handoff, tool execution and result checks. | [PNG](AdversaryLabAI-mcp.png) · [SVG](AdversaryLabAI-mcp.svg) |
| 5 · Core logging | All workload CloudWatch paths, base AWS/host telemetry, collectors and Elastic. | [PNG](AdversaryLabAI-core.png) · [SVG](AdversaryLabAI-core.svg) |

Solid arrows represent requests and results; double-headed arrows summarize the return path. Purple dashed connections without arrowheads attach a control to an API; WAF and authorizers are not drawn as forwarding proxy hops. Dashed teal arrows represent telemetry delivery. Dashed amber arrows represent ingestion and embedding. AWS icons identify services; the workload pages do not use explanatory cards. Rectangular boundaries identify the lab AWS account, not extra deployed services. The earlier overview retains its grouped presentation.

The operator-side clients and Elastic are outside the AWS sandbox. Other named services are in AWS. The customer agent and MCP workload are independent of the RAG Knowledge Base and base collector. RAG uses the base collector.

The overview separates Gateway from the customer lookup Lambda so tool permission and record permission are not collapsed into one box. On the agent page, DynamoDB is shown by its two uses: backend employee/session checks and tool employee/assignment/customer reads. These are views of the existing tables, not two new databases; the entitlements table is shared between the two checks. Harness calls the Bedrock model, while the backend calls Gateway.

The RAG page separates verified clearance, passage selection and the configured model Guardrail. The MCP page distinguishes restricted and experimental catalogs and makes clear that validating a result’s format does not establish that its text contains no malicious instructions.

The article embeds the RAG, customer-agent and MCP PNGs in their respective sections. The combined overview is retained as a separate reference. Workload diagrams show application request paths, attached controls and data dependencies. Their logging bands have been removed: the separate Core logging page shows RAG, agent and MCP CloudWatch sources, their collectors and the shared AWS/host telemetry path into Elastic. Detailed audit findings stay in this guide.

The four workload/logging pages use a conventional architecture layout: standalone service icons, short service names, one-line descriptions and an AWS account boundary. The client and Elastic are outside the lab account. The earlier combined overview remains a separate reference. Official AWS architecture icons are embedded in the draw.io and SVG files, so they do not depend on external image links. The icons come from the [AWS architecture icon package](https://aws.amazon.com/architecture/icons/), release **31 July 2026**. Bedrock and AgentCore service icons identify their related components; the text distinguishes models, Knowledge Bases, Harness, Gateway and policy evaluation. Client applications, explanatory notes and Elastic are not marked as AWS services.

## The three workloads at a glance

| Workload | Example question | What supplies the information? | Who coordinates the request? |
| --- | --- | --- | --- |
| RAG | “How do I reset a client’s password?” | Passages retrieved from the Knowledge Base. | Chat Lambda. |
| Customer agent | “Look up customer C-104.” | A customer tool that checks employee access. | Backend Lambda bridges Harness and Gateway. |
| MCP | “What is the price of DEMO-001?” | A separate server’s synthetic product tool. | Operator-side client bridges the server and Harness. |

The model produces an answer or requests a tool. Application and service controls enforce access. A tool description or a model-generated instruction does not grant permission.

## RAG: from a question to an answer

Use **page 2** of the diagram. This walkthrough assumes controls are enabled.

### Before the question: prepare the documents

The **S3 corpus bucket** holds the synthetic documents, metadata and manifest. The manifest is the trusted document catalog. Metadata supplies searchable fields such as classification.

During a sync, the **Bedrock Knowledge Base** reads the source documents and invokes **Titan Embeddings V2** to create numerical representations for similarity search. **S3 Vectors** stores the index with associated passage information. The current small fixtures use no chunk splitting. Document ingestion is a preparation step, not something repeated for every question.

### When the user asks a question

1. **Cognito signs the user in.** It issues a signed token carrying identity and clearance claims. The client sends the question, bearer token and API key. The API key supports API access and usage limits; it does not establish employee identity or document permissions.
2. **API Gateway and WAF apply the entry controls.** The regional REST API validates the Cognito token before Lambda receives the request. WAF, usage limits and any configured edge restrictions also apply. A rejected request may never reach the application.
3. **Chat Lambda establishes the user’s access.** It requires verified claims, reads the clearance and loads the manifest from S3. A user with Internal clearance can retrieve Public and Internal documents. Department is not an access rule in this implementation.
4. **Lambda requests a filtered search.** It calls the Knowledge Base’s `Retrieve` API with the question and an allowlist of classifications. The KB embeds the query and searches S3 Vectors. It returns ranked passages, source locations and metadata; it has not generated an answer.
5. **Lambda checks the returned passages.** It validates the source and classification against the manifest, checks clearance, scans for configured injection patterns and applies a context-size budget. A matching injection pattern causes quarantine. Pattern matching does not detect every possible injection.
6. **Lambda constructs the model input.** Selected passages become context alongside the question; the model call also includes system instructions. `included_in_context: true` means a passage was selected for that request. `false` means it was excluded, with a recorded reason. If no permitted, usable passages remain, Lambda returns a message without calling the model.
7. **Bedrock generates the answer.** Lambda calls `Converse` separately from retrieval. The configured Bedrock Guardrail is attached when controls are enabled. Guardrails screen the model interaction; they do not replace document authorization.
8. **The response returns and evidence is collected.** Lambda returns through API Gateway to the client. Application, API and WAF logs go to CloudWatch. The base EC2 Elastic Agent collects those groups and forwards them to Elastic.

Controls-off is an intentional experiment configuration. It omits the Cognito authorizer, clearance enforcement, injection quarantine and model Guardrail attachment. Source validation and the context budget remain. Do not interpret its self-asserted identity as an authenticated employee.

**What to look for:** the question’s request ID, retrieval filter, returned passages, inclusion decisions, model status and answer checks. A retrieved filename alone does not establish that attack text reached the model or changed its answer.

## Customer agent: looking up C-104

Use **page 3** of the diagram. Assume an employee asks, “Look up customer C-104.”

1. **Cognito signs the employee in.** The signed access token identifies the employee and carries the application scope. It does not list assigned customers.
2. **The HTTP API authenticates the request.** API Gateway checks the configured issuer, audience and required chat scope before passing the request to the backend Lambda.
3. **The backend checks current employee and session state.** It independently verifies the token and reads the employee’s enabled status from DynamoDB. It creates or checks a session bound to that employee. These checks happen outside the model.
4. **Harness calls the configured model.** The backend sends the message to AgentCore Harness. The model can propose `get_customer` with `customer_id: C-104`. This is a tool request, not an authorization decision or proof of execution.
5. **The backend calls Gateway.** It validates the completed tool handoff, approved tool name and arguments, then calls AgentCore Gateway with the employee bearer token. Harness does not call Gateway directly in this implementation.
6. **Gateway and the interceptor establish trusted identity.** Gateway authenticates the caller and required scope. Its interceptor Lambda verifies the bearer token and replaces supplied `userContext` with the verified issuer and employee subject. The caller cannot select another employee by changing a tool argument.
7. **Cedar checks whether the tool call is permitted.** Gateway’s policy engine checks the tool action, scope and consistency between forwarded identity and JWT claims. An explicit forbid can block the operation here. Cedar does not read customer assignments from DynamoDB.
8. **The customer Lambda checks access to C-104.** It validates the forwarded context, checks that the employee remains enabled and reads that employee’s current assignment for C-104. If the assignment is not allowed, it returns a denial. If allowed, it reads the customer and returns only customer ID, name, plan and status, plus record/entitlement versions in the receipt.
9. **The backend returns the tool result to Harness.** The model uses the returned result to compose the answer. The backend requires a fresh successful tool receipt. Missing or denied receipts produce the application’s denial message instead of an accepted customer answer from the model.
10. **The answer and telemetry return.** The response goes through the backend and HTTP API to the employee. CloudWatch subscriptions send application and service logs to the dedicated agent shipper, which forwards them to Elastic. Native policy and invocation evidence use the additional audit path described below.

### Where employee access is checked

| Boundary | Decision |
| --- | --- |
| HTTP API | Is the token valid and does the caller have the required route scope? |
| Backend | Is the employee enabled and does this session belong to them? |
| Gateway and interceptor | Is the tool caller authenticated and is the forwarded employee identity trustworthy? |
| Cedar | May this caller invoke this tool with this identity context? |
| Customer Lambda | May this employee read C-104 right now? |
| IAM | Which services may invoke functions or read the tables? |

**Customer-level access is enforced in the customer Lambda using current assignment records.** Permission to invoke a tool is a separate decision.

For native evidence, Gateway traces go through the X-Ray destination into CloudWatch `aws/spans`, using shared Transaction Search prerequisites. A scoped CloudTrail trail records customer Lambda Invoke data events to S3 and CloudWatch. Scoped subscriptions send the selected spans and invocation events through a separate audit forwarder to Elastic. This is the configured path; the dated delivery limitation in “Reading limits” still applies.

**What to look for:** employee identity, application/session IDs, tool call ID, interceptor context, policy decision, customer allow/deny receipt and final response. No customer log by itself does not prove Cedar prevented invocation; that conclusion needs the native evidence and a complete observation window.

## MCP: looking up DEMO-001

Use **page 4** of the diagram. The example question is, “What is the price of DEMO-001?” The client runs on the operator’s machine; the server runs in AWS in this view.

### What the components do

- **MCP client:** discovers available tools, checks their definitions, coordinates model requests and executes permitted tool calls.
- **AgentCore Runtime:** hosts the separate MCP server and authenticates remote requests using operator IAM/SigV4.
- **MCP server:** advertises and executes one read-only synthetic tool, `lookup_product`. It does not call the model.
- **Dedicated Harness:** manages model interactions for this workload. It is separate from the customer agent’s Harness.
- **Bedrock model:** receives the question and accepted tool information, proposes a tool call and generates an answer from the returned result.
- **S3 artifact bucket:** stores the server code package for deployment. It is not a product database or a request-time retrieval source.

### When the experiment runs

1. **The operator starts a question with AWS credentials.** The client connects to the selected owned Runtime using signed requests. Calls to the dedicated Harness also use operator IAM. There is no employee Cognito token or C-104 assignment check in this workload.
2. **The client asks the server which tools it offers.** MCP discovery returns the tool name, description and input schema. Our server advertises `lookup_product` with the single approved SKU `DEMO-001`.
3. **The client checks the catalog before using it.** The tool name and executable schema must match the approved surface. Restricted mode also requires the baseline description. Experimental mode permits a changed description so a poisoning experiment can reach the model, while retaining the same tool/schema restrictions.
4. **The client sends accepted tool information and the question to Harness.** The model can request `lookup_product` with `sku: DEMO-001`. The client, not the model, will execute that request.
5. **The client rechecks before executing.** It checks the tool name and arguments and rediscovers the catalog. If the accepted model-visible catalog changed since discovery, it refuses execution. This checks that observation; it is not an atomic guarantee against every possible server change.
6. **The server executes the bounded lookup.** It independently accepts only the approved tool and exact SKU. The baseline fixture returns the fictional Atlas Demo Desk, priced at 42 USD, with its summary, fixture version and catalog hash. No real customer records, refunds or writes are involved.
7. **The client validates the result.** It checks the expected structure, product fields, catalog hash and any selected fixture-version requirement. The text and structured forms must agree. These checks establish the expected format and consistency, not that free-text content is harmless. An instruction inside an otherwise valid summary can still be supplied in the result-poisoning experiment.
8. **The client returns the accepted result to Harness.** The model receives it as a tool result and generates an answer. The experiment records the submitted content, completed model call and answer, then checks whether the expected test phrase appeared.
9. **The experiment retains and correlates evidence.** Private local artifacts preserve catalog, request, result and answer evidence with hashes. Server and native Harness logs go to CloudWatch. Full acceptance also publishes sanitized client events there. The dedicated MCP shipper forwards the three sources to Elastic; an individual local experiment does not necessarily publish its client events.

### What the poisoning experiments change

| Experiment | Controlled change | What must be checked separately |
| --- | --- | --- |
| Description poisoning | An instruction is added to the server’s tool description. | Was it rejected by restricted mode, or accepted and submitted in experimental mode? Did the completed answer contain the requested test phrase? |
| Result poisoning | An instruction is added to the returned product summary. | Did the accepted result match the server evidence, reach a completed model interaction and influence the answer? |
| Catalog/schema change | The server advertises a changed executable schema or changes accepted definitions between observations. | Did the client reject the unsupported schema or changed catalog before executing the tool? |

A `model_submission` event records an attempted submission. A completed model event with the AWS request ID supplies evidence of a completed service call. Neither alone proves the model followed an injected instruction. The answer check addresses that separate question, within the limits of the chosen phrase and experiment.

## Supporting services across the diagrams

IAM roles constrain service permissions. KMS encrypts the configured resources. The external Secrets Manager secret supplies Elastic credentials to the relevant collection components. Terraform state and local ownership records track what each deployment owns and how cleanup resumes after failure. They support the request paths rather than adding model decisions.

The base collector also collects host/system events, CloudTrail and VPC Flow Logs through S3/SQS, and scoped SSM output through CloudWatch. RAG depends on that collector. Agent and MCP use dedicated shippers and can run without it. See the source table for exact resources and configuration.

## What was checked

Reviewed against private AdversaryLabAWS revision `e639b498763a2a61e7e88298ebf96e3f46635248` on **26 November 2026**. Paths below are relative to that repository. Service and control shapes also carry source paths in their draw.io tooltips and `source` attributes.

| Diagram claim | Implementation checked |
| --- | --- |
| RAG uses a regional REST API, WAF, an API key and, in defended mode, a Cognito authorizer. An API key is not employee identity. | `ai_lab/terraform/api_gateway.tf`, `waf.tf`, `cognito.tf` |
| The Lambda uses verified clearance claims, builds an allowlist classification filter, calls Retrieve and validates returned sources against the manifest. | `ai_lab/src/chat/handler.py`: `resolve_identity`, `retrieval_filter`, `retrieve_documents`, `get_manifest` |
| The Lambda applies injection-pattern screening and a context budget before a separate Converse call. Empty usable context means no model invocation. | `ai_lab/src/chat/handler.py`: `scan_for_injection`, `lambda_handler`, `call_bedrock` |
| S3 documents and metadata are indexed through a deployment-owned KB, Titan Embeddings V2 and S3 Vectors. Small fixtures currently use chunking strategy NONE. The embedding model also supports query embedding. | `ai_lab/terraform/knowledge_base.tf`, `s3_corpus.tf` |
| Controls-off is an intentionally different RAG experiment configuration: no Cognito authorizer, clearance enforcement, quarantine or attached model Guardrail. Source validation and the context budget remain. | `ai_lab/terraform/api_gateway.tf`; `ai_lab/src/chat/handler.py` |
| RAG application, API and WAF logs are collected by the base EC2 Elastic Agent. | `ai_lab/terraform/logging.tf`; `scripts/lib/ai_elastic.py`; `docs/logging/RAG.md` |
| Employee Cognito tokens and the chat scope are checked by the HTTP API; the backend independently verifies identity and current enabled status and binds sessions to the employee. | `agent_lab/terraform/api.tf`, `identity.tf`; `agent_lab/src/agent_app/backend.py`, `identity.py`, `ddb_sessions.py` |
| Harness returns an inline get_customer request. The backend calls Gateway with the employee token and returns the tool receipt to Harness. There is no direct Harness-to-Gateway call in this implementation. | `agent_lab/terraform/agent.tf`; `agent_lab/src/agent_app/backend.py`: `parse_turn`, `gateway_call`, `handler` |
| Gateway authenticates the caller. Its request interceptor replaces supplied userContext with verified identity. Cedar compares that context with JWT claims and checks the scope/tool action. | `agent_lab/terraform/agent.tf`; `agent_lab/src/agent_app/interceptor.py` |
| The customer Lambda separately checks the current enabled employee and customer assignment before returning selected fields. Cedar does not look up those assignments. | `agent_lab/src/agent_app/customer.py`; `agent_lab/terraform/identity.tf`, `runtime_permissions.tf` |
| Agent application/native service logs reach its dedicated shipper through CloudWatch subscriptions. Policy spans and scoped customer Invoke audit use a separate audit forwarder. | `agent_lab/terraform/logging.tf`; `agent_lab/policy_audit/main.tf`, `policy_audit/forwarding/main.tf`; `scripts/agent_policy_audit.py`: `bootstrap` |
| The MCP operator client connects independently to the remote Runtime and a dedicated Harness, using operator IAM. | `mcp_lab/runtime_client.py`, `client.py`, `harness.py`, `permissions.py`; `mcp_lab/terraform/main.tf` |
| The MCP client validates the catalog, rediscovers before execution, enforces the single tool/SKU and checks structured/text receipts. Controlled fixture variants change descriptions, results or catalog/schema. | `mcp_lab/client.py`: `accepted_catalog`, `Bridge`; `server.py`, `fixtures.py`, `acceptance.py` |
| MCP source groups are the server, native Harness and published client events. The full acceptance workflow publishes sanitized client events; an individual local experiment need not publish them. | `mcp_lab/terraform/elastic.tf`; `acceptance.py`, `shipper.py`, `telemetry.py` |
| Base collection includes host/system events, CloudTrail and VPC Flow Logs through S3/SQS, and scoped SSM session/command output through CloudWatch. It does not capture every possible SSM operation. | `infrastructure/modules/telemetry/main.tf`; `infrastructure/modules/endpoint-host/main.tf`; `docs/logging/BASE.md` |

## Reading limits

These are walkthrough diagrams, not an exhaustive Terraform resource inventory. They group IAM policies, encryption, secrets and deployment records so the request paths remain readable. See the referenced Terraform and operator code for exact resources, conditions and lifecycle ownership.

The pages describe implemented configuration. They do not certify live health, complete telemetry delivery, successful compromise or ATLAS technique coverage. At this review, the latest agent redeployment failed its native invocation-evidence check; CloudTrail reported `CannotAssumeRole` for CloudWatch delivery. The native logging path describes intended configuration; the agent diagram directs readers here for its current delivery and verification limits. Earlier successful runs do not establish that this latest redeployment passed.

Open audit items, recorded here rather than as large boxes in the article diagrams, include: RAG auxiliary-input and generic answer/identity evidence validation (C04/C05), agent invocation-stage/error attribution (C06), and credential-bearing runtime redirects (C09). These remain limitations of the shown implementation, not new controls or completed repairs. The other lifecycle and query findings remain in the separate remediation assessment; these pages are not a complete audit register.

A retrieved passage is not necessarily submitted context. A model tool request is not proof of execution. Attack text reaching the model is not proof that the model followed it. Keep those distinctions when using the diagrams to explain experiments.

## Updating the diagrams

1. Edit the relevant page in `AdversaryLabAI-architecture.drawio`; update the overview only when relationships change.
2. Check request direction, identity propagation, authorization, data access and log delivery against the referenced implementation. Update source tooltips when code moves.
3. Keep explanatory notes separate from service boxes. Do not add an arrow solely because two services appear in the same Terraform stack.
4. Export the changed page as its matching PNG and SVG, without cropping out its title, notes or revision. The newsletter references each workload PNG in its matching section and Core logging in the core-environment section; the overview remains a separate reference.
5. Review all five pages for labels, crossings and stale claims. Update this review revision and any dated validation caveat only when supported by evidence.

`AdversaryLabAI.drawio` is an older, separate sketch. It is retained unchanged; use **AdversaryLabAI-architecture.drawio** for this four-page walkthrough.
