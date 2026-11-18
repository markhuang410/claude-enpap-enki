# claude-enpap-enki

Enpap Enki (恩帕普·恩基) persona plugin for Claude Code. This repository is both a plugin and a single-plugin marketplace.

## Components

| Path | Purpose |
|------|---------|
| `output-styles/enpap-enki.md` | Persona rules, appended to the system prompt. `force-for-plugin: true` applies it whenever the plugin is enabled. `keep-coding-instructions: true` keeps Claude Code's built-in engineering instructions. |
| `hooks/hooks.json` | SessionStart hook on `startup|resume|clear|compact`. |
| `hooks/session-start.json` | Short re-anchor injected as `additionalContext` (identity, language policy, stop-loss rule, skill precedence). |

## Local install

```
/plugin marketplace add markhuang410/claude-enpap-enki
/plugin install enpap-enki@enpap-enki
```

Update after pushing changes:

```
/plugin marketplace update enpap-enki
```

## Cloud sessions

Cloud sessions do not read `~/.claude`. Add this to `.claude/settings.json` in each project repository:

```json
{
  "extraKnownMarketplaces": {
    "enpap-enki": {
      "source": { "source": "github", "repo": "markhuang410/claude-enpap-enki" }
    }
  },
  "enabledPlugins": {
    "enpap-enki@enpap-enki": true
  }
}
```

If the plugin does not load in a cloud session, copy the files into the project repository instead:

```
mkdir -p .claude/output-styles
cp output-styles/enpap-enki.md .claude/output-styles/
```

and set `"outputStyle": "Enpap Enki"` in the project's `.claude/settings.json`. `force-for-plugin` only applies to plugin styles, so the explicit setting is required for the copied file.

## Signing

Commits drafted by Enki keep Hen as author and carry `Drafted-By` and `On-Behalf-Of` trailers. Claude Code's default `Co-Authored-By: Claude` trailer is controlled separately by the `attribution` setting in `settings.json`.
