# Settings
## SAMMI Settings
| Setting | Description |
|---------|-------------|
| Enable Advanced Commands | Enables some of the advanced extension commands I used to make this extension work, I figured I'd leave this in as an option incase people would like to use them. |
## Extension Module Settings
| Setting | Description |
|---------|-------------|
| Enable Commands| Enables the Command Module |
| Enable Quotes | Enables the Quote Module |
| Enable Announcements| Enables the Announcement Module |
| Backfill new Quotes | Lets new quotes replace the position of deleted quotes. |
| Quote Message | The message that gets sent when someone does `!quote` you can use `/$id$/`, `/$quote$/`, `/$category$/`, `/$user$/` and `/$timestamp$/`|
| Bridge Message Interval | The amount of time that has to pass before SAMMI sends message count to the bridge. This is just so SAMMI isn't spamming your bridge everytime a message is sent (It probably wont matter but I like to save on processing). (0) to disable. |
| Enable Death Counter | Enables the !death/+/-/s command |
| Enable Set Game Command | [MOD ONLY] Enables the !setgame command |
| Enable Set Title Command | [MOD ONLY] Enables the !settitle command |
| Enable Followage Command | Enables the !followage command |
| Enable Watch Time | Enables the counting of users watchtime. |
| Watch Time Interval | Default: 10 Minutes. How frequently watch time is calculated. Lower = more accurate but more processing.

# Basic Chat Commands

## Usage

Parameters wrapped in `( )` are optional and not needed. If they are not provided. They will target the person who used the command.

Paramaters wrapped in `{ }` are required and will not function if not provided.

| Operation | Usage | Description |
|-----------|-------|-------------|
| `Followage` | `!followage (user)` | Sends a chat message with how long the user has followed. |
| `Watch Time` | `!watchtime (user)` | Sends a chat message with how long a user has watched the stream for. Watch time is since you added the extension. |
| `Set Game` | `!setgame {game}` | [MOD ONLY] This command will update your game in Twitch and give an error message if it fails. |
| `Set Title` | `!settitle {title}` | [MOD ONLY] This command will update your stream title and gives an error message if it fails. |
| `Death` | `!deaths`<br>`!death+`<br>`!death-` | Sends a chat message with how many deaths are recorded in your set category<br>[MOD ONLY] Adds a death to the counter for your current category<br>[MOD ONLY] Removes a death from the counter for your current category. |

# Commands Module

SAMMI Starter Pack gives you access to a very handy moderator command that allows mods/yourself to add commands on the fly. You can edit/delete/disable these commands from the `Commands` tab in the bridge.

## Usage
Only Mods can add commands via chat. Commands parse most twitch commands, so be weary of that.

!command `<operation>` `<command>` `<response>`

