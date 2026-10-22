---
name: ai-website-deploy-skill
description: Deploy an existing website to Netlify with free-tier hosting, optional Render backend and user data storage, and end-to-end verification. Use for free website deployment, AI-built site publishing, frontend/backend integration, 网站部署, 免费网站上线, or 免费后端 requests. Preserve the existing design; do not add a database by default or guarantee worldwide availability.
---

# AI Website Deploy Skill

Take an existing project to a verified public website. Use Netlify for the frontend and, when an independent backend is needed, Render Free Web Service. Add persistent storage only when the application's retention requirements justify it. A static website needs no idle backend.

Execute the user's authorized deployment. Ask only for genuinely missing account, workspace, repository, access, or retention information. This skill does not authorize paid upgrades, irreversible data deletion, or broader application permissions.

## Scope and defaults

- Preserve the site's interface, content and business behavior. Change deployment configuration, routing, runtime compatibility and necessary integration code.
- When a new source repository is needed and visibility is unspecified, default to **Private**. Preserve existing repository visibility. Never make private source public to bypass deployment permissions. Website audience and source visibility are separate decisions.
- Do not add PostgreSQL, Redis or another data service merely because the app needs a backend. Preserve existing dependencies unless changing them is in scope; resolve conflicts with a free-only target before replacing them.
- Check current official free plans, usage limits, overage behavior and storage lifecycle at deployment time. Do not promise unlimited or permanently free hosting, domains or storage. Do not silently upgrade paid plans.
- Memory or JSON files can suit temporary tests when that lifecycle meets the user's requirements. Render Free local files can disappear after restarts, redeploys or spin-downs. Do not present them as durable user-data storage.

## 1. Identify the mode and audience

Choose among frontend-only, frontend + temporary backend, and frontend + backend + persistent user data. Infer from the existing code and request where possible. For accounts, comments, forms or uploads, establish required retention, access boundaries and recovery needs. Browser localStorage is not a substitute for a shared backend.

For mainland China/overseas audiences or data retention, read [Regional access and user data](references/access-and-data.md). Test pages, essential assets and APIs separately. Report unavailable regional test locations as unverified; one successful request does not establish worldwide accessibility. Do not promise that a default or custom domain resolves every regional access issue.

## 2. Discover the project and connections

Read applicable project instructions. Inspect entry points, framework, lockfiles, build command, publish directory, API paths, runtime, port, environment and Git state. Preserve unrelated local changes.

Discover the available GitHub, Netlify and Render tools. Prefer connected structured tools; use official CLIs or browser flows for missing capabilities. Inspect current schemas rather than assuming historical tool names. Read relevant installed platform skills when available and needed.

Confirm the intended deployment account and Render workspace; reuse suitable project/service IDs to avoid duplicate resources. Save non-sensitive progress in an ignored location such as `work/deployment/state.json`: repository, site/service IDs, source commit, deployment IDs and outstanding checks. Never save credentials there.

Read [Provider operations](references/providers.md) for private repository connections, publication and recovery.

## 3. Establish source access when Git deployment is needed

Render Git deployments require an accessible remote repository. Create/upload source in the user's hosting account when authorized and needed. Do not hardcode account names or resource IDs from past deployments.

A private GitHub deployment requires all three:

1. Render's GitHub App has repository access to the target repository.
2. The Render account has connected **Git Deployment Credentials**, separately from GitHub login methods.
3. The service uses credentials that can read the repository.

A working GitHub connector does not prove Render can clone source. After changing a repository from Public to Private, check the next build's clone stage. If access fails, guide the user to the exact missing connection rather than repeatedly redeploying unchanged credentials.

## 4. Configure only the needed components

For frontend-only tasks, skip Render, backend health endpoints and write-interface checks.

For independent backends:

- Bind to `0.0.0.0` and the platform's `PORT`; choose a supported runtime version.
- Provide a lightweight, read-only health endpoint such as `/api/health`. Reflect actual runtime/storage mode without disclosing secrets; check only genuinely required dependencies.
- Retain input validation, safe output rendering, reasonable payload limits and proportionate throttling for public write interfaces.
- Use commands appropriate to actual dependencies. A database-free app must not require an SQL client, `DATABASE_URL`, or an unrelated datastore.
- When authoring `render.yaml`, consult the current official specification and explicitly choose the available Free Web Service plan. Omitting a plan can select a paid default. Respect the configuration source of truth for Blueprint-managed resources.

For persistent data, choose and connect storage using [Regional access and user data](references/access-and-data.md). Do not substitute ephemeral files for required retention.

For the frontend:

- Prefer same-origin `/api/*` requests proxied by Netlify to the real Render HTTPS URL. Preserve existing API prefixes and routing order; avoid duplicated `/api/api` paths.
- When cross-origin requests are necessary, scope allowed origins to actual needs.
- Use the real static publish directory, or the framework's proper SSR adapter; do not force SSR apps into static hosting.
- Keep secrets out of browser code/build output. Ignore `.env`, `.netlify/`, dependencies and runtime data as appropriate.
- Handle cold starts with honest waiting, failure and recovery states. Do not display sample content as live user data or report failed writes as successful.

Remove deployment placeholders from the final configuration and keep local, repository and deployed settings consistent.

## 5. Deploy and recover

1. Run checks proportionate to the changes; count only observed successful checks as passed.
2. If a backend is needed, upload source and create/update the Render Free service. Follow the automatic deployment triggered by a push instead of triggering duplicates.
3. Track the intended commit's deployment to `live`; diagnose the first failed lifecycle stage from logs. Resource creation or accepted deploy triggers do not mean the new version is serving traffic.
4. Update any API proxy with the returned actual backend URL, publish the final frontend, and wait for Netlify `ready`.
5. Reconcile source and deployed configuration. Record any remaining difference as unfinished work.

After uncertain resource creation or network failure, read state before retrying to avoid duplicate sites, services or comments. Recover approval transport failures according to the tool's rules; if they persist, explain the blocked operation and request user action. Do not bypass approval through another channel.

When removing SQL dependencies, preserve necessary data first and verify the replacement before deleting anything. Removing a database from application code does not itself delete the old cloud resource. Handle permanent deletion separately under applicable confirmation rules.

## 6. Verify and deliver

Verify from the **public frontend URL**, not only directly against Render:

- Main page and required static assets load.
- If a backend exists, health returns its actual mode and required dependencies are ready.
- Existing read APIs return valid responses.
- Where appropriate and authorized, write one clearly identified test/welcome record and independently read it back. Check a second browser session when available to exclude browser-local fake success. Do not blindly resubmit requests of uncertain outcome.
- For private per-user data, test authorization boundaries rather than making real records public.
- Use browser QA when changes affect layout/interaction and the environment supports it. Report verification limits when it does not.

Deliver the website URL, actual deployment mode, completed checks and tested regions; include backend/repository links when useful. Distinguish deployed, integrated and unverified states. Explain cold starts and the selected storage's retention/expiry/usage boundaries briefly. Do not confuse a database trial expiry with a Web Service monthly allowance, or reuse old-version test results as proof of a new version.
