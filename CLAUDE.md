## Resource rules (many agents run in parallel on this machine)
- Only run tests related to your change: `npx vitest run <path>`, never the full suite unless asked.
- Never start watch mode (`vitest` without `run`, `npm run dev`, `tsc --watch`).
- Don't run `npm install` unless package.json changed.
- Stop any server or background process you started before finishing.
