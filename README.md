<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/opencode-dark.svg">
    <img src="assets/opencode-light.svg" alt="opencode" height="200" width="420">
  </picture>
  &nbsp;&nbsp;&nbsp;
  <img src="assets/deepseek.svg" alt="DeepSeek" width="20" height="20">
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

### Prerequisites

- [Node.js](https://nodejs.org) and npm
- [Docker](https://docs.docker.com/get-docker/) — the agent runs inside an isolated container
- [GitHub CLI](https://cli.github.com) (`gh`) — the agent reads and manages GitHub Issues
- A [DeepSeek API key](https://platform.deepseek.com)
- A [GitHub personal access token](https://github.com/settings/personal-access-tokens/new)

### Setup

1. Install dependencies:

   ```bash
   # might have activate docker first
   colima start

   # create directory for project and run this commands.
   npm init
   npm install --save-dev @ai-hero/sandcastle

   # This scaffolds a .sandcastle directory with all the files needed.
   npx @ai-hero/sandcastle init
   ```

2. Update the newly created `main.ts` file

   ```ts
   // agent: opencode("opencode/big-pickle"),
   agent: opencode("deepseek/deepseek-flash"),
   ```

3. Create your environment file by copying the example:

   ```bash
   cp .sandcastle/.env.example .sandcastle/.env

   # delete OPENCODE_API_KEY=
   ```

4. Fill in the required values in `.sandcastle/.env`:

   - `DEEPSEEK_API_KEY` — your DeepSeek API key.
   - `GH_TOKEN` — a fine-grained GitHub personal access token. Under
     **Repository permissions** it needs **Issues: Read and write** and
     **Metadata: Read**. Some agents may also need **Contents: Read and write**
     and **Pull requests: Read and write**.

5. Create GitHub Issues for the work you want the agent to pick up, and give
   each one the **`Sandcastle`** label. The agent only looks at open issues with
   that label. See the
   [Sandcastle README](https://github.com/mattpocock/sandcastle/blob/main/README.md)
   for more on getting started.

6. Run the agent:

   ```bash
   npx tsx .sandcastle/main.ts

   # or in application root. add script to package.json

   "scripts": {
    "sandcastle": "npx tsx .sandcastle/main.ts && git push origin HEAD"
   },
   ```

   This executes [`.sandcastle/main.ts`](.sandcastle/main.ts) and pushes the
   resulting commits to the current branch.

## Configuration

The agent is configured in [`.sandcastle/main.ts`](.sandcastle/main.ts) and the
prompt template lives in [`.sandcastle/prompt.md`](.sandcastle/prompt.md).
