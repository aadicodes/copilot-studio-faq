# Dev / Test / Prod Setup for Custom Agents in Copilot Studio  
### With Automated Deployment via Power Platform Pipelines

---

## 0. Overview

This guide walks through, step by step, how to:

1. Create **Dev, Test, and Prod** environments for Copilot Studio.
2. Build custom agents as **solution‑aware** assets.
3. Configure **Power Platform Pipelines** for ALM.
4. Deploy agents from **Dev → Test → Prod** using an automated pipeline.

This assumes you’re using:

- **Microsoft Copilot Studio** (Power Platform)
- **Dataverse** environments
- **Power Platform Pipelines** for CI/CD

---

## 1. Prerequisites

Before you start, ensure:

- **Licensing**
  - Power Platform / Copilot Studio licenses assigned.
  - Dataverse available for your tenant.

- **Permissions**
  - Power Platform admin or environment admin.
  - Ability to create environments and install apps.

- **Tools**
  - Access to **Power Platform Admin Center**.
  - Access to **Power Apps** and **Copilot Studio**.
  - (Optional) Azure DevOps / GitHub if you want external source control.

---

## 2. Create Dev, Test, and Prod Environments

### 2.1 Open Power Platform Admin Center

1. Go to: `https://admin.powerplatform.microsoft.com`
2. Sign in with admin credentials.

### 2.2 Create the Dev Environment

1. Go to **Environments → + New**.
2. Set:
   - **Name:** `Copilot-Dev`
   - **Type:** *Sandbox* (recommended for Dev)
   - **Region:** same region as your users/data.
   - **Dataverse:** **Create a database** (required).
3. Click **Save** and wait for provisioning.

### 2.3 Create the Test Environment

1. **Environments → + New**.
2. Set:
   - **Name:** `Copilot-Test`
   - **Type:** *Sandbox* or *Production* (often Sandbox).
   - **Managed:** enable **Managed environment** if available (recommended for Test/Prod).
   - **Dataverse:** **Create a database**.
3. Save and wait for provisioning.

### 2.4 Create the Prod Environment

1. **Environments → + New**.
2. Set:
   - **Name:** `Copilot-Prod`
   - **Type:** *Production*.
   - **Managed environment:** **On** (strongly recommended).
   - **Dataverse:** **Create a database**.
3. Save and wait for provisioning.

> **Rule:** No direct edits in **Prod**. All changes flow Dev → Test → Prod via solutions and pipelines.

---

## 3. Create a Pipeline Host (Orchestration) Environment

Power Platform Pipelines need a **host environment** where the pipeline app lives.

### 3.1 Create Host Environment

1. In Admin Center, **Environments → + New**.
2. Set:
   - **Name:** `Pipelines-Host`
   - **Type:** *Production* or *Sandbox*.
   - **Enable Dynamics 365 apps:** **Yes** (required for Pipelines app).
   - **Dataverse:** **Create a database**.
3. Save.

### 3.2 Install Power Platform Pipelines App

1. Go to **Power Apps** (`https://make.powerapps.com`).
2. Switch to **Pipelines-Host** environment.
3. Go to **Apps → Dynamics 365 apps / Resources**.
4. Find and **Install**: **Power Platform Pipelines**.
5. Wait for installation to complete.

---

## 4. Prepare Dev Environment for Copilot Studio Development

### 4.1 Open Copilot Studio in Dev

1. Go to `https://copilotstudio.microsoft.com`.
2. Switch environment to **Copilot-Dev**.
3. Confirm you can:
   - Create agents.
   - Access Dataverse tables (if needed).

### 4.2 Use Solutions for All Assets

You must package agents as **solution‑aware** assets.

1. In **Power Apps** (Dev environment):
   - Go to **Solutions → + New solution**.
   - Name: `TireCompany-Copilot-Agents`.
   - Publisher: create or use existing (e.g., `TireCo`).
   - Version: `1.0.0.0`.
2. Save the solution.

### 4.3 Build Agents Inside the Solution

1. Open the `TireCompany-Copilot-Agents` solution.
2. Click **+ New → App → Copilot Studio agent** (or similar entry).
3. Create your custom agent(s):
   - Define topics, actions, plugins, connections.
   - Configure environment variables for URLs, API keys, etc.
4. Save and test in **Dev**.

> **Tip:** Use **environment variables** for anything that changes between Dev/Test/Prod (e.g., API endpoints).

---

## 5. Configure Power Platform Pipelines (Dev → Test → Prod)

### 5.1 Open Deployment Pipeline Configuration App

1. Switch to **Pipelines-Host** environment in **Power Apps**.
2. Find app: **Deployment Pipeline Configuration**.
3. Click **Play** to open.

### 5.2 Register Environments

Inside the configuration app:

1. Go to **Environments**.
2. Add:
   - `Copilot-Dev` (Source).
   - `Copilot-Test` (Intermediate).
   - `Copilot-Prod` (Target).
