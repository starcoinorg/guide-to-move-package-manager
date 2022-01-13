## Move Package Manager Tutorial

Move Pacakge Manaager(mpm) is a command line tool to manage move pacakges, like Cargo for Rust, or NPM for NodeJS.
It integrates the latest move pacakge system introduced in [diem/move](https://github.com/diem/move/tree/main/language/tools/move-package),

and reuse most functionality of [move-cli](https://github.com/diem/move/tree/main/language/tools/move-cli) by diem.

**Before dive into this tutorial, please read the [pacakge section](https://github.com/diem/move/blob/main/language/documentation/book/src/packages.md) of move book first.**
Understanding how move package work is a prerequest.


### Overview of mpm

``` shell
move-package-manager
Package and build system for Move code.

USAGE:
    mpm [FLAGS] [OPTIONS] <SUBCOMMAND>

FLAGS:
    -d, --dev        Compile in 'dev' mode. The 'dev-addresses' and 'dev-dependencies' fields will be used if this flag
                     is set. This flag is useful for development of packages that expose named addresses that are not
                     set to a specific value
        --force      Force recompilation of all packages
        --abi        Generate ABIs for packages
        --doc        Generate documentation for packages
    -h, --help       Prints help information
        --test       Compile in 'test' mode. The 'dev-addresses' and 'dev-dependencies' fields will be used along with
                     any code in the 'test' directory
    -V, --version    Prints version information
    -v               Print additional diagnostics if available

OPTIONS:
        --install-dir <install-dir>    Installation directory for compiled artifacts. Defaults to current directory
    -p, --path <package-path>          Path to a package which the command should be run with respect to [default: .]

SUBCOMMANDS:
    experimental    (Experimental) Run static analyses on Move source or bytecode
    help            Prints this message or the help of the given subcommand(s)
    package         Execute a package command. Executed in the current directory or the closest containing Move
                    package
    sandbox         Execute a sandbox command
    spectest        Datatest-harness for running data-driven tests
```


mpm is a convenient wrapper and superset of [diem/move-cli](https://github.com/diem/move/tree/main/language/tools/move-cli).
What applies to move-cli is also applied to mpm.

**So, We recommend you to go through the [tutorial](https://github.com/diem/move/tree/main/language/documentation/tutorial) written by diem.**

In that tutorial, you can add an alias `alias move="mpm"` so that you can invoke move as it is.
You can check that it is working by running the following command:

```
move package -h

mpm-package 0.1.0
Execute a package command. Executed in the current directory or the closest containing Move package

USAGE:
    mpm package [FLAGS] [OPTIONS] <SUBCOMMAND>

FLAGS:
    -d, --dev        Compile in 'dev' mode. The 'dev-addresses' and 'dev-dependencies' fields will be used if this flag
                     is set. This flag is useful for development of packages that expose named addresses that are not
                     set to a specific value
        --force      Force recompilation of all packages
        --abi        Generate ABIs for packages
        --doc        Generate documentation for packages
    -h, --help       Prints help information
        --test       Compile in 'test' mode. The 'dev-addresses' and 'dev-dependencies' fields will be used along with
                     any code in the 'test' directory
    -V, --version    Prints version information
    -v               Print additional diagnostics if available

OPTIONS:
        --install-dir <install-dir>    Installation directory for compiled artifacts. Defaults to current directory
    -p, --path <package-path>          Path to a package which the command should be run with respect to [default: .]

SUBCOMMANDS:
    build          Build the package at `path`. If no path is provided defaults to current directory
    coverage       Inspect test coverage for this package. A previous test run with the `--coverage` flag must have
                   previously been run
    disassemble    Disassemble the Move bytecode pointed to
    errmap         Generate error map for the package and its dependencies at `path` for use by the Move explanation
                   tool
    help           Prints this message or the help of the given subcommand(s)
    info           Print address information
    new            Create a new Move package with name `name` at `path`. If `path` is not provided the package will
                   be created in the directory `name`
    prove          Run the Move Prover on the package at `path`. If no path is provided defaults to current
                   directory. Use `.. prove .. -- <options>` to pass on options to the prover
    test           Run Move unit tests in this package
```

### Spec Test

Based on move-cli, mpm add the support to write spec test to test your move pacakge in the whole.

It can simulates:

- account initialization.
- block generation.
- module publishing.
- execute scripts or script function.

All actions are wrapped into transactions. So it can mock real actions onchain.


