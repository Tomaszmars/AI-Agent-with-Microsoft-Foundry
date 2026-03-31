# Challenge Lab Project 1: Build and Deploy an Intelligent AI Agent with Microsoft Foundry

## Challenge Task 1: Create a Foundry Project

**Objective:**  
Establish the foundational Microsoft Foundry project that will serve as the central workspace for building and managing AI agents, including the required infrastructure, identity, and endpoint configuration.

### Instructions

#### Step 1: Access the Microsoft Foundry portal

1. Open the Microsoft Foundry portal in your browser.  
2. Sign in with your lab or organizational account if prompted.

#### Step 2: Enable the new Foundry experience

1. If the portal offers a toggle or banner for the **new Foundry experience**, enable it.  
2. Confirm that the UI refreshes to the new experience before proceeding.

#### Step 3: Create and configure the project

Create a new project with the following configuration:

* **Project name:** `agent-projectXXXX`  
  *Replace `XXXX` with your unique identifier (for example, `agent-project1234`).*

* **Subscription:** Use the **default** subscription provided in the lab environment.

* **Resource group:**  
  * Select **Create new resource group**  
  * Name it: `newagent12-RG`

* **Microsoft Foundry resource:** Keep the **default** selection.

* **Region:** Choose one of the following (as appropriate for your lab environment):  
  * **East US 2**  
  * **Australia East**  
  * **West US**

After saving, wait for the project creation to complete before moving to the next task.

---

## Challenge Task 2: Create an Agent

**Objective:**  
Create an AI agent within the Foundry project using a default language model. Configure this agent to act as a product expert and interact with enterprise knowledge sources.

### Instructions

#### Step 1: Configure the agent

1. In your Foundry project, navigate to the **Agents** section.  
2. Select **Create agent** (or equivalent).  
3. Provide a name and basic description for the agent (for example, *Contoso Product Expert*).  
4. Keep the default language model selection for now (for example, `gpt-4.1-mini` or `gpt-4.1`).  
5. Save the agent configuration.

#### Step 2: Verify agent provisioning

After the agent is created:

* A **default language model** (such as `gpt-4.1-mini` or `gpt-4.1`) should be automatically deployed and associated with the agent.  

* The **agent playground** should open with the model pre-selected and ready for interaction (you should see a chat interface where you can send test prompts).

If the playground does not open automatically, navigate to the agent and open the playground manually to confirm the model is active.

---

## Challenge Task 3: Configure Your Agent and Foundry IQ

**Objective:**  
Define the agent's role-based instructions and connect it to Foundry IQ so the agent retrieves grounded, knowledge-based responses instead of relying solely on the base model.

### Instructions

#### Step 1: Configure agent instructions

Update the agent configuration with the following instruction (system prompt):

```text
You are a helpful AI assistant for Contoso, specializing in outdoor camping and hiking products.

You must ALWAYS search the knowledge base to answer questions about our products or product catalog. Provide detailed, accurate information and always cite your sources.

If you don't find relevant information in the knowledge base, say so clearly.
```

Then:

1. Paste the instruction into the **Agent instructions** or **System message** field.  
2. Review for typos and ensure the full text is included.  
3. Save the updated configuration and confirm there are no validation errors.

#### Step 2: Connect to Foundry IQ

1. In the agent configuration, navigate to the **Knowledge** (or **Knowledge sources**) section.  
2. Select **Connect to Foundry IQ**.  
3. Choose **Connect to an AI Search resource**.  
4. Select **Create new resource**.  
   * This action will open the **Azure portal** in a new browser tab to provision the required **AI Search** resource.

5. In the Azure portal, complete the creation of the AI Search resource using the default or lab-specified settings.  
6. After provisioning completes, return to the **Foundry portal** tab.  
7. Refresh or re-open the **Connect to Foundry IQ** dialog if needed, then select the newly created AI Search resource to complete the connection.

Once connected, your agent will use Foundry IQ to retrieve grounded answers from the knowledge base before responding.

---

### Step 3: Create and configure the AI Search resource

Provision an **AI Search** resource with the following configuration:

* **Subscription:** Keep the **default** subscription.

