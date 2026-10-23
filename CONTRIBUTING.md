# Contributing to AI Website Deploy Skill

Thanks for helping developers deploy existing websites with fewer surprises.

## Report a deployment problem

Use the deployment report issue form. Include the framework, agent, failed stage,
expected behavior, actual result, and a small redacted log excerpt. For regional
access reports, include the test time and country/region or network category;
exact locations and IP addresses are unnecessary. Use a minimal reproduction
when the application source is private.

Never attach credentials, connection strings, user records, or private source.
If a report would expose private information, remove it before submission.

## Suggest an improvement

Useful contributions include reproducible fixes, current official platform links,
clearer installation steps, and deployment reports from other agent environments.
Please distinguish an observed deployment result from an untested suggestion.

For instruction changes, edit `SKILL.md` or its focused references. For public
installation or usage changes, keep the English and Chinese README consistent.
Preserve the existing-site scope, optional backend/database behavior, and honest
free-tier and regional-access limits.

## Check your change

1. Read the changed instructions as a first-time user. Check commands and links.
2. For installation changes, test in an unused project directory; avoid replacing
   personal skills. Record the CLI version and chosen agent.
3. For cloud deployment changes, use authorized accounts and test resources.
   Verify the affected public frontend/API path and describe untested boundaries.
4. Include evidence and limitations in the pull request. Do not trigger repeated
   installs, deploys, or writes just to create activity.

You can fork the repository and adapt the skill for your team under the MIT license.
Please preserve its copyright and license notice when redistributing it.
