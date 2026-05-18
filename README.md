# AI-intake-triage-pipeline

AI Intake & Triage Workflow is an AI-powered automation system built with n8n and LLMs to process unstructured inbound customer requests.

## Input

The workflow accepts customer requests from two sources:

- **Gmail**: incoming support emails are captured automatically.
- **Web Form**: users can submit their email address and request message through an intake form.

Each input is normalized into a standard format containing:

- source
- sender
- raw message
- received timestamp

## Output

For each request, the workflow produces a structured record containing:

- request ID
- source and sender
- original message
- category
- priority
- confidence score
- classification reasoning
- core issue
- extracted identifiers, such as invoice numbers, error codes, account IDs, product areas, dates, and amounts
- urgency signal
- suggested SLA
- destination queue
- escalation flag
- escalation reasons
- human-readable summary

The final output is written to Google Sheets, either in the **Normal Queue** or the **Human Review Queue**.

## How It Works

After a request is received, the workflow normalizes the input and sends it to an LLM for analysis. The LLM classifies the request into categories such as bug reports, feature requests, billing issues, technical questions, and incidents/outages.

The model also extracts key entities, assigns priority and confidence scores, identifies urgency, suggests an SLA, and generates a short summary for the receiving team.

After the AI analysis, a code node parses the structured JSON output and applies deterministic routing and escalation rules. These rules decide whether the request should go to Engineering, Product, Billing, IT/Security, Incident Response, or Human Review.

## Escalation Logic

The workflow sends a request to human review when:

- the model confidence score is below 70%
- the message contains critical outage-related terms
- the request mentions serious production impact
- a billing discrepancy is greater than $500

This ensures that risky or uncertain cases are not handled automatically without human oversight.

## Tech Stack

- n8n
- OpenAI GPT-4o mini
- Gmail Trigger
- n8n Form Trigger
- JavaScript Code Nodes
- Google Sheets
- JSON structured outputs

## Why This Project Matters

This project demonstrates practical AI workflow engineering. It combines multi-source ingestion, input normalization, LLM-based classification, structured JSON generation, entity extraction, deterministic routing logic, escalation rules, and persistent output storage.

Instead of only using an LLM to generate text, the workflow uses AI as one step inside a larger automation system with validation, routing, and human-in-the-loop review.
