# Smart Support Agent

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![Google Cloud](https://img.shields.io/badge/Google%20Cloud-Connected-4285F4?logo=googlecloud&logoColor=white)
![AI Support](https://img.shields.io/badge/AI-Support%20Automation-6C47FF)

Smart Support Agent is an AI system for handling support tickets. It reads a ticket, finds the main meaning, groups similar problems, scores their impact, and prepares important issues for escalation.

The project also connects support tools such as Gmail, Google Drive, and Discord. It stores ticket and incident data in Google Cloud services and includes an admin panel for reviewing clusters.

## What It Does

1. Checks incoming ticket text with input guardrails.
2. Extracts the main details from each ticket.
3. Finds similar past incidents with retrieval and embeddings.
4. Groups related tickets into problem clusters.
5. Scores the impact of each cluster.
6. Saves useful records for later search and reporting.
7. Prepares high-impact issues for escalation.
8. Sends information through connected support tools.

## Project Map

```text
smart-support-agent-main/
├── agents/         AI steps that read, group, score, and escalate tickets
├── data/           Sample tickets, incidents, embeddings, and output records
├── deployment/     API service, admin panel, and workflow files
├── guardrails/     Checks that protect input and output quality
├── integrations/   Connections to Gmail, Google Drive, Discord, and MCP
├── memory/         Scripts that move records into cloud data stores
├── monitoring/     Space for system monitoring code
├── rag/            Retrieval tools for finding similar incidents
└── testing/        Shared testing package space
```

## Folder Guide

### `agents/`

Contains the AI workers that turn raw support tickets into useful support data.

| File | Description |
| --- | --- |
| `cluster_assignment.py` | Matches a ticket to the most similar problem cluster. |
| `escalation_preparation_agent.py` | Builds the details needed to escalate a serious problem. |
| `impact_scoring_agent.py` | Measures the impact and priority of a problem cluster. |
| `meaning_extraction_agent.py` | Extracts key facts and meaning from a support ticket. |
| `ticket_clustering_agent.py` | Groups tickets that describe the same type of issue. |
| `test_batch_extraction.py` | Tests ticket meaning extraction with a batch of tickets. |
| `__init__.py` | Marks the folder as a Python package. |

### `data/`

Stores example input, saved results, and records used by the support pipeline.

| File | Description |
| --- | --- |
| `historical_incidents.json` | Past incidents used to compare new problems. |
| `sample_tickets.json` | Example support tickets for testing and demonstrations. |
| `extracted_output.json` | Saved ticket details produced by extraction. |
| `clusters_output.json` | Saved groups of related support tickets. |
| `embeddings9_output.json` | Saved vector data for incident similarity search. |
| `__init__.py` | Marks the folder as a Python package. |

### `deployment/`

Contains the services and workflows used to run the support system.

| File | Description |
| --- | --- |
| `pipeline_service.py` | Runs the ticket API and the main support pipeline. |
| `admin_panel.py` | Provides a Gradio panel for reviewing problem clusters. |
| `epc_pipeline_workflow.yaml` | Defines the cloud workflow for the EPC pipeline. |
| `__init__.py` | Marks the folder as a Python package. |
| `.gradio/certificate.pem` | Certificate file used by the Gradio service. |
| `README.md` | Notes for the deployment folder. |

### `guardrails/`

Checks ticket text before processing and checks results before they are returned.

| File | Description |
| --- | --- |
| `input_guardrails.py` | Cleans and checks incoming ticket text. |
| `output_guardrails.py` | Checks generated results before they leave the system. |
| `__init__.py` | Marks the folder as a Python package. |
| `README.md` | Notes for the guardrails folder. |

### `integrations/`

Connects the support system to outside services and communication tools.

| File | Description |
| --- | --- |
| `gmail_tool.py` | Reads or works with Gmail support messages. |
| `drive_tool.py` | Works with files and records in Google Drive. |
| `discord_notifier.py` | Sends support updates to Discord. |
| `authorize_google.py` | Handles Google service authorization. |
| `mcp_server.py` | Exposes integration tools through an MCP server. |
| `test_mcp_client.py` | Tests the MCP client connection. |
| `__init__.py` | Marks the folder as a Python package. |
| `README.md` | Notes for the integrations folder. |

### `memory/`

Moves processed support records into long-term Google Cloud storage.

| File | Description |
| --- | --- |
| `migrate_tickets_to_firestore.py` | Copies ticket records into Firestore. |
| `migrate_clusters_to_firestore.py` | Copies cluster records into Firestore. |
| `migrate_incidents_to_bigquery.py` | Copies incident records into BigQuery. |
| `__init__.py` | Marks the folder as a Python package. |
| `README.md` | Notes for the memory folder. |

### `monitoring/`

Provides a place for health checks, logs, and system monitoring features.

| File | Description |
| --- | --- |
| `__init__.py` | Marks the folder as a Python package. |
| `README.md` | Notes for the monitoring folder. |

### `rag/`

Uses retrieval-augmented generation tools to find incidents that are similar to a new ticket.

| File | Description |
| --- | --- |
| `hybrid_retrieval.py` | Combines keyword and vector search for better matches. |
| `query_similar_incidents.py` | Searches for incidents similar to a given problem. |
| `generate_embeddings.py` | Creates vector representations of incident text. |
| `create_index.py` | Creates a search index for stored embeddings. |
| `deploy_index.py` | Publishes the search index to its cloud service. |
| `undeploy_index.py` | Removes a deployed search index. |
| `embeddings_output.json` | Stores one set of generated embeddings. |
| `embeddings9_output.json` | Stores another set of generated embeddings. |
| `embeddingsnew_output.json` | Stores newer generated embeddings. |
| `embeddingsw2_output.json` | Stores an additional embedding set. |
| `__init__.py` | Marks the folder as a Python package. |
| `README.md` | Notes for the retrieval folder. |

### `testing/`

Holds shared testing code as the test area grows.

| File | Description |
| --- | --- |
| `__init__.py` | Marks the folder as a Python package. |

## Root Files

| File | Description |
| --- | --- |
| `Dockerfile` | Describes how to package the application in a container. |
| `requirements.txt` | Lists the Python libraries used by the project. |
| `help.md` | Stores extra help and project notes. |
| `setup_env.sh` | Sets up the project environment on Linux or macOS. |
| `setup_env.bat` | Sets up the project environment on Windows. |
| `deploy_epc_pipeline.sh` | Deploys the EPC pipeline from a shell. |
| `deploy_epc_workflow.sh` | Deploys the EPC workflow from a shell. |
| `deploy_epc_admin_panel.sh` | Deploys the admin panel from a shell. |
| `deploy_epc_admin_panel.bat` | Deploys the admin panel from Windows. |
| `testrun_workflow.sh` | Runs a workflow test from a shell. |
| `.gitignore` | Lists files that Git should not track. |
| `.gitgnore` | An older misspelled ignore file kept in the project. |

## Main Technologies

- Python for the application code.
- Google Cloud Firestore for ticket and cluster records.
- Google BigQuery for incident data.
- Google Cloud AI tools for language and embedding tasks.
- Flask for the pipeline API.
- Gradio for the admin panel.
- Docker and Cloud Run tools for deployment.

## Project Goal

The goal is to help support teams handle repeated problems faster. Instead of reading every ticket by hand, the system finds patterns, shows which problems matter most, and gives teams a clear path for review and escalation.
