---
name: msx
description: "Use this skill any time the user wants to interact with MSX (Microsoft's internal CRM system, Dynamics 365). This includes: looking up accounts, searching for users or colleagues, finding opportunities, creating or listing tasks, checking your own identity (WhoAmI), or running raw OData queries against MSX. Trigger whenever the user mentions \"MSX,\" \"CRM,\" \"Dynamics,\" \"opportunities,\" \"deal team,\" \"accounts\" in a sales/CRM context, or wants to log a task or activity in the sales system. The skill operates through the `msx` CLI tool, which must be authenticated with a browser cookie before use."
compatibility: "Requires .NET 10+ runtime. The `msx` CLI must be installed as a global dotnet tool. Requires network access to microsoftsales.crm.dynamics.com."
---

# MSX CLI Skill

A CLI tool for interfacing with MSX (Microsoft's internal CRM / Dynamics 365). Every operation is a single `msx` command — no interactive mode.

The method that you will use to interface with MSX is via the `MSX.exe` CLI tool.

## Before you do anything
THIS IS VERY IMPORTANT!
1. Before you do anything, read the documentation of the MSX.exe tool using your `web_fetch` tool, found here: https://raw.githubusercontent.com/TimHanewich/MSX/refs/heads/master/readme.md
2. Run `msx` in the terminal to check if the user has the MSX CLI tool installed.
  - If they do NOT have it installed, let them know of this and offer to install it for them. If they say yes they want to install it (or are unreachable), install it for them by downloading the most recent version of `MSX.exe` found in the project readme you read above.
3. Run `msx version` to validate it is installed and check the version. If the version they have is not the most recent one specified in the readme, note this to the user. Ask them if they want you to download the most recent version. If the user is not reachable, just leave it, no need to download the latest version, proceed with the version you have.
  - If they DO want to download the latest version, run `where msx` to see where MSX is installed on the user's PC. Download the latest version and then be sure to completely replace the old MSX.exe with the new one. Then run `msx version` again to validate it installed correctly and you now have the latest one.
4. Proceed with the steps below, starting first with authentication!

## Authentication

The CLI authenticates via a browser cookie stored locally. **All API commands will fail if no cookie is saved.**

Before doing anything, check if a cookie is already set:

```bash
msx auth show
```

- If this prints a cookie value, authentication is ready.
- If it errors with `No cookie saved`, ask the user to provide their MSX cookie. They can grab it from their browser DevTools (Network tab → any request to `microsoftsales.crm.dynamics.com` → `cookie` request header).

Save the cookie:

```bash
msx auth set "<cookie_value>"
```

Other auth commands:

| Command | Description |
|---|---|
| `msx auth show` | Print the saved cookie |
| `msx auth path` | Print the file path where the cookie is stored |
| `msx auth clear` | Delete the saved cookie |

If an API command fails with an HTTP error (401/403), the cookie has likely expired. Ask the user for a fresh one.

## Commands

All API commands return **JSON output** to stdout. Errors go to stderr with exit code 1.

---

### Identity

```bash
msx whoami
```

Returns the current user's Dynamics 365 system user GUID as a plain string. Use this when you need the user's ID for other commands (e.g., `opps user`).

---

### Search Users

```bash
msx users "<name>"
```

Searches users by full name (partial, case-insensitive match). Returns a JSON array of user objects with fields: `fullname`, `title`, `internalemailaddress`, `msp_solutionarea`, `msp_rolesummary`, `msp_salesdistrictname`, `msp_solutionareadetails`, `msp_qualifier2`.

Example:

```bash
msx users "Jane Smith"
```

---

### Search Accounts

```bash
msx accounts "<search_term>"
```

Searches accounts by name (partial match). Returns a JSON array with `name` and `accountid` for each match.

Example:

```bash
msx accounts "Contoso"
```

Use the returned `accountid` with `msx opps search` to find opportunities under that account.

*TIP: U.S. State & Local Government accounts often follow a naming convention like `TX-State Government` or `NM-State Government` or `CA-COUNTY OF LOS ANGELES`. Start your search with terms like these.*

---

### Opportunities

Three subcommands for working with opportunities:

#### Search by Account

```bash
msx opps search "<account_id>" "<search_term>"
```

Finds open opportunities under a specific account by title (partial match). Returns `opportunityid`, `name`, `description`, `estimatedvalue`.

Typical workflow: first run `msx accounts` to get the account ID, then search its opportunities.

Example returned response:
```
[
  {
    "opportunityid": "b912f4aa-45c1-ee11-9f22-44d2a1c0f7b1",
    "name": "AURELION GOV | Dept. of Sky Transit | Cloud Workflow Suite",
    "description": "Modernizing aerial traffic request processing for the Sky Transit Authority",
    "estimatedvalue": 187500.0
  },
  {
    "opportunityid": "7f33c1d9-88b2-ee11-82c1-12f4b9e0a3c2",
    "name": "NOVA MUNICIPAL | Office of Arcology Services | DataHub Automation",
    "description": "Implementing automated data routing for vertical-city infrastructure",
    "estimatedvalue": 62400.0
  },
  {
    "opportunityid": "e2a4d0f1-19e3-ee11-9a11-55c2d4f8b9a7",
    "name": "KINGDOM OF VELORA | Ministry of Resource Harmony | Platform Revamp",
    "description": "Revamping digital systems for inter‑region resource allocation",
    "estimatedvalue": 402300.0
  },
  {
    "opportunityid": "c4f1a2e8-55d9-ee11-8c77-09f1e2a4c7d3",
    "name": "CITY OF LUMENFALL | Civic Innovation Bureau | Process Automation",
    "description": "Automating permit workflows for the Lumenfall Innovation District",
    "estimatedvalue": 11250.0
  }
]
```

#### My Opportunities

```bash
msx opps mine
```

Gets all open opportunities where the authenticated user is a deal team member. Returns `opportunityid`, `name`, `description`, `value`, `closeDate`, and the parent `account` (`id`, `name`).

#### User's Opportunities

```bash
msx opps user "<system_user_id>"
```

Same as `opps mine` but for any user. Get a user's system ID from `msx whoami` or `msx users`.

#### Example Response from `msx opps`
```
[
  {
    "opportunityid": "f91c2b77-aa12-ee11-9c44-55d2f8c1a9e3",
    "name": "AURELION JUSTICE AUTHORITY – Platform Modernization Initiative",
    "description": "Exploring a unified low‑code platform to streamline case workflows across the agency.",
    "value": 86450.0,
    "closeDate": "2026-08-27",
    "account": {
      "id": "1c7eab44-22d1-4f8b-9b11-8a0c4f77d9e1",
      "name": "AURELION FEDERAL SERVICES"
    },
    "forecastComments": [
      {
        "userId": "{A1B2C3D4-1111-2222-3333-444455556666}",
        "modifiedOn": "6/15/2023, 10:12:33 PM",
        "comment": "Initial discussions with AJA leadership about adopting a platform-wide low‑code solution. Team preparing early value assessment."
      },
      {
        "userId": "{A1B2C3D4-1111-2222-3333-444455556666}",
        "modifiedOn": "10/25/2023, 6:39:18 PM",
        "comment": "Left message with AJA tech lead to re-engage on modernization roadmap."
      },
      {
        "userId": "{DDEE1122-3344-5566-7788-99AABBCCDDEE}",
        "modifiedOn": "12/21/2023, 7:32:58 AM",
        "comment": "Funding tied to a separate modernization grant. Opportunity moved to Q1 for alignment."
      },
      {
        "userId": "{A1B2C3D4-1111-2222-3333-444455556666}",
        "modifiedOn": "8/23/2024, 5:21:36 PM",
        "comment": "Customer noncommittal on timing. Requested clarity on whether purchase aligns with next fiscal cycle."
      }
    ]
  },
  {
    "opportunityid": "c8e4a0b1-cc44-ee11-8f77-11aa22bb33cc",
    "name": "LUMENFALL CHILD SERVICES – Low‑Code Enablement Program",
    "description": "Agency exploring structured development environments and governance for 1,200 internal users.",
    "value": 189300.0,
    "closeDate": "2026-08-08",
    "account": {
      "id": "1c7eab44-22d1-4f8b-9b11-8a0c4f77d9e1",
      "name": "AURELION FEDERAL SERVICES"
    },
    "forecastComments": [
      {
        "userId": "{A1B2C3D4-1111-2222-3333-444455556666}",
        "modifiedOn": "7/27/2023, 10:29:15 AM",
        "comment": "Initial workshop held with LCS leadership. Strong interest in governance, ALM, and environment strategy."
      },
      {
        "userId": "{A1B2C3D4-1111-2222-3333-444455556666}",
        "modifiedOn": "12/11/2024, 2:51:29 AM",
        "comment": "Coordinating with internal engineering to schedule follow‑up enablement session."
      },
      {
        "userId": "{99887766-5544-3322-1100-AABBCCDDEEFF}",
        "modifiedOn": "3/11/2025, 3:08:13 PM",
        "comment": "Partner engagement deferred until agency direction becomes clearer."
      },
      {
        "userId": "{A1B2C3D4-1111-2222-3333-444455556666}",
        "modifiedOn": "6/16/2025, 12:35:08 PM",
        "comment": "No recent movement. Pushing opportunity out until customer re-engages."
      }
    ]
  }
]
```

### Tasks

#### List My Recent Tasks

```bash
msx tasks
```

Returns the user's most recent tasks (up to 150), ordered by scheduled start date descending. Each task includes `subject`, `description`, `scheduledstart`, and optionally a `regarding` object with the linked account or opportunity (`type`, `name`, `id`).

Example response:
```
[
  {
    "subject": "Aurelion Digital Forum – AI Agents Spotlight",
    "description": "Featured guest on the ADF’s tech broadcast with host Jalen Rho, presenting an overview of autonomous agent models.",
    "scheduledstart": "2025-10-21T15:00:00Z",
    "regarding": {
      "type": "account",
      "name": "AURELION CENTRAL ADMINISTRATION",
      "id": "9a22c1f3-55d1-4b8a-9c11-1f77a8c4e2b9"
    }
  },
  {
    "subject": "Nexora Platform Integration Discovery",
    "description": "Met with Nexora Systems to explore requirements for integrating Copilot‑style orchestration into their modular platform.",
    "scheduledstart": "2025-10-21T15:00:00Z",
    "regarding": {
      "type": "account",
      "name": "NEXORA SYSTEMS",
      "id": "c4b1d2e8-7f44-4d9a-8f22-0a9c55e1b7d3"
    }
  },
  {
    "subject": "Technical Architecture Review with SolaraGrid",
    "description": "Walked through solution architecture with the SolaraGrid engineering team, addressed technical questions, and aligned on next steps.",
    "scheduledstart": "2025-10-20T07:00:00Z",
    "regarding": {
      "type": "opportunity",
      "name": "AURELION | SOLARAGRID | AI | Intelligent Support & Protocol Navigator",
      "id": "b2d4e8f1-6a11-4c0d-9f77-2c1e5b9d7a44"
    }
  }
]
```

#### Create a Task

```bash
msx tasks create "<title>" "<description>" "<date>" [--category <category>] [--account <id>] [--opportunity <id>]
```

| Argument | Required | Description |
|---|---|---|
| `<title>` | Yes | Task subject |
| `<description>` | Yes | Task description |
| `<date>` | Yes | Scheduled start date, format: `yyyy-MM-dd` |
| `--category <category>` | No | Task category (see table below) |
| `--account <id>` | No | Link task to an account by GUID |
| `--opportunity <id>` | No | Link task to an opportunity by GUID |

Only one of `--account` or `--opportunity` can be used. If both are provided, account takes precedence.

#### Task Categories

| Value | Name |
|---|---|
| 606820000 | ACE |
| 606820001 | CrossSegment |
| 606820002 | CrossWorkload |
| 606820003 | PostSales |
| 606820004 | TechSupport |
| 606820005 | TechnicalCloseWinPlan |
| 861980000 | CustomerEngagement |
| 861980001 | Workshop |
| 861980002 | Demo |
| 861980003 | NegotiatePricing |
| 861980004 | ArchitectureDesignSession |
| 861980005 | PoCPilot |
| 861980006 | BlockerEscalation |
| 861980007 | ConsumptionPlan |
| 861980008 | Briefing |
| 861980009 | RFPRFI |
| 861980010 | CallBackRequested |
| 861980011 | NewPartnerRequest |
| 861980012 | Internal |
| 861980013 | ExternalCoCreationOfValue |

Examples:

```bash
# Standalone task (no category)
msx tasks create "Call customer" "Discuss Q3 renewal" 2026-04-01

# Task with a category
msx tasks create "Follow up call" "Discuss renewal timeline" 2026-04-01 --category CustomerEngagement

# Tied to an account with a category
msx tasks create "Prep for meeting" "Review history" 2026-04-01 --category CustomerEngagement --account "b1c2d3e4-5678-90ab-cdef-1234567890ab"

# Tied to an opportunity with a category
msx tasks create "Send proposal" "Draft SOW" 2026-04-05 --category Demo --opportunity "a9b8c7d6-5432-10fe-dcba-0987654321ab"
```

Prints `Task created.` on success.

---

### Raw OData Query

```bash
msx query "<odata_query>"
```

Runs any OData query against the Dynamics 365 API (`https://microsoftsales.crm.dynamics.com/api/data/v9.2/`). Only provide the path and query parameters — the base URL is added automatically.

Returns the `value` array from the API response as formatted JSON.

Example:

```bash
msx query "contacts?\$top=5&\$select=fullname,emailaddress1"
```

**Note:** Escape `$` characters in shells that interpret them (e.g., use `\$` in bash).

---

## Common Workflows

### Find a colleague's opportunities

```bash
msx users "Jane Smith"          # Get their systemuserid
msx opps user "<user_id>"       # List their open opportunities
```

### Log a task against an account

```bash
msx accounts "Contoso"          # Get the accountid
msx tasks create "Follow up" "Discuss renewal" 2026-04-01 --category CustomerEngagement --account "<account_id>"
```

### Explore an account's opportunities

```bash
msx accounts "Fabrikam"                          # Get accountid
msx opps search "<account_id>" "Azure"           # Search open opps
```

### Logging "HVAs"
A request you may receive is to log "High Value Activities", or "HVA's" for the user. This is a term some teams at Microsoft use to describe to their high-impact activities that they log in MSX as tasks. If a user inquires about their HVAs or asks to log an HVA, just know it is the task table they are referring to.

- When the user provides information to you about an HVA (task) for you to log, it is usually quite important that you tie it to an account or an opportunity.
- Do you best to determine what it should be tied to based on context clues. Perhaps they were discussing an opportunity or an account earlier in the conversation that it the HVA belongs to.
- If you can't immediately infer what the account or opportunity the task should be tied to, you can try to find it by searching through accounts and then searching through opportunities for accounts of interst you found. Use your best judgement in beginning your search. If you are quite lost and it isn't obvious where to begin searching, ask the user for clarification.
- You will work with all sorts of users. One of the users you are working with may be a Solution Engineer (a technical sales person). If so, they are working in close partnership with a Sales Executive. If they provide the name of the Sales Executive they work with, find the opportunities that Sales Executive has logged: first search users for them, then get a list of their opportunities, then try to find whichever opportunity in that list is right.

### Opportunity Updates
Another user you may work with is the manager of Sales Executives. This type of user cares most about getting high-level health checks of the opportunities that a particular Sales Executive on their team is working on. 

In this scenario, find the Sales Executive by searching through users, then pull a list of their opportunities. The Sales Executive Manager cares most about the recent forecast comments of the high-value opportunities in the Sales Executive pipeline. Be sure to provide the latest information and health assessment on each opportunity as this will be most important. In fact, infer the health of each opportunity as green, yellow, or red.
- Green = opportunity is progressing well. Forecast comments are recent and indicate positive progress towards deal close by predicted close date.
- Yellow = opportunity is stale or has shown challenging signs in forecast comments.
- Red = opportunity is progressing poorly. Forecast comments have not been added for some time or they are trending negatively.

## Error Handling
- Exit code `0` = success. Exit code `1` = error.
- All errors are written to stderr.
- HTTP errors from MSX include the status code and response body in the error message.
- If you see 401/403 errors, the cookie has expired — ask the user for a new one.
