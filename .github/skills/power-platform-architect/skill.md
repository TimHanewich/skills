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

### Power Platform Component Catalog
The Power Platform provides a vast suite of tools that can be used in any digital solution. Below is a list of the various components (at least the main ones) that may be involved in your output architecture.
- **Power Apps:**- Custom business apps (Canvas or Model-Driven) for task-specific or data-centric interfaces.
- **Power Pages:**- Secure, low-code websites for external partners, customers, or internal portals.
- **Copilot Studio:**- AI-powered conversational agents for natural language interaction with users and data.

## Logic & Automation
- **Power Automate:**- Cloud flows for integration, scheduled tasks, and multi-stage approval workflows.
- **Dataverse Functions (Preview):**- Reusable Power Fx logic embedded in the data layer to ensure consistent business rules across all apps and flows.
- **AI Builder:**- Pre-built AI models (OCR, sentiment analysis, prediction) to add intelligence to processes.
- **Prompts:**- Custom generative AI instructions for standardized LLM-based interactions.

## Data & Storage
- **Dataverse:**- The primary secure, relational data platform for the Power Platform ecosystem.
- **Choices:**- Global option sets used to maintain data consistency across different tables and applications.
- **Dataflows:**- Self-service data preparation (Power Query) for importing and cleaning data from external sources.
- **Connections & Custom Connectors:**- Bridges to standard SaaS services or custom REST APIs.

## Enterprise Architecture & Management
- **Solutions:**- Portable containers used to manage the Application Lifecycle (ALM) across environments.
- **Gateways:**- Secure tunnels for connecting cloud services to on-premises data sources.
- **Azure Synapse Link:**- High-speed data export from Dataverse to Azure for big-data analytics.
- **Component Libraries:**- Centralized, reusable UI elements to ensure design consistency.
- **Catalog:**- A managed repository for discovering and deploying approved organizational assets.
- **Monitor:**- Real-time debugging and performance tracking for apps and integrations.
- **Wrap Projects:**- Tooling for packaging Power Apps as native mobile applications for app store distribution.

### "Cheat Sheet" Decision Logic for Architecting
For the "major needs" of a solution (e.g. user touch points), the following is a basic cheat sheet that guides you on what solution to recommend in various user scenarios.
1. **Public/External Access?**- -> Power Pages (portal website)
2. **Data Storage?**- -> Dataverse
3. **Internal Data Entry / Review / Process?**- -> Power Apps
4. **Legacy On-Prem Data?**- -> Data Gateways
5. **Multi-System Orchestration?**- -> Power Automate
6. **Conversational Interface? Agentic Automation?**- -> Copilot Studio

## Instructions

### 1. Requirements Analysis
- Scan transcripts or descriptions for stakeholders, data sources, security requirements, and functional "asks."
- Identify pain points in the current process that can be solved via automation or low-code interfaces.

### 2. Component Recommendation
Recommend specific Power Platform components based on the following logic:
- **Power Apps (Canvas):*- For high-fidelity, task-specific mobile or web interfaces.
- **Power Apps (Model-Driven):*- For data-dense, process-oriented back-office tools (Dataverse-driven).
- **Power Automate:*- For cross-system integration, scheduled jobs, or approval workflows.
- **Dataverse:*- Use as the primary data backbone for complex relational needs and RBAC security.
- **Power Pages:*- For external-facing stakeholder portals.

### 3. Architecture Visualization
Always conclude the architectural recommendation with a **Mermaid.js*- diagram. 
- Use `graph TD` or `sequenceDiagram` to illustrate data flow between the user, the Power Platform, and external systems (e.g., SharePoint, SQL, SAP, or Azure).
- Use clear labels and ensure the syntax is compatible with standard Markdown previewers.

## Example Trigger Phrases
- "Review this transcript from our discovery session and tell me how to build it."
- "What Power Platform components should I use for this HR onboarding use case?"
- "Generate an architecture diagram for a Power Apps solution that connects to SQL and uses an approval flow."