* **Resource group:** `newagent12-RG`

* **Service name:** `search-serviceXXXX`  
  *Replace `XXXX` with your unique identifier (for example, `search-service1234`).*

* **Location:** Choose one of the following regions (as appropriate for your lab environment):  
  * **West US 2**  
  * **West US 3**  
  * **Canada East**

* **Pricing tier:** **Standard**

* **Compute type:** **Default**

After provisioning:

1. Open the newly created **AI Search** resource in the Azure portal.  
2. Go to the **Keys** section.  
3. Under **API access control**, make sure **both available options** are enabled (as required in the lab instructions).  
4. If you changed the settings, click **Save** and wait **30–60 seconds** for the changes to propagate.  
5. Return to the **Foundry portal** and click **Refresh** on the **Foundry IQ** page, then confirm that the AI Search resource is successfully connected to the agent (no errors in the Knowledge/Foundry IQ connection status).

> **Note:** Misconfigured API access is a common cause of “Failed to fetch knowledge bases for connection …” errors when Foundry IQ tries to use the search service.

---

## Challenge Task 4: Clone Repository, Create Storage Account, and Upload Data

**Objective:**  
Create an Azure Blob Storage account and upload product-related PDF documents that will serve as the enterprise knowledge source for the AI agent.

### Instructions

#### Step 1: Clone the repository

1. Open **Visual Studio Code** (or your preferred IDE) on the lab VM or your local machine.  
2. Open a **terminal** window in the IDE.  
3. Run the following command to clone the lab repository to a local folder named `ai-agents`:

   ```bash
   git clone https://github.com/technofocus-pte/mslearn-ai-agents.git ai-agents
   ```

4. Change into the cloned repository folder:

   ```bash
   cd ai-agents
   ```

5. Verify that the project files (including any `data` or `docs` folders) are present in the `ai-agents` folder before proceeding to storage configuration.

#### Step 2: Create a Storage Account

1. In the **Azure portal**, select **Create a resource** &gt; **Storage account**.  
2. Configure the storage account with the following settings:

   * **Subscription:** Keep the **default** subscription.  
   * **Resource group:** `newagent12-RG`  
   * **Storage account name:** `agentstorageXXXX`  
     *Replace `XXXX` with your unique identifier (for example, `agentstorage1234`).*  
   * **Region:** Use the same region as your Foundry project where possible (for example, **East US 2**, **Australia East**, or **West US**).  
   * **Performance:** **Standard**  
   * **Redundancy:** **Locally-redundant storage (LRS)** (or the default redundancy option for the lab).  

3. Review and create the storage account. Wait until the deployment completes.

#### Step 3: Create a Blob Container and Upload Product Documents

1. In the Azure portal, open the newly created **Storage account**.  
2. Under **Data storage**, select **Containers**.  
3. Select **+ Container** and create a new container with:

   * **Name:** `contosoproducts`  
   * **Public access level:** **Private (no anonymous access)**

4. Once the container is created, open it and select **Upload**.  
5. Browse to the following folder on the lab VM (or equivalent path in your environment):

   ```text
   C:\Users\demouser\ai-agents\Labfiles\04-integrate-agent-with-foundry-iq\data
   ```

6. Upload the following three PDF files into the `contosoproducts` container:

   * `contoso-tents-catalog.pdf`  
   * `contoso-camping-accessories.pdf`  
   * `contoso-backpacks-guide.pdf`

7. Verify that **all three** PDF files appear in the `contosoproducts` container and that the upload completed successfully with no errors.

These documents will be used later as part of the enterprise knowledge source that your AI agent queries through Foundry IQ.

---

## Challenge Task 5: Connect Your Data with Microsoft Foundry IQ

**Objective:**  
Create a knowledge base in Foundry IQ by linking Azure Blob Storage and Azure AI Search. This process indexes documents, generates embeddings, and makes the data searchable for the agent.

### Instructions

#### Step 1: Connect the Search Service

