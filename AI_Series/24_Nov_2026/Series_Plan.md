# AI Series — Article Plan

Date: 24_Nov_2026

Article 1: [Building an AI Security Lab with AWS and Elastic](01_Building_an_AI_Security_Lab.md)

| Article | Main question | What you’d share |
| --- | --- | --- |
| **2. Turning ATLAS into lab requirements** | How did you determine what infrastructure was needed? | Your grouping method, existing capabilities, gaps and why RAG, an agent and MCP became separate workloads. Distinguish potential coverage from tested coverage. |
| **3. Building the document-retrieval workload** | What does an AWS retrieval application need to support useful security experiments? | The Knowledge Base architecture, source documents, metadata, access filtering and telemetry. Explain the implementation choices without making the old S3 approach the central story. |
| **4. Building an agent with an authorization boundary** | What happens between a model requesting a tool and that tool executing? | Cognito, Harness, Gateway and the customer lookup. Follow identity and authorization through an allowed and denied request, once supported by retained evidence. |
| **5. Why add a separate MCP workload?** | What could it test that the existing agent couldn’t? | Discovery, tool descriptions, returned content and catalog changes. Explain the server/client boundary and distinguish attack delivery from model influence. |
| **6. Bringing AWS and application telemetry together** | Can you reconstruct an experiment from the available evidence? | A sanitized request timeline, correlation fields, collection paths, useful events and missing visibility. Show what each source contributes. |
| **7. Making experiments repeatable—and knowing when they failed** | What makes this a dependable research platform? | Verification checks, missing-evidence tests, deployment ownership, recovery, cleanup and same-build redeployment. Separate local guarantees from live results. |
