# Deployment Readiness Checklist

A personal, reusable engineering reference to run through before deploying any project — websites, web apps, APIs, backend services, frontends, ML applications, or full-stack systems.

## Purpose

Deployments fail for a small, repeatable set of reasons: a secret leaked into git, an endpoint that trusts the frontend, a migration with no rollback path, a backup that was never actually restored, a health check nobody wired up. This repo exists to catch those failures *before* they ship, every time, regardless of which stack a given project uses.

It is not a generic "best practices" list padded out for length. Every item earned its place because it maps to a real, common way deployments go wrong.

## Who it's for

Primarily: me, before every deployment. Structured so it's also useful to:
- Anyone shipping solo projects who doesn't have a second engineer to catch what they missed
- Small teams without a dedicated security/DevOps review process
- Anyone who wants a stack-agnostic reference to adapt to their own workflow

## Priority system

- 🔴 **Critical** — directly prevents a security breach, data loss, or an outage. Don't skip these.
- 🟡 **Recommended** — standard good practice; skipping has a real but smaller cost.
- 🟢 **Nice-to-have** — genuinely useful polish, not a blocker.

Some items are also tagged with an **Applicability** note (e.g. *Docker/Kubernetes projects*, *marketing/content sites only*). If a tagged item doesn't match your stack or project type, skip it — it isn't a gap, it's just not relevant.

## Not every item applies to every project

An internal API has no use for SEO meta tags. A static marketing site has no database migrations to worry about. Read the Applicability tags and use judgment — the goal is a checklist that catches real problems for *your* project, not 100% completion for its own sake.

## How to use this

1. Copy `CHECKLIST.md` into your project (or keep this repo open alongside it).
2. Go category by category. Sections 4–7 (Secrets, Security, Auth, Database) matter most if you're short on time — they cover the failures that are hardest to recover from.
3. Check off what applies, skip what doesn't, and use the "why it matters" note on any item you're tempted to skip but aren't sure about.
4. Run the **Smoke Testing** and **Rollback** sections *after* every deploy, not just before — they're your safety net if something still goes wrong.
5. Update `CHECKLIST.md` itself whenever you catch a new class of mistake in the wild — that's the whole point of keeping this as a living reference. Log meaningful changes in `CHANGELOG.md`.

## Structure

```
deployment-readiness-checklist/
├── README.md
├── CHECKLIST.md              # canonical source — the full checklist
├── deployment-checklist.pdf  # printable version, generated from CHECKLIST.md
├── CHANGELOG.md
└── templates/
    ├── .env.example
    └── production-notes.md
```

`CHECKLIST.md` is the single source of truth. The PDF is generated from it and should never contradict it — if you ever need to update the checklist, edit the Markdown first, then regenerate the PDF.
