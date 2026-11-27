You Gave Your AI Agent Access. Now Prove What It Did.

The search returned content from five documents. The application marked four for inclusion in the model request. Content from the vendor onboarding memo matched a configured injection check and was marked for exclusion.

In Elastic, a `retrieval` event records the document in the search results. For the memo, `action = quarantined_injection` and `included_in_context = false` record the application’s decision to exclude its text from this request’s model context. The application also recorded a successful model call under the same request ID.

Those fields tell me what the application recorded. I’d still compare them with the assembled request before treating them as proof of what the model received.

I’m building AdversaryLabAI to work through MITRE ATLAS technique by technique and map what each would require in a lab: which infrastructure has to exist, what I need to control, and where I can collect evidence.

I started with document chat, a customer support agent, and an MCP client and server, using synthetic data in AWS. Elastic gives me somewhere to examine the application and infrastructure logs. These workloads are a starting point; other techniques may need different infrastructure.

I wrote up how I designed the lab and why I chose these workloads. In the series, I’ll share the tests, the evidence in Elastic, and the questions it still leaves unanswered.

https://github.com/purpleshellsecurity/Substack/blob/main/AI_Series/26%20Nov%202026/01_Building_an_AI_Security_Lab-purpleshell.md

---

**Publication notes:** The link above opens the revised article draft. Replace it with **[PUBLISHED SUBSTACK ARTICLE URL]** when available. Match the five returned documents, four inclusion decisions, excluded memo, and successful model-call record to the same retained deployment and request before publication. If attaching an Elastic screenshot, use the [screenshot guidance](Elastic_Discover_Screenshot.md) and confirm its visible fields support the description above.

**Image to attach:** [AdversaryLabAI diagram](assets/AdversaryLabAI-architecture.png) · [Editable source](assets/AdversaryLabAI-architecture.drawio)

**Alt text:** AWS architecture of AdversaryLabAI. The chat Lambda retrieves document content from a Bedrock Knowledge Base and submits selected context to a model. The support agent uses AgentCore Gateway and a customer lookup Lambda. The MCP client calls a separate product tool server. Cloud and application logs reach Elastic Security Serverless outside AWS.

