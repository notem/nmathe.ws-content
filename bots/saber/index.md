---
Title: Saber
Description: A Calendar/Schedule Manager Discord Bot
Hiding: 1
---

## Saber bot

### Features
+ Schedule events with a date, start time, end time, title, comments and repeat.
+ View scheduled events on schedule channels.
+ Organize events across multiple schedule channels.
+ Custom announcement messages on start/end of events (can be used to schedule other bot commands).
+ Set announcement message, channel to announce to, timezone and clock format per schedule channel.
+ Sync a schedule channel to a public Google Calendars calendar

### Roadmap
+ Improve sync to google calendar
+ Add optional reminders which send announcement messages before an event begins
+ Use a DB system as backend for storing the list of schedule entries
+ (When channel categories release) organize schedule channels under the 'Schedule' category
+ Dynamically sort entries in a channel w/ the top-most entry having the earliest start time
+ More options for custom messages
+ User experience improvements, and automated setup
+ Character limits on user input

[Invite to Discord](https://discordapp.com/api/oauth2/authorize?client_id=250801603630596100&scope=bot&permissions=76800) | [Saber on GitHub](https://github.com/notem/Saber-Bot) | [Support Server](https://discord.gg/NcmqF)

<div style="overflow:auto;"> 
<table>
  <thead>
    <th>Command</th>
    <th>Action</th>
  </thead>
  <tbody>
    <tr>
      <td>create</td>
      <td>Generates a new event entry and sends it to the specified schedule channel</td>
    </tr>
    <tr>
      <td>edit</td>
      <td>Modifies a schedule entry, either changing parameters or adding/removing comment fields</td>
    </tr>
    <tr>
      <td>destroy</td>
      <td>Used to delete events</td>
    </tr>
    <tr>
      <td>set</td>
      <td>Is used to configure the schedule settings for each channel</td>
    </tr>
    <tr>
      <td>timezones</td>
      <td>Shows all timezones that bot understands</td>
    </tr>
    <tr>
      <td>setup</td>
      <td>Provides a guide for preparing your server for use with Saber</td>
    </tr>
    <tr>
      <td>help</td>
      <td>Direct messages the user the list of commands as well as additional information</td>
    </tr>
    <tr>
      <td>sync</td>
      <td>Synchronize a schedule channel to a public Google Calendar</td>
    </tr>
  </tbody>
</table>
</div>

## User Docs

### Server Setup

Saber bot is designed to save events of schedule on dedicated "schedule channels." 

When Discord App implements categories for channels, any channel that is a part of a 'scheduling' category will be treated as a schedule channel. Until that day comes, Saber is configured to treat and channel whose name starts with "event_schedule" as a schedule channel.

Scheduling channels require saber be given some permissions, which should already have been requested if Saber joined your server using the above oath link.

In addition to schedule channels, Saber bot is configured to listen for scheduling commands only on a dedicated channel.  Create a channel with the name "saber_control," and allow Saber to view and send messages to it.

### Command Usage

Saber commands are of the form ``!command <arguments>``; an argument is any space separated, quotation enclosed phrase -- with the exception of single word phrases which may drop the quotations. 

Here's an example : ``!create #event_schedule "Rampage on Monday" 8:00am 9:00pm``. Saber will parse out four tokens from that command: ``#event_schedule``, ``Rampage on Monday``, ``8:00am``, and ``9:00pm``.

#### All Commands
For each of the following commands, \<text> denotes a required argument and [text] denotes optional arguments.

+ ``!create <#channel> <title> <start> <end> [date <mm/dd>|repeat <Su,Mo,Tu,We,Th,Fr,Sa>|<comment>]``
  
  Every new entry MUST be initialized with a title, a start time, and an end time.  Start and end times should be of form h:mm with optional am/pm appended on the end.
  
  Entries can optionally be configured with comments, event repeat settings, and/or to begin on a specific date.
  
  * Ex1. ``!create #event_schedule "Party in the Guild Hall" 19:00 2:00 date 04/10`` 
  * Ex2. ``!create "#event_channel Reminders" "Sign up for Raids" 4:00pm 4:00pm``
  * Ex3. ``!create "#event_channel Raids" "Weekly Raid Event" 7:00pm 12:00pm repeat "Fr,Sa" "Healers and tanks always in demand." "DM @RaidCaptain with your role and level if attending."``
  
+ ``!edit <id> <title|start|end|date|repeat|comment> <changes>``

  This command can be used to change any parameter of an event given the event's ID. The first argument is always the event ID, the second argument is the parameter you wish to change, and the third argument what the parameter should be changed to. 
  
  ``comment`` is the only exception to this rule.  When 'comment' is the second argument, the third argument needs to be either 'add' or 'remove', and the fourth argument should either be the new comment to add or the number of the comment to remove.
  
  * Ex1: ``!edit 3fa0 comment add "Attendance is mandatory"``
  * Ex2: ``!edit 0abf start 21:15``
  * Ex3: ``!edit 49af end 2:15pm``
  * Ex4: ``!edit 80c0 comment remove 1``
  
+ ``!destroy <id|all>``

  This command can be used to delete an event. Passing the event ID as the first argument will delete the individual event; passing the word 'all' will result in the deletion of every scheduled event on the server. **This command is likely to be revised soon**
  
+ ``!set <#channel> <msg|chan|zone|clock|style|sync> <new_config>``

  On every schedule channel the last message on the channel should contain a collection of configurable settings for the schedule. This command may be used to reconfigure those settings.  When changing a channel's settings, the displayed timers may be wiped.  Use the ``!init`` command as a temporary solution.
  
  * Ex1: ``!set msg "@here The event %t %a."``
  * Ex2: ``!set chan #general``
  * Ex3: ``!set clock 12``
  
+ ``!sync <#channel> <calendar address>``

  This command will replace all events in the specified channel with events imported from a public google calendar. Up to the next 7 days of events will be imported. To learn more, see the **Sync'ing a Channel with a Google Calendar** guide below.
  
  * Ex: ``!sync #schedule_entries g.rit.edu_g4elai703tm3p4iimp10g8heig@group.calendar.google.com``

+ ``!timezones [filter]``

  This command will output the list of all valid timezones that can be set with the ``set`` command. The raw output can be overwhelming. Output can be filtered by providing one argument to the command to filter for all zones which contain the word provided. For both our sakes, use a filter."
  
+ ``!help [command]``

  Direct messages the user a list of commands that can be used in Saber's dedicated control channel. If a command is supplied as the optional first argument, additional usage information for that command is provided.
  
+ ``!setup``

  The only purpose of this command is to direct message the user of the command a 'brief' walkthrough as to how to setup Saber bot.  **Likely to be removed soon**

### Sync'ing a Channel with a Google Calendar

1. Create a public calendar with Google Calendar. To set the calendar public, you should find a sharing setting near that looks something like this: 

 ![Make calendar public](%base_url%/saber/images/MakePublic.JPG)

2. (optional) If you already have a calendar setup, but not yet made it public, you can toggle the calendar's share settings in the 'Calendar settings'>>'Share this calendar tab' It should look something like this: 

 ![Change calendar share settings](%base_url%/saber/images/ChangeShareSettings.JPG)

3. Next, you'll need to find the calendar's public address.  The calendar's public address is listed near the end in the calendar's settings webpage under the 'Calendar details' tab. It should look something like this: 

 ![Location of calendar settings](%base_url%/saber/images/CalendarSettings.JPG)
  
 ![Your calendar's public address](%base_url%/saber/images/PublicAddress.JPG)

4. Finally, use the ``!sync [channel] [address]`` command in your discord server's saber_control channel to sync the events in your public calendar to the Saber schedule channel. 
  
  The timer is automatically setup to resync the channel to your calendar once every day. However, if changes are made to the Google Calendar the channel will not show such changes until resync. Either wait until auto-sync, or reuse the ``sync`` command.

5. If you wish to unsync the channel from your google calendar, use the ``set`` command (ex. ``!set sync off``).

### Channel Settings Options

<div style="overflow:auto;"> 
<table>
  <thead>
    <th>Setting</th>
    <th>Purpose</th>
    <th>Options</th>
  </thead>
  <tbody>
    <tr>
      <td>zone</td>
      <td>The timezone to use for events on the channel</td>
      <td>Use the timezones command</td>
    </tr>
    <tr>
      <td>msg</td>
      <td>The message that is announced on the start and end of an event</td>
      <td>The '%'character may be used to insert event specific text, see below.</td>
    </tr>
    <tr>
      <td>chan</td>
      <td>The channel to which announcement messages are sent</td>
      <td>The name of any channel. An invalid channel name will cause no announcement to be sent</td>
    </tr>
    <tr>
      <td>clock</td>
      <td>The hour format to display the start and end times of events</td>
      <td>For 12 hour format use '12', for 24 hour format use '24'</td>
    </tr>
    <tr>
      <td>style</td>
      <td>The style in which the events on the schedule are displayed</td>
      <td>The default is 'embed', use 'plain' if you'd rather use the legacy code-style.</td>
    </tr>
    <tr>
      <td>sync</td>
      <td>The Calendar address that the channel is set to sync too</td>
      <td>A valid address, anything else will result in 'off'</td>
    </tr>
  </tbody>
</table>
</div>

#### Setting Custom Announce Message
Every schedule channel is configured with it's own message to announce to a specified channel when an event begins or ends. With the ``set`` command the message can be configured.

Saber will announce the message string verbatum unless a '%' character is encountered.  When a '%' character is encountered, Saber will read the next character(s) and substitute the token with whatever value is associated that character combination.

**Suggestions / requests / complaints regarding this custom message system are very much welcome!**

| token | What is substituted in| Example msg : possible results
|----------:|----------:|-----:
| %t        | Title of event announced | ``@here Event: %t`` : ``@here Event: PoE Cut-throat League``
| %c``x``   | The ``x``th comment of the event | ``@everyone %c1`` : ``@everyone Dont forget to signup for our weekly raids!``
| %a        | ``begins`` or ``ends`` or `` `` | ``@here %t %a`` : ``@here PoE Cut-throat League begins``
