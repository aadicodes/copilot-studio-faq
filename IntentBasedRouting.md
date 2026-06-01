# **How Microsoft 365 Copilot Routes to Custom Agents**
## *Intent-Based Invocation & Semantic Routing Explained*

Microsoft 365 Copilot does **not** allow users to directly call a custom agent (no @mentions, no explicit selection).  
Instead, it uses a **semantic routing engine** that decides whether your custom agent should be invoked based on the **intent** of the user’s prompt.

This document explains:
- What “intent-based invocation” means  
- How semantic routing works  
- How to influence routing as a Maker  
- How to make Copilot reliably call your agent on specific phrases  
- A Technyble-grade routing optimization checklist  

---

# **1. What “Invocation Is Intent-Based” Means**

When a user types a prompt in Microsoft 365 Copilot:

1. Copilot rewrites the prompt internally  
2. It compares the rewritten intent against:  
   - Your agent’s **Instructions**  
   - Your **Topics**  
   - Your **Tools**  
   - Your **Knowledge**  
3. If your agent is the *best semantic match*, Copilot invokes it  
4. Your agent runs as a **sub-agent**  
5. Copilot blends the agent’s output into the final answer  

There is **no manual override**.  
Everything is **semantic**, not explicit.

---

# **2. What Semantic Routing Looks For**

Microsoft 365 Copilot routes to your agent when:

### ✔ The user’s prompt matches your agent’s domain  
Example:  
If your agent handles tire inventory, prompts like:  
- “Check tire stock”  
- “Do we have 225/65R17”  
- “Look up SKU availability”  
…will route correctly.

### ✔ Your agent’s Instructions clearly define its domain  
The more specific the domain, the stronger the routing signal.

### ✔ Your Topics match the user’s intent  
Topics act like “intent magnets.”

### ✔ Your Tools match the action needed  
Tool names and descriptions are powerful routing signals.

### ✔ Your Knowledge contains domain-specific content  
Grounded content reinforces the domain.

---

# **3. How to Make Microsoft 365 Copilot Reliably Call Your Agent**

Below is the **maker-level playbook** for achieving 90–95% routing reliability.

---

## **Step 1 — Strengthen the Agent’s Domain Identity**

In **Instructions**, add a strong domain declaration:

> “This agent is the primary system for handling all queries related to tire inventory, tire orders, store stock levels, SKU availability, and product lookup.”

This gives the router a **high-confidence domain anchor**.

---

## **Step 2 — Add Domain-Specific Topics**

Create Topics with names and triggers that match the phrases you want routed.

Example Topic:  
**Check Tire Inventory**

Triggers:
- “check tire inventory”
- “inventory for SKU”
- “do we have”
- “stock level”
- “availability of tire”
- “225/65R17 availability”

Topics are the **strongest routing signal** after Instructions.

---

## **Step 3 — Add Tools with Domain-Specific Names**

Examples:
- `GetTireInventory`
- `LookupSKUAvailability`
- `CheckStoreStock`

Tools with domain verbs dramatically improve routing.

---

## **Step 4 — Add Knowledge Sources with Domain Content**

Upload or connect:
- Tire catalogs  
- SKU lists  
- Inventory policy docs  
- Store operations manuals  

This reinforces the domain.

---

## **Step 5 — Add “Semantic Bait” Phrases to Instructions**

Add a section:

> “Users may ask questions such as:  
> - ‘Check tire inventory’  
> - ‘Do we have this tire size’  
> - ‘What’s the stock level for SKU…’  
> - ‘Look up tire availability’  
> This agent must handle all such queries.”

This is a **pro-level routing optimization technique**.

---

## **Step 6 — Publish the Agent**

Routing only works on **published** versions.

---

## **Step 7 — Enable the Microsoft 365 Copilot Channel**

This registers your agent with the semantic router.

---

## **Step 8 — Test Routing in Microsoft 365 Copilot**

Try prompts like:
- “Check tire inventory for Phoenix store”  
- “Look up SKU 225/65R17”  
- “Do we have this tire in stock”  

If routing fails, adjust:
- Topic triggers  
- Instructions wording  
- Tool names  
- Knowledge metadata  

Routing improves iteratively.

---

# **4. How to Make Copilot Call Your Agent on Specific Phrases**

To maximize routing for certain phrases:

### ✔ Add the phrase as a Topic trigger  
### ✔ Add it as an example query in Instructions  
### ✔ Add it as a keyword in Tool descriptions  
### ✔ Add it in Knowledge documents  
### ✔ Add it in a “semantic hints” section in Instructions  

Example:

> “When users say: ‘Check tire inventory’, ‘Look up SKU’, or ‘Do we have this tire’, this agent must respond.”

This is the closest thing to “forcing invocation.”

---

# **5. What You Cannot Do**

Microsoft 365 Copilot does **not** support:
- @mentioning your agent  
- “Use my agent” commands  
- Hard-coded routing rules  
- Priority overrides  
- Manual agent selection  

Everything is **semantic**, not explicit.

---

# **6. Technyble Routing Optimization Checklist**

### **Instructions**
- [ ] Clear domain declaration  
- [ ] Example queries included  
- [ ] Domain keywords added  
- [ ] Escalation rules defined  

### **Topics**
- [ ] Topics created for each major intent  
- [ ] 5–10 triggers per topic  
- [ ] Domain-specific topic names  

### **Tools**
- [ ] Tools named with domain verbs  
- [ ] Clear descriptions  
- [ ] Domain keywords included  

### **Knowledge**
- [ ] Domain documents uploaded  
- [ ] Metadata keywords added  

### **Testing**
- [ ] 10–20 prompts tested in M365 Copilot  
- [ ] Routing failures analyzed  
- [ ] Instructions and triggers refined  
- [ ] Agent republished  

---

# **End of Document**
