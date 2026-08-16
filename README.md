# skills

Agent skills by [Renzo Bianchi](https://github.com/renzobianchi).

## Install

```bash
npx skills add renzobianchi/skills
```

Pick the skills you want, or install everything at once. Works with Claude Code, Cursor, Codex, opencode, and any agent that supports the [skills](https://skills.sh) format.

Claude Code users can also install via the plugin marketplace:

```
/plugin marketplace add renzobianchi/skills
```

## Skills

### html

Turn agent↔designer conversations into standalone interactive HTML artifacts: review docs with approve/deny/discuss controls, N-way prototype variant boards, before/after motion comparisons, visual explorers, and inline-editable copy ecosystems.

The core idea: instead of describing options in bullet points, the agent builds a single `.html` file that renders the real thing — real tokens, real copy, real motion — and every artifact ends with a **Copy response** button that serializes your clicks and notes back into a compact prompt for the next iteration. Seeing beats imagining, and responding costs one click.

```
/html build the review doc with the pending findings from the critique
/html show me 4 layout directions for the work section
```

## Credits

The `html` skill is inspired by the artifact-driven design workflows of [Kyle Zantos](https://x.com/kylezantos) and [Michael Riddering (Ridd)](https://x.com/Ridd_design).

## License

[MIT](LICENSE)
