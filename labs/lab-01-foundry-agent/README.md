#### Step 3: Create and Configure the AI Search Resource

Provision an AI Search resource with the following configuration:

- **Subscription:** Keep default
- **Resource group:** `newagent12-RG`
- **Service name:** `search-serviceXXXX` (replace `XXXX` with unique identifier)
- **Location:** West US 2 / West US 3 / Canada East
- **Pricing Tier:** Standard
- **Compute Type:** Default

After provisioning:

- Access the resource settings.
- Enable both options under **API access control** in the **Keys** section.

> **Important:** The AI Search resource must be successfully connected to the agent through Foundry IQ.