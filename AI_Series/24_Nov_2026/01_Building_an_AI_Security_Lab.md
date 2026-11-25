# Building an AI Security Lab with AWS and Elastic

Date: 24_Nov_2026

I started this project because I wanted to better understand MITRE ATLAS and the telemetry generated when AI attacks are simulated.

Reading the technique descriptions gave me a starting point. I wanted to run experiments and examine what the application logged, what AWS captured and what reached Elastic. Would that information be enough to investigate the behavior or develop a useful detection?

Those questions led me to build a lab using AWS and Elastic Security.

## Using ATLAS to determine what to build

My first step was organizing the MITRE ATLAS attack patterns by the application capabilities and infrastructure needed to simulate them.

That helped me assess what the existing lab could support and where there were gaps. Some experiments required document retrieval. Others needed an agent that could select tools, supply parameters and request execution. Behaviors involving malicious tool descriptions, results and discovery changes led me toward an MCP server and connected client.

I then researched how to implement those capabilities in AWS. That meant evaluating services and integrations, determining where authentication and authorization would be enforced, and examining the available telemetry.

The work shaped three workloads:

- **Document retrieval:** a chat application using a Bedrock Knowledge Base and synthetic documents with different access classifications.
- **A business support agent:** an application with employee authentication and a read-only customer lookup tool.
- **MCP:** a synthetic server and connected client for testing tool descriptions, results and discovery changes.

The mapping gave each workload a purpose and helped me decide whether additional infrastructure would support a useful experiment. It defines opportunities for testing, not confirmed coverage of every associated ATLAS technique.

## Bringing the telemetry together

The lab provides a way to examine AWS telemetry alongside application logs. AWS telemetry offers visibility into service and infrastructure activity, while application telemetry records behavior such as document retrieval, authorization decisions and tool use.

I wanted to understand how those sources could be correlated during an investigation. What happened within the application? What activity did AWS record? Could I connect those observations to the same experiment?

Collecting the data in Elastic provides a place to investigate those relationships. The question is whether the available evidence is sufficient to explain what happened. That requires checking the behavior being tested, the logging and the collection path together.

## Working toward repeatable experiments

I also wanted an environment I could deploy, test, clean up and redeploy without manually repairing it between runs.

That brought deployment tracking, error reporting, recovery and cleanup into scope. As the project grew, I reviewed the code and documentation to clarify responsibilities and make the platform easier to operate.

This required more engineering than I initially expected. It also required keeping implementation checks separate from live validation. Local tests can check application logic and verification behavior; they do not establish that AWS services executed correctly or that telemetry reached Elastic. Those claims need evidence from the deployed build.

## What I’ll share

In this series, I’ll walk through how I used MITRE ATLAS to define the lab’s requirements, the decisions involved in building it on AWS, and what I learn from the experiments.

The source code will remain private. I’ll share architecture, sanitized examples and the evidence behind my observations, while distinguishing completed testing from work that still needs validation.

For security engineers assessing similar applications, the aim is to make that work useful: which events to collect, how to connect them and what questions the available evidence can—and cannot—answer.
