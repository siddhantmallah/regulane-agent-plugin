# Regulane compliance check

When the user asks for a compliance, security or privacy check, or asks whether code is ISO 27001 or DPDP compliant, follow `skills/compliance-check/SKILL.md` in this extension: call the `regulane` server's `get_compliance_rules`, check the code in scope against the rules, then call `report_compliance_check` and show the user the scorecard with each fix.

Never send source code, secrets or personal data to Regulane. A finding is a repository-relative file path, a line number and one sentence.
