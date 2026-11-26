# Building an AI Security Research Lab with AWS and Elastic

*Why I built a document retrieval app, a customer support agent, and an MCP test environment to study MITRE ATLAS techniques.*

When I read a technique in MITRE ATT&CK, I usually have two questions. How would I reproduce that behavior in my own environment? And if I did, what would actually show up in the logs?

I wanted to take that same approach to AI security using MITRE ATLAS. Say an AI agent requests a tool. What does the application record about the request? Can I tell which user it was acting for, whether the tool ran, and what came back? How much of that could I piece together later in Elastic?

Before I could answer those questions, I had to build something that could produce the behavior in the first place. AdversaryLabAI grew out of that work. It includes a document retrieval app, a customer support agent, and a separate MCP server and client. All three run in AWS, use synthetic data, and send telemetry to Elastic Security.

![AdversaryLabAI architecture. The core AWS environment and document chat share an Elastic Agent on EC2. The customer support agent and MCP workload each use a dedicated Lambda to send events to Elastic Security.](assets/AdversaryLabAI.png)

## The core AWS environment

The core lab has an Ubuntu research host on EC2. I use AWS Systems Manager to access it and Elastic Agent with Elastic Defend to collect process, file, and network activity. I also collect CloudTrail and VPC Flow Logs. Those logs land in S3, and the Elastic Agent uses SQS notifications to pick them up.

That gives me a starting point for investigating what happened on the host and in the AWS account. For questions about what a model was given or why a customer lookup was denied, I also needed records from the applications themselves.

## The three workloads

**A chat app that searches documents.** Users sign in through Amazon Cognito and ask questions against a collection of synthetic documents in a Bedrock Knowledge Base. The documents have different access classifications. The application applies a filter based on the user’s clearance and records which passages it retrieves and which ones it includes in the model request. If a restricted document shows up in the search results, I can check whether its text made it into the request.

**A customer support agent with one tool.** An employee can ask the agent to look up a customer record. I kept that tool read-only because the part I wanted to study was the decision between the model requesting a lookup and the employee getting access to the record. The agent runs on Amazon Bedrock AgentCore. A Cedar policy at the gateway checks the employee’s assignment, and the lookup service checks it again before returning a record.

**An MCP server and client.** Model Context Protocol (MCP) gives me another part of tool use to study. Here the client discovers a product lookup tool from a server I control. I can change the description the server publishes or the content it returns, then compare what the server sent with what the client received. Giving this workload its own product catalog lets me change those details without also changing the customer support agent.

## Tearing it down and running it again

I built deployment, verification, and cleanup into the project because I wanted to run an experiment, tear the environment down, and come back to the same setup later. Terraform and a set of scripts handle that work. I ran the release checks across two deployments of the same build. For the chat app, I can filter by deployment ID and request ID in Elastic to find the exact run, even if I’ve asked the same question a dozen times.

In the next issue, I’ll take one MITRE ATLAS technique and walk through how I turned it into a lab requirement. From there, I’ll get into the individual workloads and share sanitized examples of what I could reconstruct from the evidence each one produced.

See you in the next one 👋

Charles
