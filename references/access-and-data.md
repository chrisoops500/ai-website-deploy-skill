# Regional access and optional user data

Read when the task involves mainland China/overseas audiences or user-data retention.

## Mainland China and overseas visitors

A public HTTPS address, an overseas access result, and a successful request on a particular mainland China network are different observations. Do not combine them into an assertion of worldwide reliability.

1. Identify audience regions, relevant networks and existing domain configuration. Preserve working entrypoints. Custom domains are optional; registration/renewal may cost money, so do not purchase one automatically.
2. Bundle distributable fonts, icons, scripts, styles and images when appropriate. Avoid essential page functions depending on untested third-party domains. Respect asset licenses.
3. A same-origin `/api` rewrite reduces browser connections to separate backend domains. It does not guarantee regional reachability or eliminate backend cold starts.
4. Use genuine target-region test locations for DNS, TLS, the main page, critical assets, API calls and interaction. If none is available, provide user-test steps and label the location unverified. Do not change network settings, circumvent access restrictions or fabricate results.
5. Record the test time, actual hostname, region/network, page/API results and untested scope. Do not collect or publish unrelated visitor IPs or other personal data.

Example reporting format, not evidence of any actual test:

| Entrypoint | Region/network | Page | API | Conclusion |
| --- | --- | --- | --- | --- |
| Actual hostname | Current execution network; location unverified | Pass | Pass | Flow verified only from this network |
| Actual hostname | Mainland China | Not tested | Not tested | Awaiting a regional test |
| Actual hostname | Overseas | Not tested | Not tested | Awaiting a regional test |

For frontend-only sites, mark API checks not applicable.

## Choose storage from retention requirements

| Need | Starting point | Boundary |
| --- | --- | --- |
| Static content | No backend or datastore | Keep browser-only tasks simple |
| Computation, transformations, temporary shared state | Render backend; optional memory/JSON | Ephemeral state can disappear |
| Comments/forms retained across sessions | Existing durable storage or an appropriate approved free-tier service | Verify expiry, capacity, write access and overages |
| Attachments/generated files | Optional object storage | Validate size/type, permissions and retention |
| Accounts/private user records | Existing identity system plus durable storage | Authenticate, isolate users and define recovery behavior |

SQL is not mandatory. Compare existing services, object/document storage or managed databases according to actual needs. Before selecting a provider, read its current official documentation, free-tier terms and regional availability. This reference is not proof of a provider's prices or reachability.

Prefer sufficient connected tools. Request only necessary account connections. Connection strings and management credentials remain server-side; public browser code must not contain administrator keys. Do not write user records back to a public source repository. This skill's public repository contains only general instructions and example configuration.

### Persistence acceptance

- Create a non-personal test record and read it from a separate session.
- For private per-user records, check that an unauthorized session cannot read or modify another user's data.
- Where authorized and operationally acceptable, verify data survives the relevant deploy/process lifecycle. Explain any untested boundary.
- Check datastore expiry, spin-down, backups, quotas and deletion behavior. Required long-term retention needs a real storage solution; Render Free local files and expiring database trials must not be described as permanent storage.
