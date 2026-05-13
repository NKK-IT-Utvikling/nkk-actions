@~/.nkk/CLAUDE.md

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository. NKK-wide conventions are imported from `~/.nkk/CLAUDE.md` (see [`nkk-developer/doc/setup-claude.sh`](https://github.com/NKK-IT-Utvikling/nkk-developer/blob/main/doc/setup-claude.sh)).

## What this is

Org-wide reusable GitHub Actions workflows consumed by all NKK repos. Updates here ripple to every consuming repository the next time their workflows run — change carefully.

## Reusable workflows (`.github/workflows/`)

- **maven-build.yml** — Standard Maven build. Inputs: JDK version, Maven goals, Axon license toggle. Handles GitHub Packages auth.
- **node-build.yml** — Node.js / npm build. Inputs: Node version, working directory, optional `gen-api` step for OpenAPI clients. GitHub npm registry auth.
- **maven-release.yml** — Release workflow (Maven Central + GitHub Packages). Creates tag, publishes artifacts, handles versioning.
- **codeql.yml** — CodeQL security analysis for Java repos. Configures Maven `settings.xml` with the GitHub Packages token before autobuild (CodeQL default setup can't do this).
- **deploy-spring-boot.yml** — Deploy Spring Boot JAR to EC2 with security group, context path, and owner customization.
- **deploy-jetty.yml** — Deploy WAR to self-hosted Jetty server with profile selection.
- **deploy-jetty-ec2.yml** — Deploy WAR to EC2-hosted Jetty.
- **dependabot-auto-merge.yml** — Auto-approve/merge Dependabot patch updates, GitHub Actions, and grouped PRs.

## Using in your repo

Repos call these via `uses: NKK-IT-Utvikling/nkk-actions/.github/workflows/<name>.yml@main`, with `secrets: inherit` to pass the GitHub Packages token through.

## Helper scripts

`.scripts/` holds org-wide deploy/sync helpers (e.g. CodeQL deploy, Dependabot patches, branch-protection sync). Follow the wrapper-`SCRIPT_DIR` pattern from the org-wide CLAUDE.md when adding new scripts.
