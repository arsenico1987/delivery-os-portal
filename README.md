# delivery-os portal

A zero-infra, browser-only wizard that spins up a new project from the
[`delivery-os`](https://github.com/arsenico1987/delivery-os) template.

**Live:** https://arsenico1987.github.io/delivery-os-portal/

## What it does
Fill the form → it calls the GitHub API (with *your* token, from your browser) to:
1. create a repo from the `delivery-os` template,
2. commit your `delivery-os.config.yml`,
3. dispatch the repo's **Bootstrap project** workflow (token substitution · labels ·
   branch-protection ruleset · hub `hello`).

The new repo arrives with the `.claude/` agents + commands already in it. The 3
scheduled cloud agents (Ideation · Refinement · Reporter) are registered separately in
Claude Code via `/schedule`.

## Auth
A **fine-grained PAT** (or classic `repo` + `workflow` token), supplied at runtime and
kept only in the browser tab's `sessionStorage` — it is sent **only** to `api.github.com`
and never stored or transmitted anywhere else. This page is static and holds no secrets.

Fine-grained token needs, on your account, *All repositories* with: `Administration`
read/write, `Contents` read/write, `Actions` read/write.

> Why a PAT and not the GitHub App: a pure static page can't hold an App's private key or
> complete its OAuth token exchange (browser CORS blocks GitHub's OAuth endpoints). The
> GitHub App is the auth for the hosted Azure portal phase, where a backend can hold it.

This repo is intentionally **public** (so GitHub Pages serves it on the free plan); the
`delivery-os` template stays private and is generated via your token.
