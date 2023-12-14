oclif-hello-world
=================

oclif example Hello World CLI

[![oclif](https://img.shields.io/badge/cli-oclif-brightgreen.svg)](https://oclif.io)
[![CircleCI](https://circleci.com/gh/oclif/hello-world/tree/main.svg?style=shield)](https://circleci.com/gh/oclif/hello-world/tree/main)
[![GitHub license](https://img.shields.io/github/license/oclif/hello-world)](https://github.com/oclif/hello-world/blob/main/LICENSE)

<!-- toc -->
* [Usage](#usage)
* [Commands](#commands)
<!-- tocstop -->
# Usage
<!-- usage -->
```sh-session
$ npm install -g oclif-yarn4
$ oclif-yarn4 COMMAND
running command...
$ oclif-yarn4 (--version)
oclif-yarn4/0.0.0 linux-x64 node-v18.19.0
$ oclif-yarn4 --help [COMMAND]
USAGE
  $ oclif-yarn4 COMMAND
...
```
<!-- usagestop -->
# Commands
<!-- commands -->
* [`oclif-yarn4 hello PERSON`](#oclif-yarn4-hello-person)
* [`oclif-yarn4 hello world`](#oclif-yarn4-hello-world)
* [`oclif-yarn4 help [COMMANDS]`](#oclif-yarn4-help-commands)
* [`oclif-yarn4 plugins`](#oclif-yarn4-plugins)
* [`oclif-yarn4 plugins:install PLUGIN...`](#oclif-yarn4-pluginsinstall-plugin)
* [`oclif-yarn4 plugins:inspect PLUGIN...`](#oclif-yarn4-pluginsinspect-plugin)
* [`oclif-yarn4 plugins:install PLUGIN...`](#oclif-yarn4-pluginsinstall-plugin-1)
* [`oclif-yarn4 plugins:link PLUGIN`](#oclif-yarn4-pluginslink-plugin)
* [`oclif-yarn4 plugins:uninstall PLUGIN...`](#oclif-yarn4-pluginsuninstall-plugin)
* [`oclif-yarn4 plugins reset`](#oclif-yarn4-plugins-reset)
* [`oclif-yarn4 plugins:uninstall PLUGIN...`](#oclif-yarn4-pluginsuninstall-plugin-1)
* [`oclif-yarn4 plugins:uninstall PLUGIN...`](#oclif-yarn4-pluginsuninstall-plugin-2)
* [`oclif-yarn4 plugins update`](#oclif-yarn4-plugins-update)

## `oclif-yarn4 hello PERSON`

Say hello

```
USAGE
  $ oclif-yarn4 hello PERSON -f <value>

ARGUMENTS
  PERSON  Person to say hello to

FLAGS
  -f, --from=<value>  (required) Who is saying hello

DESCRIPTION
  Say hello

EXAMPLES
  $ oex hello friend --from oclif
  hello friend from oclif! (./src/commands/hello/index.ts)
```

_See code: [src/commands/hello/index.ts](https://github.com/garrettjstevens/oclif-yarn4/blob/v0.0.0/src/commands/hello/index.ts)_

## `oclif-yarn4 hello world`

Say hello world

```
USAGE
  $ oclif-yarn4 hello world

DESCRIPTION
  Say hello world

EXAMPLES
  $ oclif-yarn4 hello world
  hello world! (./src/commands/hello/world.ts)
```

_See code: [src/commands/hello/world.ts](https://github.com/garrettjstevens/oclif-yarn4/blob/v0.0.0/src/commands/hello/world.ts)_

## `oclif-yarn4 help [COMMANDS]`

Display help for oclif-yarn4.

```
USAGE
  $ oclif-yarn4 help [COMMANDS] [-n]

ARGUMENTS
  COMMANDS  Command to show help for.

FLAGS
  -n, --nested-commands  Include all nested commands in the output.

DESCRIPTION
  Display help for oclif-yarn4.
```

_See code: [@oclif/plugin-help](https://github.com/oclif/plugin-help/blob/v5.2.20/src/commands/help.ts)_

## `oclif-yarn4 plugins`

List installed plugins.

```
USAGE
  $ oclif-yarn4 plugins [--json] [--core]

FLAGS
  --core  Show core plugins.

GLOBAL FLAGS
  --json  Format output as json.

DESCRIPTION
  List installed plugins.

EXAMPLES
  $ oclif-yarn4 plugins
```

_See code: [@oclif/plugin-plugins](https://github.com/oclif/plugin-plugins/blob/v4.1.10/src/commands/plugins/index.ts)_

## `oclif-yarn4 plugins:install PLUGIN...`

Installs a plugin into the CLI.

```
USAGE
  $ oclif-yarn4 plugins add plugins:install PLUGIN...

ARGUMENTS
  PLUGIN  Plugin to install.

FLAGS
  -f, --force    Run yarn install with force flag.
  -h, --help     Show CLI help.
  -s, --silent   Silences yarn output.
  -v, --verbose  Show verbose yarn output.

GLOBAL FLAGS
  --json  Format output as json.

DESCRIPTION
  Installs a plugin into the CLI.
  Can be installed from npm or a git url.

  Installation of a user-installed plugin will override a core plugin.

  e.g. If you have a core plugin that has a 'hello' command, installing a user-installed plugin with a 'hello' command
  will override the core plugin implementation. This is useful if a user needs to update core plugin functionality in
  the CLI without the need to patch and update the whole CLI.


ALIASES
  $ oclif-yarn4 plugins add

EXAMPLES
  $ oclif-yarn4 plugins add myplugin 

  $ oclif-yarn4 plugins add https://github.com/someuser/someplugin

  $ oclif-yarn4 plugins add someuser/someplugin
```

## `oclif-yarn4 plugins:inspect PLUGIN...`

Displays installation properties of a plugin.

```
USAGE
  $ oclif-yarn4 plugins inspect PLUGIN...

ARGUMENTS
  PLUGIN  [default: .] Plugin to inspect.

FLAGS
  -h, --help     Show CLI help.
  -v, --verbose

GLOBAL FLAGS
  --json  Format output as json.

DESCRIPTION
  Displays installation properties of a plugin.

EXAMPLES
  $ oclif-yarn4 plugins inspect myplugin
```

_See code: [@oclif/plugin-plugins](https://github.com/oclif/plugin-plugins/blob/v4.1.10/src/commands/plugins/inspect.ts)_

## `oclif-yarn4 plugins:install PLUGIN...`

Installs a plugin into the CLI.

```
USAGE
  $ oclif-yarn4 plugins install PLUGIN...

ARGUMENTS
  PLUGIN  Plugin to install.

FLAGS
  -f, --force    Run yarn install with force flag.
  -h, --help     Show CLI help.
  -s, --silent   Silences yarn output.
  -v, --verbose  Show verbose yarn output.

GLOBAL FLAGS
  --json  Format output as json.

DESCRIPTION
  Installs a plugin into the CLI.
  Can be installed from npm or a git url.

  Installation of a user-installed plugin will override a core plugin.

  e.g. If you have a core plugin that has a 'hello' command, installing a user-installed plugin with a 'hello' command
  will override the core plugin implementation. This is useful if a user needs to update core plugin functionality in
  the CLI without the need to patch and update the whole CLI.


ALIASES
  $ oclif-yarn4 plugins add

EXAMPLES
  $ oclif-yarn4 plugins install myplugin 

  $ oclif-yarn4 plugins install https://github.com/someuser/someplugin

  $ oclif-yarn4 plugins install someuser/someplugin
```

_See code: [@oclif/plugin-plugins](https://github.com/oclif/plugin-plugins/blob/v4.1.10/src/commands/plugins/install.ts)_

## `oclif-yarn4 plugins:link PLUGIN`

Links a plugin into the CLI for development.

```
USAGE
  $ oclif-yarn4 plugins link PLUGIN

ARGUMENTS
  PATH  [default: .] path to plugin

FLAGS
  -h, --help          Show CLI help.
  -v, --verbose
      --[no-]install  Install dependencies after linking the plugin.

DESCRIPTION
  Links a plugin into the CLI for development.
  Installation of a linked plugin will override a user-installed or core plugin.

  e.g. If you have a user-installed or core plugin that has a 'hello' command, installing a linked plugin with a 'hello'
  command will override the user-installed or core plugin implementation. This is useful for development work.


EXAMPLES
  $ oclif-yarn4 plugins link myplugin
```

_See code: [@oclif/plugin-plugins](https://github.com/oclif/plugin-plugins/blob/v4.1.10/src/commands/plugins/link.ts)_

## `oclif-yarn4 plugins:uninstall PLUGIN...`

Removes a plugin from the CLI.

```
USAGE
  $ oclif-yarn4 plugins remove plugins:uninstall PLUGIN...

ARGUMENTS
  PLUGIN  plugin to uninstall

FLAGS
  -h, --help     Show CLI help.
  -v, --verbose

DESCRIPTION
  Removes a plugin from the CLI.

ALIASES
  $ oclif-yarn4 plugins unlink
  $ oclif-yarn4 plugins remove

EXAMPLES
  $ oclif-yarn4 plugins remove myplugin
```

## `oclif-yarn4 plugins reset`

Remove all user-installed and linked plugins.

```
USAGE
  $ oclif-yarn4 plugins reset
```

_See code: [@oclif/plugin-plugins](https://github.com/oclif/plugin-plugins/blob/v4.1.10/src/commands/plugins/reset.ts)_

## `oclif-yarn4 plugins:uninstall PLUGIN...`

Removes a plugin from the CLI.

```
USAGE
  $ oclif-yarn4 plugins uninstall PLUGIN...

ARGUMENTS
  PLUGIN  plugin to uninstall

FLAGS
  -h, --help     Show CLI help.
  -v, --verbose

DESCRIPTION
  Removes a plugin from the CLI.

ALIASES
  $ oclif-yarn4 plugins unlink
  $ oclif-yarn4 plugins remove

EXAMPLES
  $ oclif-yarn4 plugins uninstall myplugin
```

_See code: [@oclif/plugin-plugins](https://github.com/oclif/plugin-plugins/blob/v4.1.10/src/commands/plugins/uninstall.ts)_

## `oclif-yarn4 plugins:uninstall PLUGIN...`

Removes a plugin from the CLI.

```
USAGE
  $ oclif-yarn4 plugins unlink plugins:uninstall PLUGIN...

ARGUMENTS
  PLUGIN  plugin to uninstall

FLAGS
  -h, --help     Show CLI help.
  -v, --verbose

DESCRIPTION
  Removes a plugin from the CLI.

ALIASES
  $ oclif-yarn4 plugins unlink
  $ oclif-yarn4 plugins remove

EXAMPLES
  $ oclif-yarn4 plugins unlink myplugin
```

## `oclif-yarn4 plugins update`

Update installed plugins.

```
USAGE
  $ oclif-yarn4 plugins update [-h] [-v]

FLAGS
  -h, --help     Show CLI help.
  -v, --verbose

DESCRIPTION
  Update installed plugins.
```

_See code: [@oclif/plugin-plugins](https://github.com/oclif/plugin-plugins/blob/v4.1.10/src/commands/plugins/update.ts)_
<!-- commandsstop -->
