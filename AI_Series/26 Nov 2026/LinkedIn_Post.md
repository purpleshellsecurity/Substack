You Gave Your AI Agent Access. Now Prove What It Did.

I started building AdversaryLabAI because I wanted to know what I could reconstruct after an AI application handled a request. If an agent used a document to answer a question or looked up a customer, what would I need in Elastic to explain what happened?

In one document-chat request, the search returned five documents. The application selected text from four and marked a vendor onboarding memo for exclusion after it matched an injection check. The model call succeeded, but I’d have missed that exclusion if I’d logged only filenames and the model status.

I’m using the lab to work through MITRE ATLAS techniques and map the infrastructure and evidence each test needs. This first article walks through the three AWS workloads I started with, why I built them this way, and what I can investigate through their logs.

Full article:
https://github.com/purpleshellsecurity/Substack/blob/main/AI_Series/26%20Nov%202026/01_Building_an_AI_Security_Lab-purpleshell.md

---

**Publication notes:** The link above opens the revised article draft. Replace it with **[PUBLISHED SUBSTACK ARTICLE URL]** when available. Match the five returned documents, four inclusion decisions, excluded memo, and successful model-call record to the same retained deployment and request before publication. If attaching an Elastic screenshot, use the [screenshot guidance](Elastic_Discover_Screenshot.md) and confirm its visible fields support the description above.

**Image to attach:** [AdversaryLabAI diagram](assets/AdversaryLabAI-architecture.png) · [Editable source](assets/AdversaryLabAI-architecture.drawio)

**Alt text:** AWS architecture of AdversaryLabAI. The chat Lambda retrieves document content from a Bedrock Knowledge Base and submits selected context to a model. The support agent uses AgentCore Gateway and a customer lookup Lambda. The MCP client calls a separate product tool server. Cloud and application logs reach Elastic Security Serverless outside AWS.

