# Power Platform Architect Agent Skill
A **GitHub Copilot agent skill** that acts as a Senior Solution Architect for the Microsoft Power Platform. Give it business requirements, use case descriptions, or even raw meeting transcripts, and it produces a tailored technical architecture, complete with component recommendations and an optional Mermaid.js diagram.

## What It Does

| Input | Output |
|---|---|
| Business requirements, use case descriptions, discovery-session transcripts | Component recommendations, a narrative architecture walkthrough, and an optional Mermaid.js architecture diagram |

The skill covers the full Power Platform ecosystem: **Power Apps** (Canvas, Model-Driven, Code Apps), **Power Pages**, **Copilot Studio**, **Power Automate** (Cloud & Desktop Flows), **AI Builder**, **Dataverse**, **Power BI**, **Connectors**, and **Gateways**.

## How It Works

The skill guides the agent through a structured, multi-phase process (though the output is presented seamlessly to the user):

1. **Requirements Analysis** — Scans the provided material for stakeholders, data sources, security needs, and functional asks. Documents the current ("As-Is") process and identifies friction points.

2. **Follow-Up Questions** — The agent asks clarifying questions to fill gaps (e.g., "Is this for mobile field workers or desktop back-office users?", "What triggers this process?"). If the user can't answer, it makes reasonable assumptions.

3. **Component Recommendation** — Selects only the Power Platform components that serve a real purpose in the solution and explains the role each one plays. It follows a built-in decision framework (e.g., external access → Power Pages, data storage → Dataverse, conversational interface → Copilot Studio).

4. **Architecture Narrative** — Delivers a business-process-oriented architecture recommendation that tells the "story" of how data flows through the system, which components handle each step, and which user audiences interact at each point.

5. **Architecture Diagram (Optional)** — On request, generates a Mermaid.js diagram visualizing the architecture, saves it to a `.md` file, and directs the user to [mermaid.ai/live/edit](https://mermaid.ai/live/edit) to render it.

## Example Prompts

- *"Review this transcript from our discovery session and tell me how to build it."*
- *"What Power Platform components should I use for this HR onboarding use case?"*
- *"Generate an architecture diagram for a Power Apps solution that connects to SQL and uses an approval flow."*

## License

MIT — see `skill.md` for details.
