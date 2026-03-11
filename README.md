# Agentforce DX Pro-Code Testdrive

Use this hands-on project to learn how to create next-gen Agentforce agents using Agent Script and Agentforce DX.

This Salesforce DX project contains a pre-built agent called Local Info Agent that could be embedded in, for example, a resort's web site. The agent provides local weather updates, shares information about local events, and helps guests with facility hours. 

The agent demonstrates:

- Three types of agent actions (Invocable Apex, Prompt Template, and Flow)
- Mutable variables
- Flow control with `available when`
- Deterministic branching with `if/else` in reasoning instructions

## Prerequisites

- **Salesforce Developer Edition (DE)** org. Get a free one at [developer.salesforce.com/signup](https://developer.salesforce.com/signup). 
- **Salesforce CLI** (`sf`). Download and install it from [developer.salesforce.com/tools/sfdxcli](https://developer.salesforce.com/tools/sfdxcli).  See the [Salesforce CLI Setup Guide](https://developer.salesforce.com/docs/atlas.en-us.sfdx_setup.meta/sfdx_setup/sfdx_setup_install_cli.htm) for more detailed information. 
- **VS Code** with the **Salesforce Extensions** pack and the **Agentforce DX** extension. See [Install Pro-Code Tools](https://developer.salesforce.com/docs/ai/agentforce/guide/agent-dx-set-up-env.html) for details. 
- **Node.js** (v20 or later) and NPM. 

## Setup

### STEP ONE: Prepare your Developer Edition org. 

1. If you haven't already, sign up for a DE org at [developer.salesforce.com/signup](https://developer.salesforce.com/signup).
2. Enable the following features:
   - **Einstein** *(Setup > Einstein > Einstein Generative AI > Einstein Setup)*
     - Some orgs have Einstein enabled by default. If yours already shows Einstein as enabled, you can skip this step.
     - Reload your browser tab after enabling Einstein so Agentforce becomes available in your Setup tree.
   - **Agentforce** *(Setup > Einstein > Einstein Generative AI > Agentforce Studio > Agentforce Agents)*

### STEP TWO: Clone this repo and open it in VS Code.

1. Clone this repo.
   ```
   git clone https://github.com/forcedotcom/afdx-pro-code-testdrive.git
   ```
2. Open the `afdx-pro-code-testdrive` folder in VS Code.
3. Open the integrated terminal in VS Code. *(From the top menu, select View > Terminal.)*

 ⚠️  Run All CLI commands from the VS Code integrated terminal from this point forward.

### STEP THREE: Connect to your org.

Authorize your DE org for use with Salesforce CLI.

```
sf org login web -s -a AFDX-Testdrive
```

You can also use the VS Code **SFDX: Authorize an Org** command from the Command Palette.

### STEP FOUR: Run the setup script.

The setup script deploys source, assigns permissions, and creates a dedicated agent user. Agentforce agents run as a dedicated user with the **Einstein Agent User** profile — this user is the runtime identity for your agent.

 ⚠️  If the setup script fails, follow the [Manual Setup](#manual-setup) instructions at the end of this README to continue.

Run the setup script from the VS Code integrated terminal:

**macOS / Linux / WSL:**
```
./setup
```
**Windows:**
```
setup.cmd
```

When the script finishes, note the username of the new agent user in the output. It appears in the task titled `Create agent user (afdx-agent-XXXXXXXX@testdrive.org)`. You need this username in the next step.

 💡 You can also find the new agent username in the `Username` field on line 9 of `data-import/User.json`.

### STEP FIVE: Configure and deploy the agent.

1. Open `force-app/main/default/aiAuthoringBundles/Local_Info_Agent/Local_Info_Agent.agent` in the VS Code editor.
2. Replace the temporary value of the `default_agent_user` option (line 11) with the agent username from the previous step.
3. Deploy the updated agent from the VS Code integrated terminal by running this command:
   ```
   sf project deploy start -m AiAuthoringBundle:Local_Info_Agent
   ```

The `.agent` file you just edited uses the Agent Script language. This single readable script file defines the entire agent, such as its topics, reasoning instructions, variables, and actions.

## What's Inside This Project?

| Component | Type | Purpose |
|---|---|---|
| `Local_Info_Agent.agent` | Agent Script | The agent definition — topics, reasoning, variables, and flow control |
| `CheckWeather` | Apex Class | Invocable Apex. Checks current weather conditions for a given location |
| `CurrentDate` | Apex Class | Invocable Apex. Returns the current date for use by the agent |
| `WeatherService` | Apex Class | Provides mock weather data for the resort|
| `Get_Event_Info` | Prompt Template | Retrieves local events |
| `Get_Resort_Hours` | Flow | Returns facility hours and reservation requirements |
| `Resort_Agent` | Permission Set | Agent user permissions (Einstein Agent license) |
| `Resort_Admin` | Permission Set | Admin/developer Apex class access |
| `AFDX_Agent_Perms` | Permission Set Group | Bundles agent user permissions for assignment |
| `AFDX_User_Perms` | Permission Set Group | Bundles admin user permissions for assignment |

## Learning Exercise

Use the Agentforce DX panel in VS Code to start a conversation with the Local Info Agent.

1. Open the `Local_Info_Agent.agent` Agent Script file.
2. Right-click inside the agent and select **AFDX: Preview this Agent**.
3. Click the **Start Simulation** button. If you see **Start Live Test** instead, click the down-arrow and select **Simulation** first.

### Suggested Prompts

Try these prompts to see each type of agent action in action:

- *"What's the weather like today?"* — triggers an Apex action.
- *"I'm interested in movies. What's showing nearby?"* — triggers a Prompt Template action.
- *"When does the spa open?"* — triggers a Flow action.

### Suggested Next Steps

1. [Learn about Agent Script](https://developer.salesforce.com/docs/ai/agentforce/guide/agent-script.html).
1. Change how the Local Info Agent behaves by editing its Agent Script file.
1. Right-click inside the agent and select **AFDX: Validate this Agent** to ensure that the Agent Script file is still valid.
1. Click the **Compile & Restart** button in the Preview Panel and then ask a question to test your changes.

## Manual Setup

The setup script can sometimes fail if, for example, a firewall is blocking `npm`. In which case, run the equivalent steps manually from the VS Code integrated terminal. After you complete **STEP THREE** above, run the steps in this section instead of **STEP FOUR**.

### Deploy and Assign Permission Sets

Run these commands:

```
sf org assign permset -n EinsteinGPTPromptTemplateManager -n EinsteinGPTPromptTemplateUser
sf project deploy start --source-dir force-app
sf org assign permset -n AFDX_User_Perms
```

### Create the Agent User

Agentforce agents run as a dedicated user with the **Einstein Agent User** profile. Query for the profile ID, update `data-import/User.json` with the results, then import the user.

1. Get the profile ID:
   ```
   sf data query -q "SELECT Id FROM Profile WHERE Name='Einstein Agent User'"
   ```
2. Open `data-import/User.json`. Replace the `ProfileId` value on line 8 with the ID from the query. Replace `SOMETHING_UNIQUE` in the `Username` value on line 9 with something unique to you (e.g. your name).
   ![Update User.json with the profile ID and a unique username.](images/agent-user-data-import.png)
3. Import the user and assign permissions:
   ```
   sf data import tree --files data-import/User.json
   sf org assign permset -n AFDX_Agent_Perms -b USERNAME_OF_YOUR_AGENT_USER
   ```

After completing these steps, continue with **STEP FIVE** above.
