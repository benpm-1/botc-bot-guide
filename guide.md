# Blood on the Clocktower Bot Guide

## Setup

### Option 1 - Manual Setup

Before a manual setup, make sure to clear any previous game state with `/reset`.

For each player, use the `/setup` command to assign their role and position. They will be sent a DM with their role.
- `/setup [player] [role_name] [position]`

If the *Drunk/Lunatic/Marionette* is in play, make sure to use their **fake** role in `/setup`.


### Option 2 - Script Setup

Use the `/script` command to assign roles and positions randomly from a loaded script.
- `/script [script_name] [optional: forced_roles]`

The players for the game is everyone in the Town Square without the Storyteller role.
You can force any number of specific roles with `forced_roles`, this should be a comma separated list of role names (not case sensitive).
Each player will be sent a DM with their role. The seating positions will automatically appear in #game-chat.

**Note:** Do not force more role types than would normally be in a game. e.g. in an 8 player game, you can't force 2 outsiders.
If a role which modifies numbers of roles is chosen, this will be handled automatically. e.g. *Baron* will add extra outsiders.

If the *Sentinel* is on the script, it's effect will always happen.

## Grimoire
If using the *Script Setup* option, the grimoire will appear automatically in the #storyteller channel and will display any role modifiers.

if using the *Manual Setup* option, use `/grimoire` to send the grimoire to the #storyteller channel once setup is complete.

If a *Spy* or *Widow* is in play, you can forward the message containing the grimoire to that player. The forwarded message will not update, you can forward the grimoire again if necessary.

The grimoire displays the players in order of seating, along with:
- their alignment (blue circle for good, red square for evil)
- their role and role category (e.g. *Artist* (Townsfolk))
- their death status and ghost vote (Skull for dead, Ghost for remaining ghost vote)
- any current statuses (see below for more details)

`/status [player] [status]` is used to add a status to a player.
`/unstatus [player] [status]` is used to remove a status from a player.

The possible statuses are:
- `poisoned`
- `protected`
- `drunk`
- `mad`
- `lil_monsta` (for the player holding the *Lil' Monsta*)
- `banshee` (use instead of `/kill` if the Demon killed the *Banshee*)

`/realign [player]` is used to swap a player's alignment (Good -> Evil or Evil -> Good).

**Note:** The grimoire will update automatically to show any changes, you don't need to run `/grimoire` again.

## Night
Use `/night` to move players from the Town Square (or any Day voice channel) to private cottages.

Players can not see each other's cottages. Visit each player's cottage that requires it. If you need to simultaneously speak to multiple players in the night phase, drag and drop the players into the same channel.

## Day
Use `/day` to move players to the Town Square from their cottages.

If the Demon killed a player, use `/kill [player]` to mark them as Dead (unless *Banshee*). A message in #game-chat will tell everyone who died.

At the **start** of the day, use `/vote [minutes]` to set the vote timer. After *N* minutes has passed, all players will be moved back to the Town Square. Players will get a 10 second warning before moving.

### Nominations
In the nomination phase, if a player nominates, use `/nominate [nominee]` to nominate them.

A list of players appears in seating order, starting with the person next to the nominee. Their death status is displayed along with their ghost vote.

Players can vote or unvote freely until you click `Finalise Vote`. Advise players not to spam the `Vote / Unvote` button as this will likely cause lag for the voting.

To emulate going in a circle to lock in votes, you can say each players name so they stop voting.

**Note:** There is a small delay between a player voting and it appearing in Discord. If their vote changes just as you say their name, the vote was likely cast in time.

If a player is executed by the town, use `/kill [player]` to mark them as Dead.
If a player is resurrected by a Professor or other role, use `/resurrect [player]` to mark them as Alive.

When the game is over, use `/winner [team]` (team is Good or Evil) to declare the winner. This will display a message in #game-chat. A `Reveal Grimoire` button will appear that you can click to show all players the grimoire.

## Commands for all players
Before the start of a gaime, ensure that all players understand the commands they can use. 

The commands are:
- `/info [role_name]` - Get information about a role.
- `/positions` - Display the current seating order.
- `/showscript [script_name]` - Display the selected script, a link to the official script tool is provided.
- `/knock [room]` - Knock on a room. The players in that room can choose to let them enter or not. **Players should never enter an occupied room without using `/knock`**.
- `/import_script [script_url]` - Requests the import of a script. An admin must approve it before it is imported. Only urls from the [official script tool](https://script.bloodontheclocktower.com) are allowed.

## Known Issues & Bot Quirks
- Sometimes Discord will give an error when running commands. This is usually fixed by running the command again.
    - If the bot is performing lots of actions for a single command (e.g. moving players with `/night`) it will hit a rate limit and show an error. The command will continue after a couple of seconds however.
- For very small games/scripts, the *Baron* sometimes doesn't function. This likely extends to other Outsider adding roles.
- If *Lil' Monsta* is the only Demon on the script, the *Lunatic* will not be given a fake role.
- The bot will not decide the drunk *Village Idiot* automatically.
- The *Wraith* is very awkward to do in Discord and is probably worth avoiding.

## Untested role modifiers
These roles are accounted for in the bot, but have yet to be tested so could be buggy.
- *Legion*
- *Lord of Typhon*
- *Marionette*
- *Atheist*
- *Summoner*
- *Village Idiot*
