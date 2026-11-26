# Elastic Discover screenshot for issue one

Capture one ordinary question from the document chat. Use a known successful baseline request with synthetic documents so readers can see the normal request path before later issues cover the experiments.

## Find a request

In Discover, switch to ES|QL and set an absolute time range covering the lab run. For the November 25 release checks, include the dates and times of the actual deployment in your Kibana time zone. The lab retains indexed document-chat evidence after RAG teardown, subject to Elastic retention.

If you have the baseline replay receipt, use its deployment ID and application request ID directly. Otherwise, run this query to list candidates and match one to a known baseline by its ID or timestamp. The model status column helps you choose a completed call. This first query also lists experiment traffic.

```esql
FROM logs-adversarylab.ai-*
| WHERE ai_lab.log_type == "model_result"
    AND ai_lab.request_id IS NOT NULL
    AND ai_lab.deployment_id IS NOT NULL
| SORT @timestamp DESC
| KEEP @timestamp, ai_lab.deployment_id, ai_lab.request_id, ai_lab.model_status
| LIMIT 50
```

## Capture the request timeline

Replace the two placeholders with the IDs from the same request. For document chat, the application request ID comes from API Gateway. The separate Lambda invocation ID identifies a different event.

```esql
FROM logs-adversarylab.ai-*
| WHERE ai_lab.deployment_id == "YOUR_DEPLOYMENT_ID"
    AND ai_lab.request_id == "YOUR_REQUEST_ID"
    AND ai_lab.log_type IN ("retrieval_query", "retrieval", "model_result")
| SORT @timestamp ASC
| KEEP @timestamp, ai_lab.log_type, ai_lab.document_name, ai_lab.included_in_context, ai_lab.model_status
| RENAME ai_lab.log_type AS event_type, ai_lab.document_name AS document_name, ai_lab.included_in_context AS in_context, ai_lab.model_status AS model_status
| LIMIT 100
```

Look for the search (`retrieval_query`), a row per retrieved passage (`retrieval`), and the application’s record of the model call (`model_result`). On retrieval rows, `in_context` records the application's decision about including that passage. On the model-result row, read `model_status`. Blank cells are expected when a field belongs to another event type. If you see only part of the sequence, check the time range and both IDs before drawing conclusions.

**Screenshot.** Crop to the result table with the timestamps and column headers visible. Use a request whose document names are suitable to publish. Leave the query editor, deployment IDs, request IDs, and raw prompts out of the crop. Place the screenshot after the document chat paragraph in the article.

**Caption to use once confirmed in the results.** “One question in the document chat. I can follow the search, see which documents it returned, and find the application's record of the model call.”

## Diagram

[Editable draw.io diagram](assets/AdversaryLabAI.drawio) · [Newsletter PNG](assets/AdversaryLabAI.png). Download the editable file and open it in the [draw.io editor](https://app.diagrams.net/). The article already embeds the PNG.

[Original series plan](../24_Nov_2026/Series_Plan.md)
