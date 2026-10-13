<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/opencode-dark.svg">
    <img src="assets/opencode-light.svg" alt="opencode" width="420">
  </picture>
  &nbsp;&nbsp;&nbsp;
  <img src="assets/deepseek.svg" alt="DeepSeek" width="100" height="100">
</p>

<h1 align="center">opencode + DeepSeek</h1>

<p align="center">
  A demo of running the <a href="https://opencode.ai">opencode</a> agent with
  <a href="https://www.deepseek.com">DeepSeek</a> models via Sandcastle.
</p>

## Overview

This repository wires the opencode coding agent to DeepSeek's API so that
Sandcastle can drive an autonomous agent loop with DeepSeek models.

## Getting started

```bash
npm install
npm run sandcastle
```

Copy [`.sandcastle/.env.example`](.sandcastle/.env.example) to
`.sandcastle/.env` and fill in the required keys (`OPENCODE_API_KEY` and
`GH_TOKEN`) before running.

## Configuration

The agent is configured in [`.sandcastle/main.ts`](.sandcastle/main.ts) and the
prompt template lives in [`.sandcastle/prompt.md`](.sandcastle/prompt.md).
