You Gave Your AI Agent Access. Now Prove What It Did.

The search returned five documents. The application selected text from four. The vendor onboarding memo matched a configured injection check and was marked for exclusion before the model request was assembled.

A successful model call alone wouldn’t tell me which text was submitted. To investigate that request, I’d need to connect what the search returned with what the application selected, then compare that record with the assembled model request.

I’m building AdversaryLabAI in AWS and Elastic to map MITRE ATLAS techniques to the infrastructure needed to test them and the evidence I can collect. I started with document chat, a customer support agent, and an MCP client/server so I can examine retrieval decisions, customer access checks, and content supplied by a tool server.

I wrote up why I chose those workloads, how they fit together, and what their logs can actually tell me.

Full article:
https://github.com/purpleshellsecurity/Substack/blob/main/AI_Series/26%20Nov%202026/01_Building_an_AI_Security_Lab-purpleshell.md

---

**Publication notes:** The link above opens the revised article draft. Replace it with **[PUBLISHED SUBSTACK ARTICLE URL]** when available. Match the five returned documents, four inclusion decisions, excluded memo, and successful model-call record to the same retained deployment and request before publication. If attaching an Elastic screenshot, use the [screenshot guidance](Elastic_Discover_Screenshot.md) and confirm its visible fields support the description above.

**Image to attach:** [AdversaryLabAI diagram](assets/AdversaryLabAI-architecture.png) · [Editable source](assets/AdversaryLabAI-architecture.drawio)

**Alt text:** AWS architecture of AdversaryLabAI. The chat Lambda retrieves document content from a Bedrock Knowledge Base and submits selected context to a model. The support agent uses AgentCore Gateway and a customer lookup Lambda. The MCP client calls a separate product tool server. Cloud and application logs reach Elastic Security Serverless outside AWS.

