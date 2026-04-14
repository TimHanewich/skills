---
name: msx
description: "Use this skill any time the user wants to interact with MSX (Microsoft's internal CRM system, Dynamics 365). This includes: looking up accounts, searching for users or colleagues, finding opportunities, creating or listing tasks, checking your own identity (WhoAmI), or running raw OData queries against MSX. Trigger whenever the user mentions \"MSX,\" \"CRM,\" \"Dynamics,\" \"opportunities,\" \"deal team,\" \"accounts\" in a sales/CRM context, or wants to log a task or activity in the sales system. The skill operates through the `msx` CLI tool, which must be authenticated with a browser cookie before use."
compatibility: "Requires .NET 10+ runtime. The `msx` CLI must be installed as a global dotnet tool. Requires network access to microsoftsales.crm.dynamics.com."
---

# MSX CLI Skill

A CLI tool for interfacing with MSX (Microsoft's internal CRM / Dynamics 365). Every operation is a single `msx` command — no interactive mode.

The method that you will use to interface with MSX is via the `MSX.exe` CLI tool.

## STEP 1: READ MSX CLI DOCUMENTATION
**THIS IS VERY IMPORTANT!**

Before you do anything, read the documentation of the MSX.exe tool using your `web_fetch` tool, found here: https://raw.githubusercontent.com/TimHanewich/MSX/refs/heads/master/readme.md

## Step 2: Validate MSX CLI is Installed
Run `msx` in the terminal to check if the user has the MSX CLI tool installed.

### Install if Needed
If they do NOT have it installed, let them know of this and offer to install it for them. If they say yes they want to install it (or are unreachable), install it for them by downloading the most recent version of `MSX.exe` found in the project readme you read above. Follow the suggested steps in the readme.md of the MSX CLI project you read to place it in the `%LocalAppData%\MSX` folder and update the PATH variable with that directory so `msx` is callable from anywhere.

## Step 3: Validate MSX CLI Version
Run `msx version` to validate it is installed and check the version. If the version they have is not the most recent one specified in the readme, note this to the user. Ask them if they want you to download the most recent version. If the user is not reachable, just leave it, no need to download the latest version, proceed with the version you have.

If they DO want to download the latest version, run `where msx` to see where MSX is installed on the user's PC. Download the latest version and then be sure to completely replace the old MSX.exe with the new one. Then run `msx version` again to validate it installed correctly and you now have the latest one.

## Step 4: Validate Authentication
The CLI authenticates via a browser cookie stored locally. **All API commands will fail if no cookie is saved.**

Now check if a cookie is already set:

```bash
msx auth check
```

This will confirm if they have already set a cookie.

- If it errors with `No cookie saved`, ask the user to provide their MSX cookie. They can grab it from their browser DevTools (Network tab → any request to `microsoftsales.crm.dynamics.com` → `cookie` request header).

Save the cookie:

```bash
msx auth set "<cookie_value>"
```

## Step 5: Use the MSX CLI to interface with MSX!
You have read the most up-to-date readme for the MSX CLI tool, so you should know how to use the commands in the CLI tool and the expected outputs. Use them accordingly to achieve the user's desired goals or answer questions, even if that means chaining many together.

## Guidance
Below is some guidance on best practices in using the MSX CLI tool and common workflows.

### Raw OData Query
If you don't feel any of the existing MSX CLI functions are adequate to satisfy a particular request, a powerful alternative to turn to is the `query` command. This allows you to runs any **OData query** against the Dynamics 365 API (`https://microsoftsales.crm.dynamics.com/api/data/v9.2/`). Only provide the path and query parameters, the base URL is added automatically.

```bash
msx query "<odata_query>"
```

It will return the `value` array from the API response as formatted JSON.

Example:

```bash
msx query "contacts?\$top=5&\$select=fullname,emailaddress1"
```

**Note:** Escape `$` characters in shells that interpret them (e.g., use `\$` in bash).

### Common Workflow: Find a colleague's opportunities
```bash
msx users "Jane Smith"          # Get their systemuserid
msx opps user "<user_id>"       # List their open opportunities
```

### Common Workflow: Log a task against an account
```bash
msx accounts "Contoso"          # Get the accountid
msx tasks create "Follow up" "Discuss renewal" 2026-04-01 --category CustomerEngagement --account "<account_id>"
```

### Common Workflow: Explore an account's opportunities
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

### Error Handling
- Exit code `0` = success. Exit code `1` = error.
- All errors are written to stderr.
- HTTP errors from MSX include the status code and response body in the error message.
- If you see 401/403 errors, the cookie has expired — ask the user for a new one.

### Other Tips
U.S. State & Local Government accounts often follow a naming convention like `TX-State Government` or `NM-State Government` or `CA-COUNTY OF LOS ANGELES`. Start your search with terms like these.