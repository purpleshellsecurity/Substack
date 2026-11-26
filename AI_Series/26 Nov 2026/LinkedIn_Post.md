If an AI agent requests a customer record, what would I need to see in Elastic to tell whether the employee actually received it?

That’s one of the questions that shaped AdversaryLabAI. I wanted a repeatable way to study MITRE ATLAS techniques in AWS and see what the activity looked like from the investigator’s side.

For the customer support agent, I kept the tool read-only. A single customer lookup was enough to study the part I cared about. A Lambda execution log could tell me the function ran. To follow the lookup, I’d also need to know which employee made the request, whose record they asked for, and what the application did after it checked their access.

The other workloads came from different questions. With document chat, I wanted to follow a passage from retrieval into the model request. With MCP, I wanted control over the tool description and the result the client received.

I wrote up how I designed the lab, why I chose Elastic Serverless, and what I’m looking for in the telemetry. https://github.com/purpleshellsecurity/Substack/blob/main/AI_Series/26%20Nov%202026/01_Building_an_AI_Security_Lab.md

---

**Image to attach:** [AdversaryLabAI diagram](assets/AdversaryLabAI.png) · [Editable source](assets/AdversaryLabAI.drawio)

**Alt text:** The AWS research host and document chat share an Elastic Agent on EC2. The customer support agent and MCP workload each send CloudWatch logs through their own Lambda shipper. All three collection paths end in Elastic Security.
