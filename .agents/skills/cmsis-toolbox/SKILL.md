---
name: cmsis-toolbox
description: This skill provides access to the CMSIS Toolbox, a collection of tools and libraries for Arm Cortex-M microcontrollers. It allows users to perform various tasks such as pack management, project generation, and build management using the CMSIS Toolbox command-line interface. It should be used when working with embedded applications that utilize CMSIS software packs and cmsis solution files.
---

# CMSIS Toolbox

## Requirements to use this skill
 * CMake 3.31.5 or higher
 * Ninja 1.12.0 or higher
 * CMSIS-Toolbox 2.0.0 or higher

## When to use this skill
 * When you need to install and manage CMSIS software packs in the host development environment.
 * When you need to orchestrate the build steps utilizing CMSIS tools and a CMake compilation process.
 * When you need to create build information for embedded applications that consist of one or more related projects.


## How to initialize the pack registry if it was not initialized before
```bash
cpackget init https://www.keil.com/pack/index.pidx
```

## How to update the pack registry
```bash
cpackget update-index
```

## How to register a toolchain for use by CMSIS Toolbox

Define an environment variable with following format: `<name>_TOOLCHAIN_<major>_<minor>_<patch>=<path/to/toolchain/binaries>`
Use the path to the directory containing the toolchain binaries (e.g., armclang.exe for Arm Compiler 6). The version numbers should correspond to the toolchain version you are registering.

Example on windows: `set AC6_TOOLCHAIN_6_19_0=C:\Keil_v5\ARM\ARMCLANG\bin`

## How to build a project using CMSIS Toolbox
* Build a solution named `example` using default settings  `cbuild <solution-name>.csolution.yml`
* Build a solution named `example` using a specific toolchain `cbuild <solution-name>.csolution.yml --toolchain AC6`
* Build a solution named `example` using a specific target `cbuild <solution-name>.csolution.yml --active <board-name>`
* Build a solution named `example` using a specific toolchain and target `cbuild <solution-name>.csolution.yml --toolchain AC6 --active <board-name>`

The solution file is generally in the root folder of the project and has a name in the format `<solution-name>.csolution.yml`. The solution file contains the build information for the project.

The `<board-name>` is the type entry of the target-types defined in the solution file. The solution file can contain multiple target-types, each with a different board name. The `--active` option is used to specify which target-type to build.

Option `--output <output-folder>` can be used to specify the output folder for the build artifacts. By default, the build artifacts are generated in the `build` folder in the root of the project.

The first build should add the option `--update-rte` to ensure that all required packs are installed and the RTE is up-to-date. After the first build, the option `--update-rte` can be omitted if there are no changes to the solution file or the pack registry.

When using an IDE, the 

## How to add a new software pack to the registry
* Add a new software pack to the registry `cpackget add <pack-name>`
* Add a new specific version of a software pack to the registry `cpackget add <pack-name>@<version-number>`

Example: `cpackget add Arm::CMSIS@6.1.0`

## How to list installed software packs in the registry
* List all installed software packs in the registry `csolution list packs`

## How to list packs required by the solution
`csolution list packs  <solution-name>.csolution.yml`

## How to install missing packs required by the solution
```bash
csolution list packs <solution-name>.csolution.yml -m >packs.txt
cpackget update-index               # optional to ensure that pack index is up-to-date
cpackget add -f packs.txt
```

