---
name: msx
description: "Use this skill any time the user wants to interact with MSX (Microsoft's internal CRM system, Dynamics 365). This includes: looking up accounts, searching for users or colleagues, finding opportunities, creating or listing tasks, checking your own identity (WhoAmI), or running raw OData queries against MSX. Trigger whenever the user mentions \"MSX,\" \"CRM,\" \"Dynamics,\" \"opportunities,\" \"deal team,\" \"accounts\" in a sales/CRM context, or wants to log a task or activity in the sales system. The skill operates through the `msx` CLI tool, which must be authenticated with a browser cookie before use."
compatibility: "Requires .NET 10+ runtime. The `msx` CLI must be installed as a global dotnet tool. Requires network access to microsoftsales.crm.dynamics.com."
---

# MSX CLI Skill

A CLI tool for interfacing with MSX (Microsoft's internal CRM / Dynamics 365). Every operation is a single `msx` command — no interactive mode.

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

---

### Opportunities

Three subcommands for working with opportunities:

#### Search by Account

```bash
msx opps search "<account_id>" "<search_term>"
```

Finds open opportunities under a specific account by title (partial match). Returns `opportunityid`, `name`, `description`, `estimatedvalue`.

Typical workflow: first run `msx accounts` to get the account ID, then search its opportunities.

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

---

### Tasks

#### List My Recent Tasks

```bash
msx tasks
```

Returns the user's most recent tasks (up to 150), ordered by scheduled start date descending. Each task includes `subject`, `description`, `scheduledstart`, and optionally a `regarding` object with the linked account or opportunity (`type`, `name`, `id`).

#### Create a Task

```bash
msx tasks create "<title>" "<description>" "<date>" [--account <id>] [--opportunity <id>]
```

| Argument | Required | Description |
|---|---|---|
| `<title>` | Yes | Task subject |
| `<description>` | Yes | Task description |
| `<date>` | Yes | Scheduled start date, format: `yyyy-MM-dd` |
| `--account <id>` | No | Link task to an account by GUID |
| `--opportunity <id>` | No | Link task to an opportunity by GUID |

Only one of `--account` or `--opportunity` can be used. If both are provided, account takes precedence.

Examples:

```bash
# Standalone task
msx tasks create "Call customer" "Discuss Q3 renewal" 2026-04-01

# Tied to an account
msx tasks create "Prep for meeting" "Review history" 2026-04-01 --account "b1c2d3e4-5678-90ab-cdef-1234567890ab"

# Tied to an opportunity
msx tasks create "Send proposal" "Draft SOW" 2026-04-05 --opportunity "a9b8c7d6-5432-10fe-dcba-0987654321ab"
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
msx tasks create "Follow up" "Discuss renewal" 2026-04-01 --account "<account_id>"
```

### Explore an account's opportunities

```bash
msx accounts "Fabrikam"                          # Get accountid
msx opps search "<account_id>" "Azure"           # Search open opps
```

## Error Handling

- Exit code `0` = success. Exit code `1` = error.
- All errors are written to stderr.
- HTTP errors from MSX include the status code and response body in the error message.
- If you see 401/403 errors, the cookie has expired — ask the user for a new one.
