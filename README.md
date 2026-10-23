<div align="center">

<img src="assets/hero.svg" alt="AI website deployment skill — free frontend hosting and optional backend" width="100%" />

# AI Website Deploy Skill

### Free website deployment. Optional backend hosting. Real end-to-end checks.

**Deploy an existing website with your AI coding agent: Netlify frontend hosting, an optional Render backend, and verified frontend-to-API integration.**

[![Agent Skill](https://img.shields.io/badge/Agent-Skill-3ee0b5?style=flat-square&labelColor=10232c)](SKILL.md)
[![Netlify](https://img.shields.io/badge/Netlify-Frontend-00c7b7?style=flat-square&labelColor=10232c)](https://www.netlify.com/)
[![Render](https://img.shields.io/badge/Render-Optional_Backend-a78bfa?style=flat-square&labelColor=10232c)](https://render.com/)
[![Data](https://img.shields.io/badge/User_Data-On_Demand-80a8ff?style=flat-square&labelColor=10232c)](references/access-and-data.md)

[Install](#-quick-start) · [How it works](#-how-it-works) · [User data](#-optional-backends-and-user-data) · [Regional access](#-mainland-china-and-overseas-access) · [FAQ](#frequently-asked-questions) · [中文指南](README.zh-CN.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-3ee0b5?style=flat-square&labelColor=10232c)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/chrisoops500/ai-website-deploy-skill?style=flat-square&label=Star)](https://github.com/chrisoops500/ai-website-deploy-skill/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/chrisoops500/ai-website-deploy-skill?style=flat-square&label=Fork)](https://github.com/chrisoops500/ai-website-deploy-skill/fork)

```bash
npx skills add chrisoops500/ai-website-deploy-skill
```

Install → choose your agent → open your website project → ask it to deploy.

</div>

---

## ✦ Your website is built. Now make it reachable.

Building a site with an AI coding agent is only part of the journey. You still need to choose the publish directory, connect a private repository, configure an API, protect credentials, and verify that the public website actually works.

**AI Website Deploy Skill turns that deployment workflow into reusable agent instructions.** It starts with your existing project, preserves its design, prefers available free hosting plans, and adds infrastructure only when your application needs it.

> This is a **skill**, not a website builder, starter template, hosting provider, or unlimited free cloud service. Bring an existing website and your own platform accounts. The agent uses the connectors, official CLIs, or browser capabilities available in its environment.

<table>
<tr>
<td width="33%"><h3>↗ Deploy your frontend</h3><p>Identify the existing framework, build command, and publish directory. Deploy to Netlify without redesigning your site.</p></td>
<td width="33%"><h3>⌘ Add a backend if needed</h3><p>Connect a Render Free Web Service for APIs, computation, or shared state. A static website stays frontend-only.</p></td>
<td width="33%"><h3>✓ Verify the real flow</h3><p>Test the public website, assets, and API together. For write features, create a test record and read it back independently.</p></td>
</tr>
</table>

## ⚡ Quick start

### 1. Install the skill

Run the [Skills CLI](https://github.com/vercel-labs/skills) in your project and choose your coding agent:

```bash
npx skills add chrisoops500/ai-website-deploy-skill
```

Requires Git and a Node.js version supported by the current Skills CLI. To target one agent explicitly:

```bash
# Codex: install into this project
npx skills add chrisoops500/ai-website-deploy-skill --agent codex

# Claude Code: install into this project
npx skills add chrisoops500/ai-website-deploy-skill --agent claude-code

# Cursor: install into this project
npx skills add chrisoops500/ai-website-deploy-skill --agent cursor
```

The CLI supports these installation targets; cloud connectors, approvals, and execution capabilities depend on your agent environment. The original deployment workflow was exercised in Codex. Other agents' deployment flows have not been independently verified here.

<details>
<summary><b>Install through Codex or manually instead</b></summary>

Ask Codex:

```text
Install the agent skill from:
https://github.com/chrisoops500/ai-website-deploy-skill
```

Or clone into an unused local Codex skills directory:

```bash
git clone https://github.com/chrisoops500/ai-website-deploy-skill.git \
  ~/.codex/skills/ai-website-deploy-skill
```

Compare an existing installation before replacing it. Start a new conversation after installation. Other agents may use different skill directories.

</details>

### 2. Open your existing website project

| Deployment mode | What you need |
| --- | --- |
| Frontend only | Website source and a Netlify account |
| Frontend + backend | The above, plus a Render account and accessible Git repository |
| Frontend + persistent user data | The above, plus retention requirements and an appropriate storage connection |

### 3. Ask your agent to deploy it

```text
Use $ai-website-deploy-skill to deploy this existing website.
Prefer free hosting plans. Preserve the design and keep the source repository private.
Add a Render backend only if the application needs one.
If user data must persist, choose storage based on its retention requirements.
Check the public website, assets, and API, and report which regions were tested.
```

<details>
<summary><b>More deployment prompts</b></summary>

**Publish a portfolio or static website**

```text
Use $ai-website-deploy-skill to publish this portfolio on Netlify.
No backend or database is needed. Keep the existing design and check asset loading.
```

**Deploy an API with a free backend hosting plan**

```text
Use $ai-website-deploy-skill for this frontend and API project.
Host the frontend on Netlify and the API on Render's available Free Web Service plan.
Connect them through a same-origin /api proxy. Temporary test data is sufficient.
```

**Save comments, forms, or account data**

```text
Use $ai-website-deploy-skill to deploy this app.
User data must survive browser sessions and redeploys. Compare suitable free-tier
storage options and their limits first. Do not use temporary disk or localStorage
as a substitute for persistent shared user data.
```

</details>

## Website deployment use cases

| What you want to publish | How this skill helps |
| --- | --- |
| A portfolio, landing page, or HTML/CSS/JavaScript website | Free-tier frontend deployment on Netlify; no backend required |
| A React, Vue, or Vite website | Detect the existing build and publish settings, then verify routes and assets |
| An app with SSR or server routes | Inspect the framework adapter and runtime instead of assuming a static export |
| A website with a Node.js API | Optional Render backend deployment, health checks, and frontend API routing |
| An AI-built website that only runs on localhost | Turn the existing source into a public URL and check the real user flow |
| Comments, forms, or other shared user data | Establish retention needs and connect suitable storage only when needed |

### From the original deployment: ECHO

This skill grew out of deploying an anonymous comment app with a Netlify frontend and a Render API. The original session verified a write and an independent read through the deployed frontend. The source repository stayed private; no SQL database was required for that temporary-data test.

That deployment exposed the details now covered by the skill: private-repository deployment credentials, same-origin API rewrites, cold starts, and the difference between temporary JSON files and durable user data. It is a workflow example, not a claim of continuous uptime or permanent free storage.

## ◇ How it works

```mermaid
flowchart LR
    A[Existing website] --> B[Identify deployment mode]
    B --> C[Netlify frontend]
    B -. API needed .-> D[Render Free Web Service]
    C --> E[Public website URL]
    E -. Same-origin /api proxy .-> D
    D -. Retention required .-> F[Appropriate persistent storage]
    E --> G[Verify page, assets and business flows]
    G --> H[Report regional testing scope]
```

| Stage | What the agent checks |
| --- | --- |
| **Discover** | Existing framework, lockfile, commands, environment, Git state, and reusable cloud resources |
| **Connect** | Correct accounts and workspace, private repository access, and deployment credentials |
| **Configure** | Actual publish directory, port binding, health endpoint, and necessary API proxy |
| **Deploy** | The intended commit reaches Netlify `ready` or Render `live` |
| **Verify** | Public website → backend flow; real write/read checks when appropriate |
| **Deliver** | Working links, completed checks, untested regions, and free-tier/storage boundaries |

## ⌘ Optional backends and user data

**A backend is not automatically a database. A database is not automatically permanent storage.** The deployment mode follows your app's needs.

| Mode | Suitable for | Data behavior |
| --- | --- | --- |
| **Frontend only** | Portfolios, landing pages, browser-only tools | No backend or storage is created |
| **Frontend + API** | Computation, integration tests, temporary shared state | Memory or JSON files may be sufficient, with explicit data-loss limits |
| **Frontend + API + Data** | Comments, forms, accounts, uploaded files | Use existing or appropriate persistent storage based on retention needs |

SQL is optional. The skill does not add PostgreSQL just because an app needs an API. When records must survive restarts and redeploys, it checks the storage provider's current quotas, expiry, access controls, and recovery behavior.

Render Free local files can be lost after restarts, redeploys, or spin-downs. Web Service monthly allowances and free PostgreSQL expiry are separate rules. See [Render's current free service documentation](https://render.com/docs/free).

> Personal user data does not belong in a public source repository. Administrative credentials stay on the server; private user records need authentication and authorization checks.

## 🌏 Mainland China and overseas access

This workflow can target visitors in mainland China and overseas. **Availability must be tested from the actual target networks.** A public HTTPS URL or global CDN is not proof of reliable access from every region and ISP.

The skill guides the agent to:

- Bundle distributable essential assets when appropriate, reducing critical third-party font, script, and image dependencies.
- Check the page, assets, API, and interactions separately.
- Test from real regional networks when available; clearly label regions that were not tested.
- Configure an existing custom domain when requested, without treating a domain change as a universal availability fix.

This repository does **not** claim Netlify's default domains are always reachable from mainland China. It also does not present one successful local check as a worldwide test. See the [regional access and data guide](references/access-and-data.md).

## ◌ What “free” means

**Choose currently available $0/month plans, within their published limits.** This does not mean unlimited traffic, always-on compute, permanent data retention, or free domain registration.

| Service | Typical role | What must be checked |
| --- | --- | --- |
| Netlify | Frontend hosting and necessary API rewrites | Account plan, credits/quotas, builds, and overage behavior |
| Render | Optional Free Web Service | Free-plan availability, shared usage, cold starts, and temporary storage |
| Optional storage | Data retention suited to the app | Capacity, expiry, read/write quotas, backups, and overages |

The skill asks the agent to consult official documentation at deployment time. It does not authorize paid upgrades when a quota is exhausted.

[Netlify billing documentation](https://docs.netlify.com/manage/accounts-and-billing/) · [Render free services](https://render.com/docs/free) · [Provider reference](references/providers.md)

## ↳ Private repositories: the easily missed step

Installing Render's GitHub App is only part of the setup:

```text
GitHub App can access the target repository
                     +
Render has connected Git Deployment Credentials
                     +
The service uses the correct Git Credentials
                     =
Private source can be cloned and built
```

**GitHub login methods and Git deployment credentials are different settings.** After making a repository private, verify the next build can still clone it. The workflow covers this failure path alongside proxy configuration, cold starts, and deployment status checks.

## ▤ Repository structure

```text
.
├── SKILL.md                       Agent execution instructions
├── agents/openai.yaml             Skill display metadata and invocation prompt
├── references/
│   ├── providers.md               Platform setup, credentials and recovery
│   └── access-and-data.md         Regional access and retention decisions
├── assets/                        Project artwork and icon
├── CONTRIBUTING.md                Contribution and testing guide
├── LICENSE                        MIT license
├── docs/share.md                  Shareable project descriptions
├── README.md                      English project overview
└── README.zh-CN.md                 Chinese guide
```

## ✧ Already used an AI website builder?

Use your coding tool to build and test the site locally, then use this skill for **automated website deployment**. Its focus is the step from existing source to a verified public website, with **free frontend hosting** and **optional free backend hosting** where current plans fit the workload.

It does not replace an AI website builder or guarantee production-grade hosting at zero cost.

## Frequently asked questions

### How do I deploy a website for free with an AI agent?

Install the skill, open your existing website project, and use the deployment prompt above. The agent inspects the project and available accounts, selects a suitable free-tier deployment mode, and checks the resulting public URL. You still need your own hosting accounts and any required approvals.

### Can I host a backend for free without SQL?

Yes, when Render's currently available Free Web Service plan fits the workload. An API for computation or temporary shared state does not inherently need a database. Records that must survive redeploys need appropriate durable storage.

### Does this build a website or deploy an existing website?

It deploys an existing website. Use your coding agent to build the application first; use this skill to configure hosting, connect the frontend and backend, and verify deployment.

### Is this a Netlify or Render MCP server?

No. This repository provides `SKILL.md` instructions and references. The agent uses whichever authorized platform connectors, official CLIs, or browser tools are available. Installing the skill does not sign you into a hosting account or grant access to a private repository.

### Will this work for visitors in mainland China and overseas?

The skill includes regional access checks. Actual availability depends on the domain, hosting, network, and external assets. Ask for tests on the target networks; untested regions must remain labeled as unverified.

### How do I update or adapt the skill?

Use the Skills CLI's update command for a CLI-managed installation. To change the instructions for your team, [fork this repository](https://github.com/chrisoops500/ai-website-deploy-skill/fork), edit the skill and references, and install from your own fork. Keep the MIT copyright and license notice when redistributing it.

## ✧ Feedback and contributions

**Did it help you ship? [Star the repository](https://github.com/chrisoops500/ai-website-deploy-skill/stargazers) to save it and help other developers discover it.** [Fork it](https://github.com/chrisoops500/ai-website-deploy-skill/fork) to adapt the workflow for your team.

See [CONTRIBUTING.md](CONTRIBUTING.md) for deployment reports and pull requests. Small, reproducible improvements are welcome. [Shareable English and Chinese descriptions](docs/share.md) are available for linking to the project.

[Open an issue](https://github.com/chrisoops500/ai-website-deploy-skill/issues) or submit a pull request with reproducible deployment failures, documentation changes, or regional testing reports.

Include the framework, failed stage, and redacted logs. For access reports, include the network region and test time. **Never upload tokens, connection strings, personal user data, or logs without permission.**

## License

[MIT](LICENSE) © 2026 Chris Zhao.

---

<div align="center">

**From a local project to a verified public website.**

Free-tier first. Infrastructure only when needed. Limits made visible.

[Get started ↑](#-quick-start)

</div>
