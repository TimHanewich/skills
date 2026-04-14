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
- **Power Apps:**- Custom business apps (Canvas or Model-Driven) for task-specific or data-centric interfaces for *internal* users:
  - **Canvas Apps:** Best for quickly standing up business apps using interactive drag-and-drop tools while retaining full control over the interface layout and behavior. Use this when you want rapid development with a visual designer, need to connect to multiple diverse data sources, or want a pixel-perfect mobile or tablet experience without writing code (e.g., a frontline worker mobile app or a field inspection form).
  - **Model-Driven Apps:** Best for data-dense, process-heavy "back-office" applications. These are automatically generated from your Dataverse schema. Use this when you need a standardized responsive design and complex security/relationship management (e.g., a CRM or Asset Management system).
    - **Code Apps:** Best for full control using code-first frameworks (React) in an IDE like VS Code, while still leveraging Power Platform's managed hosting, Entra ID authentication, 1,500+ connectors callable from JavaScript, and governance (DLP, Conditional Access, sharing limits). Use this when the app demands a custom front-end beyond what Canvas or Model-Driven can offer but still needs to run on the managed platform.
- **Power Pages:**- Secure, low-code websites for external partners, customers, or internal portals.
- **Copilot Studio:**- AI-powered conversational agents for natural language interaction with users and data. Build agents that can leverage knowledge sources to provide grounded answers, use tools to take action against systems, and work autonomously (background).
- **Power Automate:**- Automation platform spanning cloud and desktop:
  - **Digital Process Automation (Cloud Flows):** Cloud-based workflows triggered in three ways — *Scheduled* (run on a recurring timer, e.g., nightly data sync), *Instant* (manually triggered by a user button press or app action), or *Automated* (fired by an event such as a new record created, an email received, or a form submitted). Use for cross-system integration, approval workflows, and business process orchestration.
  - **Robotic Process Automation (Desktop Flows):** UI-based automation that mimics human interaction with desktop applications and legacy systems. Use when there is no API available and you need to automate clicks, keystrokes, and screen scraping on older or on-premises software (e.g., mainframe terminals, legacy ERP clients).
- **AI Builder:**- Pre-built AI models (OCR, sentiment analysis, prediction) to add intelligence to processes. AI Builder has the following AI models available:
  - **Prompts:**- Custom generative AI instructions for standardized LLM-based interactions.
  - **Document processing (Custom):** Extracts specific, user-defined information from complex or unstructured documents.
  - **Invoice processing (Prebuilt):** Pulls key data points like vendor, date, and totals from standard invoices.
  - **Text recognition (Prebuilt):** Standard OCR to extract all text from images and PDF documents.
  - **Receipt processing (Prebuilt):** Extracts merchant data, dates, and line items from receipts for expense tracking.
  - **Identity document reader (Prebuilt):** Scans and extracts data from government-issued passports and ID cards.
  - **Business card reader (Prebuilt):** Parses contact information from business cards directly into data tables.
  - **Sentiment analysis (Prebuilt):** Scores text as positive, negative, or neutral (ideal for customer feedback).
  - **Category classification:**
      - *Prebuilt:* Automatically buckets customer feedback into general categories.
      - *Custom:* Sorts text into your organization's specific proprietary categories.
  - **Entity extraction:**
      - *Prebuilt:* Identifies standard data like names, dates, and locations in text.
      - *Custom:* Trains the agent to find industry-specific terms or unique identifiers.
  - **Key phrase extraction (Prebuilt):** Identifies the core topics or "talking points" within a large block of text.
  - **Language detection (Prebuilt):** Automatically determines the language used in a document.
  - **Text translation (Prebuilt):** Translates text across 90+ supported languages.
  - **Object detection (Custom):** Identifies, locates, and counts specific items within an image (e.g., inventory tracking).
  - **Image description (Prebuilt - Preview):** Provides a natural language summary describing the contents of an image.
  - **Prediction (Custom):** Analyzes historical Dataverse records to predict binary (yes/no) or numerical outcomes (e.g., credit risk or project delays).
  
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