3. Ensure **Environment IDs** match those in Admin Center.

### 5.3 Create a Pipeline

1. Go to **Pipelines**.
2. Click **+ New pipeline**.
3. Set:
   - Name: `Copilot-Agents-ALM`.
   - Description: “Dev → Test → Prod for Copilot Studio agents”.
4. Add stages:
   - **Stage 1:** Dev → Test
   - **Stage 2:** Test → Prod
5. Link each stage to the correct environment.

> **Recommendation:** Use **Test** and **Prod** as **Managed** environments so solutions are imported as **managed**.

---

## 6. Configure Solution for ALM

### 6.1 Make Solution “Pipeline‑Ready”

In **Dev** environment:

1. Open **Solutions → TireCompany-Copilot-Agents**.
2. Ensure all Copilot agents, environment variables, connections, and related assets are inside this solution.
3. Save and publish all customizations.

### 6.2 Export as Managed for Higher Stages

Pipelines will handle export/import, but conceptually:

- Dev: **Unmanaged** solution (where you build).
- Test/Prod: **Managed** solution (immutable, no direct edits).

Pipelines will:

1. Export from Dev as **managed**.
2. Import into Test.
3. Export from Test (if needed) and import into Prod.

---

## 7. Set Up Automated Deployment via Pipelines

### 7.1 Trigger Deployment from Dev

1. In **Power Apps**, switch to **Copilot-Dev**.
2. Go to **Solutions → TireCompany-Copilot-Agents**.
3. Click **Deploy** (or **Pipeline** button, depending on UI).
4. Choose pipeline: `Copilot-Agents-ALM`.
5. Select target stage: **Dev → Test**.
6. Confirm deployment.

The pipeline will:

- Export the solution from Dev.
- Import it into Test.
- Apply any configured pre/post steps.

### 7.2 Validate in Test

In **Copilot-Test** environment:

1. Open **Copilot Studio**.
2. Confirm:
   - Agents are present.
   - Environment variables are set correctly for Test.
   - Connections are configured (may need re‑auth).
3. Run test conversations.

### 7.3 Promote from Test to Prod

Once validated:

1. In **Power Apps**, switch to **Copilot-Test**.
2. Open **Solutions → TireCompany-Copilot-Agents**.
3. Click **Deploy** via pipeline.
4. Choose stage: **Test → Prod**.
5. Confirm deployment.

In **Copilot-Prod**:

- Verify agents.
- Configure any Prod‑specific environment variables.
- Confirm connections.
- Publish agents for end users.

---

## 8. Add Quality Gates and Automation (Optional but Recommended)

### 8.1 Automated Tests with Copilot Studio Kit (Advanced)

You can integrate:

- **Copilot Studio Kit**
- **Power Automate cloud flows**
- **Dataverse** test data

To:

- Run automated test conversations.
- Validate responses.
- Block deployment if tests fail.

Typical flow:

1. Pipeline triggers a **Power Automate** flow on deployment request.
2. Flow:
   - Pauses deployment.
   - Runs test suite against the agent.
   - Evaluates results.
   - Approves or rejects deployment.

### 8.2 Approvals and Governance

Add:

- Manual approval steps before Test/Prod.
- Role‑based access control (RBAC) for who can:
  - Edit in Dev.
  - Approve Test.
  - Approve Prod.

---

## 9. Source Control Integration (Optional)

If you want Git/Azure DevOps/GitHub:

1. Use **Solution export** as artifacts.
2. Store solution `.zip` in a repo.
3. Use:
   - **Azure DevOps Pipelines** or
   - **GitHub Actions**
4. Automate:
   - Export from Dev.
   - Commit to repo.
   - Deploy to Test/Prod via Power Platform CLI or Pipelines.

---

## 10. Operational Best Practices

- **No direct edits in Test/Prod** — only via solutions.
- **Version your solutions** (e.g., `1.0.0.0`, `1.1.0.0`).
- **Document environment variables** per environment.
- **Monitor**:
  - Conversation analytics.
  - Errors.
  - User feedback.
- **Rollback plan**:
  - Keep previous managed solution versions.
  - Re‑import older version if needed.

---

## 11. Quick Checklist

- [ ] Dev, Test, Prod environments created with Dataverse.  
- [ ] Pipelines‑Host environment created with Dynamics apps enabled.  
- [ ] Power Platform Pipelines app installed.  
- [ ] Copilot agents built inside a **solution** in Dev.  
- [ ] Pipeline configured: Dev → Test → Prod.  
- [ ] Test & Prod set as **Managed** environments.  
- [ ] Environment variables used for per‑env config.  
- [ ] Deployment tested Dev → Test → Prod.  
- [ ] Governance: approvals, roles, and rollback defined.  

---

**You now have a Dev/Test/Prod ALM setup for Copilot Studio agents with automated deployment via Power Platform Pipelines.**
