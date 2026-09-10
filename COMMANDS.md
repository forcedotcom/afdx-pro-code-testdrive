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
Without inspecting local files, figure out how to run `sf agent validate authoring-bundle`?
```

---

### Call any Salesforce API from the CLI.

#### Go beyond deploy and retrieve. Reach REST, Bulk, Connect, Tooling, and Graph.

##### Data Query
```
sf data query --query "SELECT Id, Name FROM Account LIMIT 5"
```
##### GraphQL Query
```
sf api request graphql --body "query accounts { uiapi { query { Account(first: 5) { edges { node { Id Name { value } } } } } } }"
```
##### Connect API
```
sf api request rest "/services/data/v64.0/connect/organization"
```

---

### The CLI is extensible and keeps growing with Salesforce.

#### Every plugin inherits the CLI's trusted auth, capabilities, and libraries.
```
sf plugins
```
#### You can extend it too. Agents like Agentforce Vibes and Claude now help you build plugins, and the community is growing.
```
sf plugins discover
```

---

