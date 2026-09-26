---
name: webdev-readme-fullstack-portable
description: Portable guidance for installing and using the webdev-readme-fullstack development guide in any AI agent, coding assistant, or project. Use when importing this skill into a skill-capable AI, adapting it to system/project instructions, or building a React + tRPC + Express + Drizzle full-stack web app.
---

# Portable Webdev Fullstack Skill

Use this skill as a platform-neutral version of the `webdev-readme-fullstack` guide. It can be installed as a native skill, copied into an AI's project instructions, or pasted into a system/developer prompt when the target AI has no skill mechanism.

## Installation workflow

1. Identify the target AI's instruction mechanism:
   - **Native skills:** copy this complete skill folder into its skills directory and ensure `SKILL.md` remains at the folder root.
   - **Project rules / custom instructions:** copy the body of this file, starting at `# Portable Webdev Fullstack Skill`, into the project's instruction file.
   - **System prompt / workspace rules:** add the same body as a reusable system or workspace instruction.
   - **Plain chat AI with no persistent instructions:** upload or paste this file at the start of a coding session and ask the AI to follow it for the project.
2. Preserve the folder name `webdev-readme-fullstack-portable` and the `SKILL.md` filename for skill systems that discover skills by convention.
3. Tell the target AI whether the project is actually running on Manus WebDev. Do not claim Manus-only tools, OAuth, storage, or environment variables exist when they do not.
4. Before coding, inspect the repository and map the abstract capabilities below to the project's actual framework, database, auth, storage, and deployment tools.

## Compatibility rule

This guide is **portable guidance, not a replacement runtime**. It does not install React, tRPC, Express, Drizzle, OAuth, a database, or cloud storage by itself. The target AI must first inspect `package.json`, lockfiles, source directories, environment files, and deployment configuration.

When a project differs from the reference stack:

- Preserve the project's existing conventions unless the user explicitly requests a migration.
- Translate concepts rather than blindly copying imports or commands.
- Never invent credentials, API keys, database URLs, OAuth endpoints, or storage paths.
- Ask only when a missing choice materially changes architecture; otherwise choose a conventional, reversible implementation and document it.

## Reference architecture

The reference full-stack template uses:

- React + TypeScript + Tailwind CSS for the client.
- Express for the server.
- tRPC for typed client/server procedures.
- Drizzle ORM for schema and queries.
- Vitest for tests.
- OAuth/session authentication.
- Object storage for media instead of bundling large assets in the frontend.

Recommended responsibility boundaries:

```text
client/src/pages/          Page-level UI
client/src/components/     Reusable UI
client/src/lib/            Client bindings
server/db.ts               Database helpers
server/routers.ts          Typed procedures/API contract
db or drizzle/             Schema and migrations
storage/                   Object-storage helpers
shared/                    Shared types and constants
```

Use the repository's actual paths when they differ.

## Build loop

For every feature, follow this sequence:

1. Inspect the existing code, routes, schema, auth model, and reusable components.
2. Update the database schema when persistence is required.
3. Generate and apply a migration using the project's documented migration command. Read the generated SQL before applying it.
4. Add focused database helpers; return the project's normal raw/domain shape consistently.
5. Add a typed procedure, route, or service method. Keep authorization at the server boundary.
6. Build the UI with the existing component system and design tokens.
7. Connect the UI through the project's typed client or service layer; do not add a second ad-hoc API client.
8. Handle loading, empty, validation, permission, and error states.
9. Add or update tests, then run the project's formatter, type checker, tests, and build.
10. Verify the feature in a running browser or integration environment when available.

## Frontend standards

- Decide the visual direction before implementing the page: palette, typography, density, layout, and light/dark behavior.
- Use existing design tokens and component primitives before creating custom CSS.
- Use a dashboard/sidebar layout for internal tools and admin panels; use purpose-built navigation for public products, marketing sites, communities, and storefronts.
- Prefer responsive, mobile-first layouts with visible focus states and keyboard access.
- Provide clear loading, empty, success, and error states.
- Use optimistic updates for low-risk list edits and toggles; use explicit loading and server confirmation for authentication, payments, destructive, or other critical actions.
- Never call state setters or navigation during render; use event handlers or effects.
- Keep animations short and interruptible, animate `transform`/`opacity` where possible, and respect `prefers-reduced-motion`.

## Backend and data standards

- Keep authorization on the server; never rely on hidden UI controls for access control.
- Validate input at the procedure/route boundary.
- Keep schema, generated migrations, and the live database synchronized.
- Reuse one data-access pattern rather than scattering raw queries across UI files.
- Prefer typed procedures/client hooks when the project uses tRPC; otherwise use the existing typed API layer.
- Keep secrets in environment configuration and never commit `.env` files or credentials.
- Use transactions for multi-step writes that must succeed or fail together.
- Return safe error messages to clients and log actionable server-side details without secrets.

## Authentication and integrations

If the project uses the Manus reference environment, follow its existing OAuth callback, session context, protected procedure, and auth hooks. Otherwise, first identify the project's auth provider and adapt these concepts:

- public versus protected server operations;
- current-user/session lookup;
- login, logout, and callback routes;
- role/permission checks;
- secure cookie or token handling.

For external integrations, inspect the repository's connector documentation and environment variables. Use an existing connector/client when available. Do not create fake integration responses merely to hide missing configuration.

## Images and large media

Do not place large images, videos, or generated media in frontend public/assets directories when the deployment system bundles them into the application. Prefer the project's object storage or CDN workflow, keep originals outside the repository when appropriate, and reference stable uploaded URLs/paths. Small static files such as favicons, robots files, and manifests may remain in the public directory.

## Completion checklist

Before declaring a feature complete, verify:

- [ ] Existing architecture and reusable components were inspected first.
- [ ] Schema, migration, and live database are synchronized when data changed.
- [ ] Server validation and authorization are present.
- [ ] UI uses the established typed API/data layer.
- [ ] Loading, empty, error, permission, and success states work.
- [ ] Responsive and keyboard-accessible behavior was checked.
- [ ] No credentials, secrets, or large untracked media were added.
- [ ] Tests, type checks, lint/format, and production build pass.
- [ ] Browser/integration verification was performed when available.
- [ ] Any platform-specific assumptions are documented for the user.

## Platform adaptation note

When the target AI asks where to install this skill, recommend its documented workspace/project skills folder first. If it has no such folder, use project instructions or a repository-level `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `.cursor/rules/`, or equivalent instruction file according to that AI's conventions. Keep this file as the source of truth and copy it rather than rewriting it into unrelated framework-specific rules.
