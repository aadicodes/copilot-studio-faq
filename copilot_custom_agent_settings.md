# Each section in Custom Copilot configuration explained
## Tools
Think of Tools as the agent’s “hands.”
They let it perform real operations — calling APIs, running flows, updating systems.
Tools = action execution layer.
## Knowledge
Knowledge is the agent’s “library.”
It provides grounded, document‑based answers.
Knowledge = RAG grounding layer.
## Instructions
Instructions are the agent’s “constitution.”
They define tone, boundaries, safety, and persona.
Instructions = behavioral governance layer.
## Topics
Topics are the agent’s “conversation modules.”
They handle structured, multi‑turn interactions.
Topics = dialog orchestration layer.
## Triggers
Triggers are the agent’s “intent detectors.”
They determine when a topic should activate.
Triggers = conversation routing layer.
``` mermaid
flowchart TD
    %% Technyble Copilot Agent Architecture Diagram
    %% © 2026 Technyble LLC. All rights reserved.

    A[INSTRUCTIONS<br><br>• Persona & Tone<br>• Safety Rules<br>• Escalation Policies]:::instructions
    B[TRIGGERS<br><br>• Intents & Keywords<br>• Conditions]:::triggers
    C[TOPICS<br><br>• Dialog Flows<br>• User Journeys]:::topics
    D[KNOWLEDGE<br><br>• Documents & FAQs<br>• Internal Policies]:::knowledge
    E[TOOLS<br><br>• APIs & Actions<br>• System Integrations]:::tools

    %% Relationships
    A --> C
    B --> C
    C --> D
    C --> E
    D --> C
    E --> C

    %% Styling
    classDef instructions fill:#333333,stroke:#222222,color:#ffffff,font-weight:bold;
    classDef triggers fill:#0078D4,stroke:#005A9E,color:#ffffff,font-weight:bold;
    classDef topics fill:#0078D4,stroke:#005A9E,color:#ffffff,font-weight:bold;
    classDef knowledge fill:#444444,stroke:#222222,color:#ffffff,font-weight:bold;
    classDef tools fill:#444444,stroke:#222222,color:#ffffff,font-weight:bold;

    %% Title
    class A,B,C,D,E title;
```
