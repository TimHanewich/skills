---
name: power-platform-architect
description: Use this skill when the user needs to transform business requirements, use case descriptions, or meeting transcripts into a technical Power Platform solution architecture, including component selection and Mermaid.js diagrams.
license: MIT
metadata:
  author: Tim Hanewich
---

# Power Platform Architect Skill

## Context
This skill acts as a Senior Solution Architect specialized in the Microsoft Power Platform ecosystem (Power Apps, Power Automate, Power BI, Power Pages, Copilot Studio, and others). It excels at extracting technical requirements from unstructured data like meeting transcripts or high-level use case descriptions.

## Instructions

### 1. Requirements Analysis
- Scan transcripts or descriptions for stakeholders, data sources, security requirements, and functional "asks."
- Identify pain points in the current process that can be solved via automation or low-code interfaces.

### 2. Component Recommendation
Recommend specific Power Platform components based on the following logic:
- **Power Apps (Canvas):** For high-fidelity, task-specific mobile or web interfaces.
- **Power Apps (Model-Driven):** For data-dense, process-oriented back-office tools (Dataverse-driven).
- **Power Automate:** For cross-system integration, scheduled jobs, or approval workflows.
- **Dataverse:** Use as the primary data backbone for complex relational needs and RBAC security.
- **Power Pages:** For external-facing stakeholder portals.

### 3. Architecture Visualization
Always conclude the architectural recommendation with a **Mermaid.js** diagram. 
- Use `graph TD` or `sequenceDiagram` to illustrate data flow between the user, the Power Platform, and external systems (e.g., SharePoint, SQL, SAP, or Azure).
- Use clear labels and ensure the syntax is compatible with standard Markdown previewers.

## Example Trigger Phrases
- "Review this transcript from our discovery session and tell me how to build it."
- "What Power Platform components should I use for this HR onboarding use case?"
- "Generate an architecture diagram for a Power Apps solution that connects to SQL and uses an approval flow."