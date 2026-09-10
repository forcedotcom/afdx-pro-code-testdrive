# DF26 Demo: Streamline development with the Salesforce CLI

## CLI Commands

### The Salesforce CLI is the headless workhorse of the Salesforce Platform.

#### Secure, trusted auth to any org.
```
sf org list
```
#### Does the real work: deploy, retrieve, test, data, org lifecycle.
```
sf apex run test -t CurrentDateTest --wait 5  
```

---

### The Salesforce CLI is built for humans.

#### Use `sf search`, your Salesforce superpower for finding commands.
```
sf search # Then search for "validate"
```
#### Every command explains itself with `--help`, so you never memorize.
```
sf agent validate -h  
```
#### Use autocomplete and stay productive without memorizing.
```
sf agent
```
#### Many long-running commands show status as you go.
```
sf agent validate authoring-bundle -n Local_Info_Agent
```

---

### The Salesforce CLI is optimized for agents.

#### Structured `--json` output lets an agent act on results, not just read them.
```
sf agent validate authoring-bundle -n Local_Info_Agent --json
```

#### Self-documentation lets agents understand the CLI.
```
How would you call `sf agent validate authoring-bundle`?
```


### Behind every Salesforce skill is the CLI.

* Every Salesforce skill teaches an agent to use the CLI for real work.
* Without the CLI, those skills have nothing to run.
* The CLI is the engine under the skills you hear about at the keynote.

### Call any Salesforce API from the CLI.

* Go beyond deploy and retrieve. Reach REST, Bulk, Connect, Tooling, and Graph.
* One trusted connection reaches everything the platform exposes.
* Your agents get that same reach. Anything the API does, an agent can drive.

### The CLI is extensible and keeps growing with Salesforce.

* Every plugin inherits the CLI's trusted auth, capabilities, and libraries.
* Salesforce teams add headless paths to their services. The agent plugin proves a plugin does far more than move metadata.
* You can extend it too. Agents like Agentforce Vibes and Claude now help you build plugins, and the community is growing.

### Getting started with the Salesforce CLI.

* Install in minutes.

## Staffer Note

For a visitor who fears the terminal, do not sell mastery. Sell the linchpin. They do not need to master the CLI. Their agents do, and the CLI is what lets those agents work.
