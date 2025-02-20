# Commands


SAMMI Starter Pack gives you access to a very handy moderator command that allows mods/yourself to add commands on the fly. You can edit/delete/disable these commands from the `Commands` tab in the bridge.

## Usage

`!command <operation> <command> <response>`

| Operation | Usage |
| -------- | ----- |
| `ADD` | `!command add <command> <response>` |
| `EDIT` | `!command edit <command> <new response>` |
| `RENAME` | `!command rename <command> <new name>` |M
| `REMOVE` | `!command remove <command>` |

Eg. `!command add hello Hello, world!`

## Arguments

Arguments are used to add values dynamically to your commands! 

Arugments can be used with the following syntax `${sender}`

Some Arguments take parameters and require a space to differentiate them for example `${rand 1-100}`;

| Argument | Parameters | Usage |Description |
| -------- | ---------- | ----- | ----------- |
| 1>100 | N/A | `${1}` `${3}`| Gets the word at the specified index, returns `""` if nothing was found. |
| sender | N/A | `${sender}` | Gets the name of the person who used the command. |
| target - NYI | N/A | `${target}` | Use `${1}` for now. Gets the name of the person who used the command. |
| rand | `100`, `50-100` | `${rand 100}` | Generates a random number up to the specified number, or between the range of `min-max`. Returns `""` if invalid. |
| rand.list | `('a' 'b')` | `${rand.list('Value 1' 'Value 2' 'Value 3')}` | Retrieves a random value from the specified list of values provided. Values must be enclosed in apostrophes (`'`) |
| count | Counter Variable | `${count cough}` | Gets the value of the counter, each time the counter is retrieved, it adds 1 to it.

The list of arguments is small and I get that, this was designed mainly to make adding simple dynamic commands easier. You can always make buttons that add commands that have complex functionality within SAMMI itself.

# Quotes

Not yet implemented.

# Announcements

Not yet implemented.