| Operation | Usage |
|-----------|-------|
| `ADD` | `!command add <command> <response>` |
| `EDIT` | `!command edit <command> <new response>` |
| `RENAME` | `!command rename <command> <new name>` |
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
| target | `none`<br>`.game`<br>`.login` | `${target}`<br>`${target.game}`<br>`${target.login}` | Fetches stream information about the target. Returns `""` if target does not exist. Target is specically pulled from the first parameter following a command. If you use target on its own, it will pull the users display name. |
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
!cool
mxpuffin is 57% cool! 
```
### Example 2: Get Target information
```plaintext
!command add shoutout Please go follow ${target} they were last seen playing ${target.game} on their channel at twitch.tv/${target.login}
```

**Output**
```plaintext
!shoutout mxpuffin
Please go follow mxpuffin they were last seen playing <game> over at twitch.tv/mxpuffin
```
### Example 3: Counter
```plaintext
!command add sneeze Streammer has sneezed ${count sneeze} times!
```

**Output:** 
```plaintext
!sneeze
Streamer has sneezed 31 times!
```
## Notes
- This system was designed to make simple dynamic commands easier to add and manage.
- For more advanced command logic, SAMMI itself provides additional functionality.

# Quotes Module

SAMMI Starter Pack has a basic quote system that lets users add quotes. When a quote is added, it saves a unique counting ID, Timestamp, User who created the quote, category and the quote itself.

## Usage
| Operation | Usage | Description |
|-----------|-------|-------------|
| !quoteadd | !quoteadd `<quote>` | Adds the quote after the command |
| !quotedel | !quotedel `<quote id>` | [MOD] Removes the quote with the matching ID |
| !quote | !quote | Retrieves a random quote from the quote list |
| !quote `<id>` | `!quote 3`| Tries to get a quote by the matching ID |

## Settings

| Setting | Description |
|---------|-------------|
| Enable Quotes | Enables/Disables the quote system as a whole. |
| Backfill new Quotes | If you have quotes `1, 2, 3, 4` and delete quote `3` you'll end up with `1, 2, 4` with back fill enabled when adding a new quote, it will add the new quote at position `3` instead of position `5` |
| Quote Message | The message that gets sent when someone does `!quote` you can use `/$id$/`, `/$quote$/`, `/$category$/`, `/$user$/` and `/$timestamp$/`|

# Announcements Modules

SAMMI Starter Pack has a unique announcement system, similar to that of Stream Elements bot timers. You can add multiple groups which interact independantly of each other.

## Bridge UI 

| Field | Description |
|-------|-------------|
| Enabled | Whether or not this group is enabled, disabling will reset the timer, but it will remember the last message it sent. |
| Group Name | The name representing the group of responses. Each group has to have a unique name and will function independantly from other groups.
| Randomise Order | This will randomise the order that messages get sent. They will exhaust all other responses before repeating. |
| Responses | A list of responses that will be sent once both `Interval` and `Chat Lines` conditions are met. Responses are sent in the order they are shown unless `Randomise Order` is checked. |
| Trigger Button | If enabled, SAMMI will trigger a button that matches the Button ID of the Response Text instead of sending a chat message. This gives you flexibility to have more dynamic chat messages, alongside static messages. |
| ( X ) | Delete button for field its next to. You will be given a confirmation popup |
| ( + ) | Adds a new response field. It cannot be left blank. |

You must hit `SAVE` in order to confirm all these changes. If you refresh or click off the table row, it will close the drawer form and you will lose any information you have typed into fields, so be sure to hit `SAVE`


# SAMMI Extension Commands

Due to the nature of Extension Commands, you will be required to use `wait until variable exists` in order to get the results from outputs

## Other

### [SSP]: Send Message

Sends a chat message to both twitcn and YouTube. If you don't have a twitch or youtube account connected it won't try to send a message to that platform.

| Box Name | Type | Description |
|----------|------|-------------|
| Chat Message | String | The message you wish to be sent to each platform |
| Twitch Account | String | The Twitch account to send the message to (Leave blank for default) |
| YouTube Account | String | The YouTube account to send the message to (Leave blank for first added YT Account) |

### [SSP]: Get Valid Subscriber

Safetly gets the Subscription Status of a User and returns True or False if the user matches a criteria. You can check if the user is Tier 1, Tier 2 or Tier 3. You can do an exact match or a minimum match. Result is Cached so you're not making requests to Twitches API every check.

| Box Name | Type | Description |
|----------|------|-------------|
| User ID | String | The ID of the User you want to validate. |
| Tier | String | The Tier you want to check for. |
| Strict | Bool | If enabled, Users Tier must match exactly. |
| Output | String | The variable you wish to save the result to. |

## String Commands

### [SSP] Format: String to snake_case

Formats a string into snake_case (no spaces, all lowercase and no symbols)

| Box Name | Type | Description |
|----------|------|-------------|
| Input | String | The string you want to convert into snake_case |
| Output | String | The variable you wish to save the result to. |

### [SSP] Format: Seconds to String

Formats seconds into a readable string message. 

| Box Name | Type | Description |
|----------|------|-------------|
| Seconds | Number | The seconds you want to convert to a string variable|
| Is MS | Bool | Whether your input is in Milliseconds |
| Unit | String | `Long`: 2 Hours, 1 Minute, 20 Seconds.<br>`Short`: 2h, 1m, 20s. <br>`Time`: 02:01:20 (truncates days/weeks/months/years) |
| Output | String | The variable you wish to save the result to. |

### [SSP] Format: Number to String

Formats a number into a readable string message ie. `245000` becomes `245,000`

| Box Name | Type | Description |
|----------|------|-------------|
| Seconds | Number | The seconds you want to convert to a string variable|
| Separator | String | The character used to separate your number. |
| Output | String | The variable you wish to save the result to. |

## Cooldown Commands

### [SSP]: Get/Set Cooldown

Returns true or false if someone has a cooldown. If someone does not have a cooldown, it will automatically set a new cooldown. This command saves having to use 2 commands.

| Box Name | Type | Description |
|----------|------|-------------|
| User ID | Number/String | The User ID of the user you want to get the cooldown of. You could theorhetically use anything here, like `'global'` if you wanna apply a global cooldown|
| Group | String | The cooldown group, if empty, will use the current buttons ID |
| Duration | Number | The amount of time you want to set for the cooldown. |
| Time Unit | String | `Seconds` `Minutes` `Hours` `Days` |
| Output | String | The variable you wish to save the result to. |
| Output Seconds Left | Bool | Returns the amount of time remaining instead of true/false (returns 0 or negative numbers if cooldown is over) |


### [SSP]: Get Cooldown

Returns true if someone still has a cooldown. Returns false if the cooldown is over.

| Box Name | Type | Description |
|----------|------|-------------|
| User ID | Number/String | The User ID of the user you want to get the cooldown of. You could theorhetically use anything here, like `'global'` if you wanna apply a global cooldown|
| Group | String | The cooldown group, if empty, will use the current buttons ID |
| Output | String | The variable you wish to save the result to. |
| Output Seconds Left | Bool | Returns the amount of time remaining instead of true/false (returns 0 or negative numbers if cooldown is over) |

### [SSP]: Set Cooldown

Sets a cooldown to the specified user. It will set a cooldown regardless of if a user has a cooldown or not.

| Box Name | Type | Description |
|----------|------|-------------|
| User ID | Number/String | The User ID of the user you want to apply a cooldown to. You could theorhetically use anything here, like `'global'` if you wanna apply a global cooldown|
| Group | String | The cooldown group, if empty, will use the current buttons ID |
| Duration | Number | The amount of time you want to set for the cooldown. |
| Time Unit | String | `Seconds` `Minutes` `Hours` `Days` |

## Advanced Commands

### [SSP] CSV: Row to Object

Takes a row from a CSV and returns an Object with all the values with headers as keys. Returns undefined if an invalid row is provided.

| Box Name | Type | Description |
|----------|------|-------------|
| CSV Name | String | The name of a `loaded` CSV |
| CSV Path | String | The file path of the CSV, you can use the relative file path of SAMMIs directory (files/my_data.csv) |
| Row Name/Number | String/Number | Either the name of the row or number position. |
| Output | String | The variable you wish to save the result to. |

### [SSP] CSV: Parse to Array

Takes a CSV and returns an array with all the rows as an object. Will not return anything if the CSV doesnt exist.

| Box Name | Type | Description |
|----------|------|-------------|
| CSV Name | String | The name of a `loaded` CSV |
| CSV Path | String | The file path of the CSV, you can use the relative file path of SAMMIs directory (files/my_data.csv) |
| Output | String | The variable you wish to save the result to. |

The file path is required so SAMMI can cache the head of the CSV
