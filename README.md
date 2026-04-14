# README

Some skills to use CMSIS Toolbox (`csolution`, `cbuild` and `cpackget`) from AI agents.

Work in progress ...

## Configuration

In `$HOME/.codex/config.toml` you may have to customize the configuration.

On Windows you'll need:

```
[windows]
sandbox = "elevated"
```
For access to CMSIS Toolbox tools, compilers etc ... you may
inherit all the environment when the agent is launching some external tools.

```
[shell_environment_policy]
inherit = "all"
```
