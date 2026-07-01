# service-bootstrap — Project Context

Monorepo for Sintj infrastructure services. Each subdirectory is a git submodule pointing to its own `sintj-labs/` GitHub repo. The submodule pointer in this repo IS the version pin for each service.

## Submodules

### service-bus (`sintj-labs/service-bus`)
Event streaming: Kafka (KRaft, no Zookeeper) + Debezium CDC.
- Deploys via Helm to k3d/k8s
- CDC: PostgreSQL logical replication → Debezium → Kafka topics
- Services: user, form, workflow
- See `service-bus/CLAUDE.md` for full context

### supertokens (`sintj-labs/supertokens`)
Authentication core: self-hosted SuperTokens running on Kubernetes.
- Deployed via Helm (`supertokens/supertokens-postgresql`)
- PostgreSQL-backed (RDS, same hosts as other services)
- Backend SDKs connect via `http://supertokens:3567`
- See `supertokens/CLAUDE.md` for full context

## Shared Conventions

- **K8s secrets:** `uat-env`, `sandbox-env`, `prod-env` hold DB credentials across all services
- **Environments:** UAT namespaces (jupiter, venus, saturn, mars, mercury), Sandbox (default), Prod (default)
- **RDS hosts:** `prosperix-uat-17` (UAT/Sandbox), `prosperix-prod-17` (Prod)
- **Deployment:** each service has its own `.github/workflows/` in its own repo

## Working with Submodules

```bash
# Update all submodules to latest
git submodule update --remote --merge

# Work inside a submodule
cd service-bus
git checkout main
# ... make changes, commit, push ...
cd ..
git add service-bus
git commit -m "chore: bump service-bus to <sha>"
git push
```

## Adding a New Service

1. Create `sintj-labs/<service>` repo on GitHub
2. `git submodule add https://github.com/sintj-labs/<service>.git <service>`
3. Add `README.md` + `CLAUDE.md` inside the submodule
4. Update root `README.md` and this `CLAUDE.md`
5. Commit `.gitmodules`, the submodule entry, and the docs
