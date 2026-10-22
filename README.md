# Home Assistant Management

A Home Assistant skill for maintaining configuration and automations, deploying custom integrations, and validating YAML and entity references. Includes Python validators and an entity explorer.

**Canonical source:** [gwyntel/homeassistant-management-skill](https://github.com/gwyntel/homeassistant-management-skill)  
**Skill name:** `homeassistant-management`  
**Requirements:** Home Assistant 2024.x+; Python 3.10+; PyYAML (`python3 -m pip install pyyaml`).

## Install with Vercel Skills CLI

Install for Hermes Agent globally:

```bash
npx skills add gwyntel/homeassistant-management-skill --skill homeassistant-management --agent hermes-agent -g -y
```

To inspect available skills before installing:

```bash
npx skills add gwyntel/homeassistant-management-skill --list
```

The Vercel CLI installs the whole skill folder, not just the entry point: a global install contains `SKILL.md`, `LICENSE.md`, `scripts/`, and `references/`. The bundled validators are usable immediately after install, with no extra download step.

## Use

Once installed, ask your agent to use the `homeassistant-management` skill for Home Assistant configuration or automation work. Run the bundled tools from the installed skill directory (a global install on Hermes lands in `~/.hermes/skills/homeassistant-management`; a project-local install lands in `.hermes/skills/homeassistant-management` under the project):

```bash
SKILL_DIR="${HERMES_HOME:-$HOME/.hermes}/skills/homeassistant-management"
python3 "$SKILL_DIR/scripts/yaml_validator.py" /path/to/ha/config/
python3 "$SKILL_DIR/scripts/reference_validator.py" /path/to/ha/config/
python3 "$SKILL_DIR/scripts/entity_explorer.py" --config /path/to/ha/config/ --domain light --full
```

The YAML validator checks syntax and HA YAML structures. The reference validator requires `.storage/core.entity_registry` in the config directory. See [SKILL.md](SKILL.md) for the complete workflow, API reference, and cautions; see [automation pitfalls](references/ha-automation-pitfalls.md) for common YAML hazards.

## Update

Update the installed skill with the Vercel Skills CLI. This refreshes the entire skill folder, including `scripts/` and `references/`:

```bash
npx skills update homeassistant-management -g -y
```

## Troubleshooting

- **Skill not discovered / invalid frontmatter:** Ensure the skill name is `homeassistant-management` and `SKILL.md` has YAML frontmatter with `name` and `description`. Re-run the install command with the explicit `--skill` and `--agent` options above.
- **Wrong installation destination:** `-g` installs globally; omit it for project-local installation. Use `--agent hermes-agent` to select Hermes Agent.
- **Scripts or references missing:** Reinstall and check the CLI output for the destination; the Vercel CLI copies the whole skill folder (`SKILL.md`, `scripts/`, `references/`). If the script files are absent, remove the partial copy and rerun the install command above.
- **Permission or install errors:** Check network access and that the selected agent's skills directory is writable; retry the command in an environment where `npx` can run.
- **Missing YAML dependency:** Install PyYAML in the Python environment used to run the scripts, as noted under Requirements above.

## License

Licensed under the Mutualist License (MutuaL-1.2); see [LICENSE.md](LICENSE.md). The existing license and skill authorship are retained.
