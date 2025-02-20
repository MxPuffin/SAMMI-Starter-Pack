# Commands

SAMMI Starter Pack gives you access to a very handy moderator command that allows mods/yourself to add commands on the fly. You can edit/delete/disable these commands from the `Commands` tab in the bridge.

## Usage

!command <operation> <command> <response>

| Operation | Usage |
| -------- | ----- |
| `ADD` | `!command add <command> <response>` |
| `EDIT` | `!command edit <command> <new response>` |
| `RENAME` | `!command rename <command> <new name>` |M
| `REMOVE` | `!command remove <command>` |

Eg. `!command add hello Hello, world!`

## Using Arguments in Commands

Arguments allow you to dynamically insert values into your coammands, making them more flexible and interactive.

## Syntax
Use arguments in your commands with the following syntax:

```plaintext
${argument}
```
Some arguments take parameters and require a space to separate them. For Example:

```plaintext
${rand 1-100}
```

## Available Arugments

| Argument | Parameters | Usage |Description |
| -------- | ---------- | ----- | ----------- |
| 1>100 | N/A | `${1}` `${3}`| Gets the word at the specified index, returns `""` if nothing was found. |
| sender | N/A | `${sender}` | Gets the name of the person who used the command. |
| target - NYI | N/A | `${target}` | Use `${1}` for now. Validates the target mentioned exists. |
| rand | `100`, `50-100` | `${rand 100}` | Generates a random number up to the specified number, or between the range of `min-max`. Returns `""` if invalid. |
| rand.list | `('a' 'b')` | `${rand.list('Value 1' 'Value 2' 'Value 3')}` | Retrieves a random value from the specified list of values provided. Values must be enclosed in apostrophes (`'`) |
| count | Counter Variable | `${count cough}` | Gets the value of the counter, each time the counter is retrieved, it adds 1 to it.

The list of arguments is small and I get that, this was designed mainly to make adding simple dynamic commands easier. You can always make buttons that add commands that have complex functionality within SAMMI itself.

## Examples
Here are some practical examples of how you can use these arguments:

### Example 1: Random number
```plaintext
!command add cool ${sender} is ${rand 0-100}% cool!
```

**Output:** 
```plaintext
<USER> is 57% cool! 
```
### Example 2: Counter
```plaintext
!command add sneeze Streammer has sneezed ${count sneeze} times!
```

**Output:** 
```plaintext
Streamer has sneezed 31 times!
```
## Notes
- This system was designed to make simple dynamic commands easier to add and manage.
- For more advanced command logic, SAMMI itself provides additional functionality.

# Quotes

Not yet implemented.

# Announcements

Not yet implemented.

