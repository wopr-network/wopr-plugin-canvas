# @wopr-network/wopr-plugin-canvas

> Canvas visual workspace plugin for WOPR — agents push HTML, Markdown, charts, and forms to the WebUI in real time.

## Install

```bash
npm install @wopr-network/wopr-plugin-canvas
```

## Usage

```bash
wopr plugin install github:wopr-network/wopr-plugin-canvas
```

Then configure via `wopr configure --plugin @wopr-network/wopr-plugin-canvas`.

## Configuration

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| (no required configuration) | — | — | Canvas operates automatically once installed |

## What it does

The canvas plugin enables WOPR agents to push visual content (HTML snippets, Markdown documents, charts, and interactive forms) to the WebUI through a shared canvas workspace. It exposes a REST API mounted at `/canvas` and broadcasts updates to connected clients via WebSocket. Each agent session gets its own A2A canvas tools for rendering content.

## License

MIT
