---
name: compliance-check
description: Check code against Regulane's secure-coding rules, mapped to ISO 27001 and the DPDP Act, and get a scorecard. Use when the user asks for a compliance, security or privacy check of their app or a change, asks whether code is ISO 27001 or DPDP compliant, or is about to finish a change that touches authentication, access control, personal data, cryptography, logging, dependencies, CI or infrastructure.
---

# Regulane compliance check

Regulane gives you its secure-coding rules and turns what you find into a scorecard. You do the reading: Regulane never receives the code.

## Run a check

1. Decide the scope. Default to the uncommitted changes; if there are none, or the user asked about the whole app, check the files that handle requests, sign-in, data and configuration. Tell the user the scope in one line.
2. Call the `regulane` server's `get_compliance_rules` tool. Take every rule into account, not only the ones that look relevant from file names.
3. Read the code in scope and check it against each rule that could apply. Look at the code itself: a route without an auth check, a query built from a string, an email in a log line.
4. Call `report_compliance_check` with:
   - `repository`: the git remote URL, or the folder name when there is none
   - `branch` and `commit` if you know them
   - `agent`: which agent you are
   - `scope`: one line on what you examined
   - `rules_checked`: every rule id you checked, including those with no finding
   - `findings`: one entry per problem, with the rule id, the file path relative to the repository root, the line, and one sentence
5. Show the user the scorecard, most severe first, with the fix for each finding, and offer to make the fixes. After fixing, run the check again.

## Never send

- Source code, diffs or file contents. A finding is a path, a line and one sentence.
- Secrets. For a committed key, say "AWS access key hard-coded", never the key.
- Personal data, such as an email address or ID number found in a fixture.

## What the result means

The scorecard says the code you were given was checked against these rules. It is not a certification, an audit opinion or a penetration test; say so if the user treats a clean result as one.

Without a token, Regulane does not store the check. Teams that want each repository's history and findings kept as audit evidence connect a Regulane workspace with an agent token: https://regulane.com/coding-agents