1. In the Microsoft Foundry portal, navigate back to the **Foundry IQ** (or **Knowledge / Foundry IQ**) page for your agent.  
2. **Refresh** the page to ensure the latest Azure resources are visible.  
3. In the **Search service** section, select your previously created AI Search resource (for example, `search-serviceXXXX`).  
4. Save or confirm the selection.  
5. Verify that the search service shows as **Connected** (no error or warning messages) before proceeding to the next steps.

> **Auth Type recommendation:** When connecting the search service, select **Project Managed Identity** as the authentication type. This uses the Foundry project’s managed identity to access Azure AI Search via RBAC, avoiding hard-coded API keys and aligning with enterprise security best practices. Use **API** auth only for quick tests or special cross-tenant scenarios, and **Entra ID** only if your organization requires a dedicated app registration/service principal for access control.

#### Step 2: Create the Knowledge Base

Initiate the creation of a new knowledge base with the following configuration:

* **Knowledge source type:** **Azure Blob Storage**  
* **Name:** `ks-contosoproducts`  
* **Description:** `Contoso product catalogue items`

* **Storage account name:** Select the storage account you created earlier (for example, `agentstorageXXXX`).  
* **Container name:** `contosoproducts`

* **Content extraction mode:** **Minimal**  
  *Use minimal extraction to keep processing lightweight while still enabling search across document content.*

* **Authentication type:** **API Key**  
  *Use the storage account key for this lab scenario as instructed in the challenge environment.*

> **Note:** If you encounter errors such as “Failed to fetch knowledge bases for connection …” when working with this knowledge base, double-check that you are using a valid storage account key and that the storage account and container (`contosoproducts`) are still present and accessible. Misconfigured or rotated keys are a common cause of connection failures.

* **Include embedding model:** **Selected**  
* **Embedding model:** `text-embedding-3-small`

* **Chat completions model:** `gpt-4.1-mini` or `gpt-4.1`  
  *Select the same model that is currently deployed for your agent to keep behavior consistent.*

Create the knowledge base and wait for the ingestion and indexing process to complete before testing queries against it.

#### Step 3: Finalize and Activate the Knowledge Base

1. In the **Chat completions model** dropdown, confirm that the same model used during agent creation is selected (either `gpt-4.1-mini` or `gpt-4.1`).  
2. Leave all other optional settings at their **default values** unless the lab explicitly instructs otherwise.  
3. Select **Save knowledge base** to initiate document ingestion, embedding generation, and indexing.  
4. After saving, **refresh** the page and verify that the knowledge source status shows **Active**.  
   *If the status remains in a pending or error state, review the search and storage connections (keys, auth types, and resource names) before proceeding.*

#### Step 4: Capture the Project Endpoint

1. In the Microsoft Foundry portal, select **Home** to return to the main project overview.  
2. Locate the **Project endpoint** field for your current project.  
3. Copy the full **Project endpoint URL** value. For example:

   ```text
   https://agent-project2159081-resource.services.ai.azure.com/api/projects/agent-project2159081
   ```

4. Store this value in a secure place (for example, a notes file used only for this lab). You will need it later when configuring the **Python client** to call your agent and knowledge base from code.

---

## Challenge Task 7: Configure Application

**Objective:**  
Prepare the local Python environment and configure the client application to connect to the deployed agent.

### Instructions

#### Step 1: Open the project in Visual Studio Code

1. On the lab VM, open **Visual Studio Code**.  
2. Select **File &gt; Open Folder...**.  
3. Browse to the following path and select the `ai-agents` folder:

   ```text
   C:\Users\demouser\ai-agents
   ```

4. When prompted with the trust dialog, choose **Yes, I trust the authors** to fully enable workspace features and extensions for this project.

#### Step 2: Create and configure a virtual environment

From the project root (`C:\Users\demouser\ai-agents`), run the following commands in the integrated terminal:

1. Create a new virtual environment named `labenv`:

   ```bash
   python -m venv labenv
   ```

2. Activate the virtual environment (Windows PowerShell or Command Prompt):

   ```bash
   .\labenv\Scripts\activate
   ```

3. Navigate to the integration project directory:

   ```bash
   cd Labfiles/04-integrate-agent-with-foundry-iq/Python
   ```

