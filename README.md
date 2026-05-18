# AI-intake-triage-pipeline

AI Intake & Triage Workflow is an AI-powered automation system built with n8n and LLMs to process unstructured inbound requests.

The workflow classifies customer messages into categories such as bug reports, feature requests, billing issues, technical questions, and incidents. It extracts key entities, assigns priority and confidence scores, generates human-readable summaries, and routes each request to the correct destination queue.

The system also includes deterministic escalation rules for low-confidence classifications, outage-related reports, and high-value billing discrepancies, ensuring that risky or uncertain cases are sent to human review instead of being handled automatically.

