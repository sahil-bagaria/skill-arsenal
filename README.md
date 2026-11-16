# Skill Arsenal

A Claude plugin marketplace that installs 220+ skills, in 15 packs, **directly from the GitHub repositories of the people who made them**. This repo holds no copies of their skills: each pack points at its maker's repo, so when they ship an update you get it.

## Install

**Claude app (claude.ai, desktop, Cowork):** Customize → Plugins → Add → Add marketplace → enter `sahil-bagaria/skill-arsenal`, then add the packs you want. Turn on **Sync automatically**, or use **Check for updates**, to pull the makers' latest versions.

**Claude Code:**

```
/plugin marketplace add sahil-bagaria/skill-arsenal
/plugin install arsenal-gstack@skill-arsenal
```

## Packs

| Pack | Skills | Source (original maker) | Maker | License |
|---|---|---|---|---|
| `arsenal-gstack` | 64 | [garrytan/gstack](https://github.com/garrytan/gstack) | Garry Tan | MIT |
| `arsenal-ui-ux-pro-max` | 7 | [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | nextlevelbuilder | MIT |
| `day-trader-skill` | 11 | [Jakeschincariol/day-trader-skill](https://github.com/Jakeschincariol/day-trader-skill) | Jake Schincariol | MIT |
| `arsenal-ponytail` | 6 | [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) | Dietrich Gebert | MIT |
| `arsenal-claude-mem` | 30 | [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | thedotmack | AGPL-3.0 |
| `arsenal-prompt-master` | 1 | [nidhinjs/prompt-master](https://github.com/nidhinjs/prompt-master) | nidhinjs | MIT |
| `arsenal-agent-reach` | 1 | [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) | Panniantong | MIT |
| `arsenal-omniroute` | 46 | [diegosouzapw/OmniRoute](https://github.com/diegosouzapw/OmniRoute) | diegosouzapw | MIT |
| `arsenal-data-science` | 30 | [K-Dense-AI/scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills) | K-Dense AI | MIT (each skill keeps its own license) |
| `arsenal-research` | 6 | [K-Dense-AI/scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills) | K-Dense AI | MIT (each skill keeps its own license) |
| `arsenal-documents` | 3 | [K-Dense-AI/scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills) | K-Dense AI | MIT (each skill keeps its own license) |
| `arsenal-visual-business` | 4 | [K-Dense-AI/scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills) | K-Dense AI | MIT (each skill keeps its own license) |
| `arsenal-finance` | 3 | [anthropics/claude-cookbooks](https://github.com/anthropics/claude-cookbooks) | Anthropic | MIT |
| `founder-skill` | 11 | [Jakeschincariol/founder-skill](https://github.com/Jakeschincariol/founder-skill) | Jake Schincariol | MIT |
| `arsenal-n8n-workflows` | 1 | this repo (library: [Zie619/n8n-workflows](https://github.com/Zie619/n8n-workflows)) | Sahil Bagaria | MIT |

Skill counts are what the makers' repos held on 14 November 2026; they change as the makers add or remove skills.

## Also from their makers (add these marketplaces directly)

| Marketplace | What you get |
|---|---|
| `anthropics/skills` | Anthropic's document skills: PDF, Word, Excel, PowerPoint |

## Licenses and credit

Every skill belongs to its maker and is used under that maker's license, linked in the table above. Some individual skills inside the K-Dense collection carry their own licenses (for example `what-if-oracle` is CC BY-NC-SA 4.0, non-commercial; `scikit-survival` is GPL-3.0); check a skill's `SKILL.md` before commercial use. claude-mem is AGPL-3.0.

The marketplace file, this README and the `arsenal-n8n-workflows` plugin are © 2026 Sahil Bagaria, released under the MIT License (see `LICENSE`). Anyone can clone, fork, use and change them.

## Requirements some packs have

- **OmniRoute** skills need the `omniroute` CLI, and the `omni-*` ones a running OmniRoute server.
- **Research** skills (exa-search, parallel-web, research-lookup) need their API keys.
- **gstack** browser skills need its full install (Playwright Chromium).
- **arsenal-claude-mem** search skills need claude-mem's memory worker; this pack installs the skills only, not its hooks.
- **n8n-workflows** expects a local clone of the library: `git clone https://github.com/Zie619/n8n-workflows ~/.claude/skill-repos/n8n-workflows`