4. Install the required Python dependencies:

   ```bash
   pip install -r requirements.txt
   ```

After installation completes, keep the virtual environment **activated** for the remaining Python configuration steps in this lab.

#### Step 3: Configure environment variables

1. In Visual Studio Code, from the Explorer pane, navigate to:

   ```text
   Labfiles/04-integrate-agent-with-foundry-iq/Python
   ```

2. Open the `.env` file in this directory. It contains configuration values used by the Python client.  
3. Locate the line that defines `PROJECT_ENDPOINT` and replace its value with the **Project endpoint** URL you captured earlier. For example:

   ```env
   PROJECT_ENDPOINT=https://agent-project2159081-resource.services.ai.azure.com/api/projects/agent-project2159081
   ```

4. Leave the other environment variables unchanged unless explicitly instructed by the lab.  
5. Save the `.env` file to apply your changes.

---

## Challenge Task 8: Complete the Agent Client Code

**Objective:**  
Implement the missing logic to connect to the Foundry project, manage conversations, and handle MCP approval flows, enabling programmatic interaction with the AI agent from a Python application.

### Instructions

#### Step 1: Review the starter code

1. In Visual Studio Code, open the `agent_client.py` file located in the same `Python` folder:

   ```text
   Labfiles/04-integrate-agent-with-foundry-iq/Python/agent_client.py
   ```

2. Review the provided starter code, paying particular attention to:

   * **Import statements and configuration loading** – how environment variables (such as `PROJECT_ENDPOINT`) and other settings are read.  
   * The **`send_message_to_agent()` function structure** – parameters, expected behavior, and any TODO comments where you will add logic to call the agent.  
   * The **`display_conversation_history()` function** – how messages and responses are displayed in the console.  
   * The **main program loop** – how user input is read, passed to the agent, and how the loop terminates.

This review will help you understand where to implement the remaining logic in the next steps of this task.

#### Step 2: Understand the client template and TODOs

The `agent_client.py` file includes a starter template with TODO comments guiding what you need to implement. The core structure looks like this:

```python
import os
from dotenv import load_dotenv
from azure.identity import DefaultAzureCredential
from azure.ai.projects import AIProjectClient

# Load environment variables
load_dotenv()
project_endpoint = os.getenv("PROJECT_ENDPOINT")
agent_name = os.getenv("AGENT_NAME")

# Validate configuration
if not project_endpoint or not agent_name:
    raise ValueError("PROJECT_ENDPOINT and AGENT_NAME must be set in .env file")

print(f"Connecting to project: {project_endpoint}")
print(f"Using agent: {agent_name}\n")

# TODO: Connect to the project and create a conversation
# Add your code here to:
# 1. Create DefaultAzureCredential
# 2. Create AIProjectClient with endpoint
# 3. Get the OpenAI client
# 4. Get the agent by name
# 5. Create a new conversation


# Conversation history for context (client-side tracking)
conversation_history = []


def send_message_to_agent(user_message):
    """
    Send a message to the agent and handle the response using the conversations API.
    """
    try:
        print(f"You: {user_message}\n")
        print("Agent: ", end="", flush=True)
        
        # TODO: Add user message to conversation and get response
        # Add your code here to:
        # 1. Add the user message to the conversation using conversations.items.create()
        # 2. Create a response using responses.create() with agent reference
        # 3. Extract and display the response text
        # 4. Check for and display any citations
        
        # Store in conversation history (client-side)
        conversation_history.append({
            "role": "user",
            "content": user_message
        })
        
        # Your code will go here

        # Extract the response text
        if response and response.output_text:
            response_text = response.output_text
            
            print(f"{response_text}\n")
            
            # Check for citations if available
            if hasattr(response, 'citations') and response.citations:
                print("\nSources:")
                for citation in response.citations:
                    print(f"  - {citation.content if hasattr(citation, 'content') else 'Knowledge Base'}")
            
            # Store in conversation history (client-side)
            conversation_history.append({
                "role": "assistant",
                "content": response_text
            })
            
            return response_text
        else:
            print("No response received.\n")
            return None
    except Exception as e:
        print(f"\n\nError: {str(e)}\n")
        return None
```

