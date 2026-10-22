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

The Vercel CLI installs the skill entry point. To use its bundled scripts and reference, also clone the repository:

```bash
git clone https://github.com/gwyntel/homeassistant-management-skill.git
cd homeassistant-management-skill
python3 -m pip install pyyaml
```

## Use

Once installed, ask your agent to use the `homeassistant-management` skill for Home Assistant configuration or automation work. For bundled tools from the repository directory:

```bash
python3 scripts/yaml_validator.py /path/to/ha/config/
python3 scripts/reference_validator.py /path/to/ha/config/
python3 scripts/entity_explorer.py --config /path/to/ha/config/ --domain light --full
```

The YAML validator checks syntax and HA YAML structures. The reference validator requires `.storage/core.entity_registry` in the config directory. See [SKILL.md](SKILL.md) for the complete workflow, API reference, and cautions; see [automation pitfalls](references/ha-automation-pitfalls.md) for common YAML hazards.

## Update

Update the installed skill with the Vercel Skills CLI:

```bash
npx skills update homeassistant-management -g -y
```

Update the cloned scripts and references separately:

```bash
cd homeassistant-management-skill
git pull --ff-only
```

## Troubleshooting

- **Skill not discovered / invalid frontmatter:** Ensure the skill name is `homeassistant-management` and `SKILL.md` has YAML frontmatter with `name` and `description`. Re-run the install command with the explicit `--skill` and `--agent` options above.
- **Wrong installation destination:** `-g` installs globally; omit it for project-local installation. Use `--agent hermes-agent` to select Hermes Agent.
- **Scripts or references missing:** The CLI installs the skill entry point; clone the repository to get `scripts/` and `references/`.
- **Permission or install errors:** Check network access and that the selected agent's skills directory is writable; retry the command in an environment where `npx` can run.
- **Missing YAML dependency:** Install PyYAML with `python3 -m pip install pyyaml` in the Python environment used to run the scripts.

## License

Licensed under the Mutualist License (MutuaL-1.2); see [LICENSE.md](LICENSE.md). The existing license and skill authorship are retained.
