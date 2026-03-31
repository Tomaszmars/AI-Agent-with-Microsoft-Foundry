# Lab 1 — Build and Deploy an Intelligent AI Agent with Microsoft Foundry

## Overview
In this lab, you will build and deploy an intelligent AI agent using Microsoft Foundry (Foundry IQ + MCP). You will:
- Create a Foundry Project (workspace)
- Prepare the environment for later labs (knowledge, search, storage, and client interaction)

## Challenge Task 1: Create a Foundry Project

### Step 1: Access the Microsoft Foundry Portal
Open the Microsoft Foundry portal.

### Step 2: Enable the New Foundry Experience
Turn on the **New Foundry Experience** (if prompted).

### Step 3: Create and configure the project
Create a new project with the following settings:

- **Project name:** `agent-projectXXXX` (replace `XXXX` with your unique identifier)
- **Subscription:** Use the default subscription
- **Resource group:** Create a new resource group named `newagent12-RG`
- **Microsoft Foundry resource:** Use the default
- **Region:** Choose one: **East US 2**, **Australia East**, or **West US**

## Challenge Task 2: Create an Agent

### Objective
Create an AI agent in your Foundry project using a default language model. The agent will act as a product expert and will later connect to enterprise knowledge sources.

### Step 1: Configure the agent
From the project home page, create a new agent with:

- **Agent name:** `product-expert-agent`

### Step 2: Verify provisioning
After the agent is created, confirm that:
- A default language model (for example, `gpt-4.1-mini` or `gpt-4.1`) is automatically deployed.
- The agent playground opens with the model already selected and ready for testing.

## Challenge Task 3: Configure Your Agent and Foundry IQ

### Objective
Define the agent's role-based instructions and connect it to Foundry IQ, enabling the agent to retrieve grounded, knowledge-based responses instead of relying solely on the base model.

## Notes / Conventions
- Replace `XXXX` in names like `agent-projectXXXX` with a unique identifier (for example, initials + 4 digits).
- Use the region that best matches your training requirements: **East US 2**, **Australia East**, or **West US**.