In the following steps of this task, you will:

* Initialize the **Azure credentials** and **AIProjectClient** using `DefaultAzureCredential` and `AIProjectClient` with the `PROJECT_ENDPOINT` value.  
* Retrieve the **OpenAI client** from the project client and look up your agent by `AGENT_NAME`.  
* Create a **new conversation** that will be reused for all user messages.  
* Implement the logic in `send_message_to_agent()` to send user input to the conversation, call the agent, and print responses and citations.

Use the TODO comments in the code as precise insertion points for your implementation.

#### Step 3: Implement message sending and MCP approval handling

Next, complete the logic inside the `send_message_to_agent()` function where the **second TODO comment** appears. Add the following code in the body of the function (at the indicated TODO) to send messages, handle responses, and process MCP approval requests:

```python
# Add user message to the conversation
openai_client.conversations.items.create(
    conversation_id=conversation.id,
    items=[{"type": "message", "role": "user", "content": user_message}],
)

# Store in conversation history (client-side)
conversation_history.append({
    "role": "user",
    "content": user_message
})

# Create a response using the agent
response = openai_client.responses.create(
    conversation=conversation.id,
    extra_body={"agent_reference": {"name": agent.name, "type": "agent_reference"}},
    input=""
)

# Check if the response output contains an MCP approval request
approval_request = None
if hasattr(response, 'output') and response.output:
    for item in response.output:
        if hasattr(item, 'type') and item.type == 'mcp_approval_request':
            approval_request = item
            break

# Handle approval request if present
if approval_request:
    print(f"[Approval required for: {approval_request.name}]\n")
    print(f"Server: {approval_request.server_label}")
    
    # Parse and display the arguments (optional, for transparency)
    import json
    try:
        args = json.loads(approval_request.arguments)
        print(f"Arguments: {json.dumps(args, indent=2)}\n")
    except:
        print(f"Arguments: {approval_request.arguments}\n")
    
    # Prompt user for approval
    approval_input = input("Approve this action? (yes/no): ").strip().lower()
    
    if approval_input in ['yes', 'y']:
        print("Approving action...\n")
        
        # Create approval response item
        approval_response = {
            "type": "mcp_approval_response",
            "approval_request_id": approval_request.id,
            "approve": True
        }
    else:
        print("Action denied.\n")
        
        # Create denial response item
        approval_response = {
            "type": "mcp_approval_response",
            "approval_request_id": approval_request.id,
            "approve": False
        }
    
    # Add the approval response to the conversation
    openai_client.conversations.items.create(
        conversation_id=conversation.id,
        items=[approval_response]
    )
    
    # Get the actual response after approval/denial
    response = openai_client.responses.create(
        conversation=conversation.id,
        extra_body={"agent_reference": {"name": agent.name, "type": "agent_reference"}},
        input=""
    )
```

This code:

* Adds the **user message** to the existing conversation.  
* Creates a **response** from the agent tied to that conversation.  
* Detects any **MCP approval requests** returned by the agent and interactively prompts the user to approve or deny the action.  
* Sends an **approval or denial response** back into the conversation and then retrieves the final agent response after that decision.

In the next step, you will reuse the `response` object to extract and display the response text and citations (as shown in the lower part of the starter function).

#### Step 4: Test the client application

1. Save your changes in `agent_client.py`.

2. In the same terminal (with the `labenv` virtual environment still activated), sign in to Azure:

   ```bash
   az login
   ```

   *When prompted, choose **Work or school account** and sign in using the credentials provided in the lab’s environment tab.*

3. Run the agent client application:

   ```bash
   python agent_client.py
   ```

4. When the application starts, you should see a header similar to:

   ```text
   Contoso Product Expert Agent
   Ask questions about our outdoor and camping products.
   Type 'history' to see conversation history, or 'quit' to exit.
   ```

5. Test with sample queries, for example:

   * `What tents do you recommend for a family of four?`
   * `What are the key features of Contoso camping accessories?`
   * `Which backpacks are best for multi-day hikes?`

6. Use:

   * `history` – to display the full conversation so far.
   * `quit` – to exit the application.
