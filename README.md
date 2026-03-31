# AI Agent with Microsoft Foundry (Foundry IQ + MCP)

This repository contains a **challenge lab** that introduces **Microsoft Foundry** and **Foundry IQ**—platforms for building **knowledge-grounded AI agents** with **enterprise security** and **Model Context Protocol (MCP)** governance.

You will provision Azure resources, connect enterprise documents to an agent using retrieval (RAG), and run a Python client that interacts with the agent through the Conversations API while handling MCP approval prompts.

## What you’ll build

- A Foundry project/workspace for AI development and governance
- A knowledge service (Foundry IQ) connected to enterprise documents
- Vector/semantic retrieval with **Azure AI Search**
- Secure storage of source documents in **Azure Blob Storage**
- An agent configured with role instructions, knowledge grounding, citations, and conversation memory
- A **Python client application** that calls the Conversations API and implements MCP approval handling

## Core architecture

| Component | Purpose |
|---|---|
| **Microsoft Foundry Platform** | Unified AI development platform for project management, model deployment, and agent orchestration with security and governance. |
| **Foundry IQ Knowledge Service** | Knowledge management service that connects enterprise data to agents via semantic search + RAG. |
| **Azure AI Search** | High-performance search with vector capabilities for semantic document retrieval and grounding. |
| **Azure Blob Storage** | Secure storage for enterprise documents (e.g., product catalogs, technical documentation). |
| **Model Context Protocol (MCP)** | Governance framework that requires explicit user approval before the agent accesses external tools/knowledge sources. |
| **Python client application** | Demonstrates programmatic interaction with the agent via the Conversations API, including MCP approvals. |

## Agent capabilities

- **Role-based instructions**: prompts that define the agent’s domain expertise and behavior
- **Knowledge base integration**: seamless grounding on indexed enterprise documents
- **Citation system**: automatic source attribution for knowledge-based answers
- **Conversation management**: persistent context/memory across user sessions

## Prerequisites

### Required tools

- **Azure Portal**: https://portal.azure.com/
- **Visual Studio Code**
- **Python 3.8+** (client app development): https://www.python.org/downloads/
- **Git** (clone repositories, version control): https://git-scm.com/downloads/
- **Azure CLI** (resource management/auth): https://docs.microsoft.com/en-us/cli/azure/install-azure-cli

### Required permissions

Your Azure account must have:

- **Contributor** role
- **Cognitive Services Contributor** permissions

> **Note:** Lack of proper permissions is the #1 cause of deployment failures.

## Getting started (high level)

1. **Clone the repo**
   ```bash
   git clone https://github.com/Tomaszmars/AI-Agent-with-Microsoft-Foundry.git
   cd AI-Agent-with-Microsoft-Foundry
   ```

2. **Sign in to Azure**
   ```bash
   az login
   az account show
   ```

3. **Open the project in VS Code** and follow the lab instructions in this repository.

## Repository structure

This repo is designed as a lab. Typical contents may include:

- `docs/` – step-by-step lab guide and screenshots
- `client/` – Python client application
- `infra/` – deployment templates/scripts (if provided)

(Your exact folders may vary depending on the lab version.)

## Troubleshooting

- If deployments fail, first verify you have **Contributor** + **Cognitive Services Contributor** permissions in the target subscription.
- Ensure you’re using **Python 3.8+** and that `az` is installed and authenticated.

## Contributing

Issues and PRs are welcome. Please include:

- What you expected vs. what happened
- Steps to reproduce
- Logs/screenshots (remove secrets)

## License

Add a license if/when you are ready to publish this repository publicly.