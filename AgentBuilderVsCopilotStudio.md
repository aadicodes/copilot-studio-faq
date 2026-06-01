# Agent Builder vs Copilot Studio

**Agent Builder** = lightweight, task-focused AI agents inside Microsoft 365 apps.  
**Copilot Studio** = full enterprise-grade conversational agents with connectors, actions, plugins, data grounding, and ALM.

They are not competing technologies — they serve different layers of the Microsoft AI stack.

---

## Comparison

| Feature | Agent Builder | Copilot Studio |
|---|---|---|
| Primary Purpose | Small, focused agents inside Microsoft 365 | Full conversational copilots for enterprise workflows |
| Where it lives | Inside M365 apps (Word, Excel, Teams, Loop) | Power Platform (Dataverse, connectors, solutions) |
| Complexity | Simple, fast, task-oriented | Advanced, multi-system, enterprise-grade |
| Data Access | Microsoft Graph + local context | Connectors, APIs, Power Automate, Dataverse, SharePoint, SQL, custom plugins |
| Actions | Limited, app-specific | Full action model: flows, connectors, APIs, RAG, grounding |
| ALM / DevOps | None | Full ALM: Dev/Test/Prod, pipelines, managed solutions |
| Governance | M365 governance | Power Platform governance (DLP, connectors, environment roles) |
| Audience | Business users | Pro devs, solution architects, enterprise IT |

---

## Agent Builder

Agent Builder is the personal agent creation tool inside Microsoft 365.

> Build a small helper that performs a specific task inside M365.

**Examples:**
- Document reviewer in Word
- Spreadsheet analyzer in Excel
- Meeting summarizer in Teams
- Customer-email classifier in Outlook

**Key Characteristics**
- No Dataverse, connectors, Power Automate, or ALM
- No multi-environment deployment or enterprise integration
- Runs inside the M365 app context
- Uses Graph grounding and local document context

**Best For**
- Personal productivity
- Department-level micro-automation
- Lightweight assistants and one-off tasks

---

## Copilot Studio

Copilot Studio is the enterprise platform for building, deploying, and governing AI agents.

> Build a full enterprise chatbot that integrates with systems, APIs, workflows, and data sources.

**Key Capabilities**
- Dataverse storage
- Power Automate actions
- 1,100+ connectors + custom connectors
- API plugins
- RAG grounding with SharePoint, websites, files
- Multi-turn conversation design (topics, orchestration, fallback logic)
- Environment variables
- Dev/Test/Prod ALM with Power Platform Pipelines
- Role-based access control
- Telemetry & analytics

**Best For**
- Enterprise workflows (HR, IT, Finance, Customer Service)
- Multi-system automation
- Agents requiring governance, security, or ALM
- Agents deployed to Teams, web, or external channels

---

## How They Fit Together

Microsoft's AI architecture is layered:

| Layer | Platform | Purpose |
|---|---|---|
| Layer 1 | Microsoft 365 Copilot | Personal productivity, embedded in apps, uses Agent Builder |
| Layer 2 | Copilot Studio | Enterprise copilots, multi-system workflows, governed |
| Layer 3 | Custom Plugins & Connectors | Extend both M365 Copilot and Studio agents |

Agent Builder is **not** a replacement for Copilot Studio — and vice versa. They complement each other.

---

## When to Use Which

### Use Agent Builder when:
- You want a small helper inside Word, Excel, or Outlook
- No connectors, APIs, or Power Automate are needed
- No Dev/Test/Prod is required
- The use case is personal or team-specific
- You want fast, simple automation

### Use Copilot Studio when:
- You need enterprise workflows or system integration
- You need to call APIs or Power Automate
- You need RAG grounding
- You need governance, security, or DLP policies
- You need multi-environment ALM
- You need to deploy to Teams or external channels
- You need analytics and monitoring

---

## Decision Framework

| Question | Yes | No |
|---|---|---|
| Does the agent need to integrate with systems outside M365? | Copilot Studio | Agent Builder |
| Does the agent need org-wide deployment? | Copilot Studio | Agent Builder |
| Does the agent need Dev/Test/Prod or ALM? | Copilot Studio | Agent Builder |
| Does the agent need connectors, Power Automate, or APIs? | Copilot Studio | Agent Builder |
| Does the agent need to run outside M365 apps? | Copilot Studio | Agent Builder |

---

## Sharing Agent Builder Agents

You can share an Agent Builder agent — but only within the Microsoft 365 context.

**What you can share with:** individual colleagues, groups, Teams channels, or your entire organization (subject to admin policy).

Sharing is done through M365 permissions, not Power Platform ALM.

### How sharing works
- Colleagues can use the agent inside their M365 apps
- They cannot modify your version without edit rights
- The agent appears in their Copilot sidebar
- The agent runs in **their** Microsoft Graph context (their emails, their files, their chats) — not yours

### What Agent Builder agents cannot do
- Deploy to Teams as an enterprise bot
- Publish to external channels
- Be packaged in Power Platform solutions
- Move through Dev/Test/Prod pipelines
- Use Power Automate flows, external APIs, or connectors
- Use RAG grounding from SharePoint or websites

For any of the above, use Copilot Studio.

---

## Tire Sales Company Examples

### Agent Builder — Email Classifier
> Create an agent in Outlook that classifies incoming customer emails as: **Warranty**, **Return**, **Appointment**, or **Quote request**.

Each team member's agent classifies their own inbox. Fast to build, no connectors needed.

### Copilot Studio — Full Warranty Copilot
> Create a Warranty Copilot that reads customer emails → extracts DOT codes → checks warranty eligibility → creates a Dataverse case → sends a customer response → notifies the store manager → logs the claim for vendor submission. Deployed in Teams for all employees via Dev/Test/Prod pipeline.

Agent Builder cannot do this. Copilot Studio can.

### Use Agent Builder for:
- Classifying or summarizing customer emails
- Drafting customer responses
- Reviewing Word documents or Excel sheets
- Quick helpers for back-office staff

### Use Copilot Studio for:
- Warranty claim automation
- Inventory lookup copilots
- Vendor escalation workflows
- Appointment scheduling bots
- Multi-agent orchestration (Warranty + Inventory + Customer Service)
- Any copilot integrated with your tire inventory system
