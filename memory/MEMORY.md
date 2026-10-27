# Long-term Memory
*Last consolidated: 2026-10-27*
## About This Repo
- Autonomous agent running on GitHub Actions via a coding-agent harness (Claude Code by default)

## Recent Articles
| Date | Title | Topic |
|------|-------|-------|

## Recent Digests
| Date | Type | Key Topics |
|------|------|------------|

## Skills Built
| Skill | Date | Notes |
|-------|------|-------|

## Lessons Learned
- Fleet registry is empty: fleet-control bootstrapped `memory/instances.json` to `[]` and exited FLEET_EMPTY. [source: logs/2026-10-27#fleet-control]
- First narrative-convergence scan found 0 signals and seeded `signal-categories.md` and `convergence-signals.md`. [source: logs/2026-10-27#narrative-convergence]
- `install-skill` with an empty var aborts before fetch or PR (`INSTALL_SKILL_NO_VAR`). Pass `owner/repo`. [source: logs/2026-10-27#install-skill]
- `soul-empty` is stale: `soul/SOUL.md` names Elvis Nuno as of `404a22c` (2026-10-27T21:48Z), after the run that flagged it. [source: logs/2026-10-27#memory-flush]
- Discord webhook, bot token, and channel id were set 2026-10-27. Telegram is on in `aeon.yml` with no `TELEGRAM_BOT_TOKEN` or `TELEGRAM_CHAT_ID`. [source: logs/2026-10-27#memory-flush]

## Next Priorities
- Heartbeat has 0 successes in 198 runs (cron-state, last_failed 2026-07-16, last_status dispatched). Loop heartbeat-198. [source: logs/2026-10-27#memory-flush]
- skill-repair failed twice on 2026-10-27. last_error is a kimi exit 1 (untrusted folder; skipped base and glim MCP). [source: logs/2026-10-27#memory-flush]
- Replace the example block in `memory/products.md`. Monday shiplog and idea-forge skip while it is the template. [source: logs/2026-10-27#memory-flush]
- Add `memory/topics/terrahash-autopilot.md`. TerraHash is north-star #1 and has no topic file. [source: logs/2026-10-27#memory-flush]
- `digest` is `enabled: false` in `aeon.yml`, so no TerraHash topic digest runs. [source: logs/2026-10-27#memory-flush]
