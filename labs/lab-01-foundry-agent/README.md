# Lab 1 — Build and Deploy Intelligent AI Agent with Microsoft Foundry

## Overview
In this lab, you will build and deploy an intelligent AI agent using Microsoft Foundry (Foundry IQ + MCP). You will create a Foundry Project/workspace and prepare the environment needed for subsequent tasks (knowledge, search, storage, and client interaction).

## Challenges
# Challenge Task 1: Create a Foundry Project

## Step 1: Access Microsoft Foundry Portal

## Step 2: Enable New Foundry Experience

## Step 3: Create and Configure the Project

Create a new project with the following configuration:

- **Project name:** `agent-projectXXXX` (replace `XXXX` with your unique identifier)
- **Subscription:** Keep default
- **Resource group:** Create a new resource group → Name: `newagent12-RG`
- **Microsoft Foundry resource:** Keep default
- **Region:** East US 2 / Australia East / West US




Task 2: Create an Agent
Objective: Create an AI agent within the Foundry project using a default language model. This agent will be configured to act as a product expert and interact with enterprise knowledge sources.

Instructions
Step 1: Configure the Agent

From the project home page, initiate agent creation with the following configuration:

Agent name: product-expert-agent
Step 2: Verify Agent Provisioning

After the agent is created:

A default language model (such as gpt-4.1-mini or gpt-4.1) should be automatically deployed.

The agent playground should open with the model pre-selected and ready for interaction.

## Notes / Conventions
- Replace `XXXX` in names like `agent-projectXXXX` with a unique identifier (e.g., initials + 4 digits).
- Use the region that matches your training requirements: **East US 2**, **Australia East**, or **West US**.
