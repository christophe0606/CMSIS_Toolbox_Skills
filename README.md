# README

Some skills to use CMSIS Toolbox (`csolution`, `cbuild` and `cpackget`) from AI agents.

Work in progress ...

This project also uses an `AGENTS.md` file for debug purposes. This file tells the agent to log all executed command and check if they have generated warnings or errors.
This slow down the build compared to a direct use of the skill.


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
