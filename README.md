# service-bootstrap

Monorepo for Sintj's service infrastructure. Each subdirectory is a git submodule with its own repo under `sintj-labs/`.

## Services

| Service | Description |
|---------|-------------|
| [service-bus](./service-bus) | Kafka (KRaft) + Debezium CDC — at-least-once event streaming across microservices |
| [supertokens](./supertokens) | Self-hosted SuperTokens Core — authentication API (sessions, users, recipes) |

## Getting Started

Clone with submodules:

```bash
git clone --recurse-submodules https://github.com/sintj-labs/service-bootstrap.git
```

Or if already cloned:

```bash
git submodule update --init --recursive
```

## Structure

```
service-bootstrap/
├── service-bus/      # Kafka + Debezium  (→ sintj-labs/service-bus)
└── supertokens/      # SuperTokens Core  (→ sintj-labs/supertokens)
```

## Working with Submodules

```bash
# Update a submodule to its latest remote commit
git submodule update --remote service-bus

# Make changes inside a submodule
cd supertokens
git checkout main
# ... edit, commit, push as a normal repo ...
cd ..
git add supertokens          # record the new commit pointer
git commit -m "chore: bump supertokens"
```

## Adding a New Service

1. Create `sintj-labs/<service>` on GitHub
2. `git submodule add https://github.com/sintj-labs/<service>.git <service>`
3. Add `README.md` and `CLAUDE.md` inside the new submodule
4. Update this README and `CLAUDE.md`
