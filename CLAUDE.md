# wopr-plugin-canvas

`@wopr-network/wopr-plugin-canvas` — Canvas visual workspace plugin for WOPR. Agents push HTML/Markdown/chart/form content to the WebUI.

## Commands

```bash
pnpm build       # tsc
pnpm lint        # biome check src/
pnpm format      # biome format --write src/
pnpm run check   # biome check + tsc --noEmit (run before committing)
pnpm test        # vitest run
```

**Linter/formatter is Biome.** Never add ESLint/Prettier config.

## Architecture

```
src/
  index.ts        # Plugin entry — exports WOPRPlugin default
  canvas.ts       # Canvas protocol — state, operations, broadcast
  a2a-canvas.ts   # A2A tool server factory (per-session)
  routes.ts       # Hono REST API routes
```

## Plugin Contract

This plugin imports ONLY from `@wopr-network/plugin-types` — never from wopr core internals.

```typescript
import type { WOPRPlugin, WOPRPluginContext, PluginManifest } from "@wopr-network/plugin-types";
```

The default export must satisfy `WOPRPlugin`. The plugin receives `WOPRPluginContext` at `init()` time.

## Key Conventions

- Canvas state is in-memory (no persistence)
- Extensions: `canvas:router` (Hono router), `canvas:setPublish` (WebSocket injection)
- A2A tools registered per session (guarded with `if (ctx.registerA2AServer)`)
- Module-level `let ctx` and `const cleanups` pattern for proper shutdown
- `shutdown()` reverses all registrations, clears injections, sets `ctx = null`
- Biome for linting/formatting
- `pnpm run check` must pass before every commit

## Issue Tracking

Issues tracked in Linear under the WOPR project.

## Version Control: Prefer jj

Use `jj` (Jujutsu) for all VCS operations instead of `git`:
- `jj status`, `jj diff`, `jj log` for inspection
- `jj new` to start a change, `jj describe` to set the message
- `jj commit` to commit, `jj push` to push
- `jj squash`, `jj rebase`, `jj edit` for history manipulation

Fall back to `git` only for operations not yet supported by `jj`.

