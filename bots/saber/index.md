---
Title: Saber
Description: A Calendar/Schedule Manager Discord Bot
Hiding: 1
---

## Saber bot

[Invite to Discord](https://discordapp.com/api/oauth2/authorize?client_id=250801603630596100&scope=bot&permissions=76800) | [Saber on GitHub](https://github.com/notem/Saber-Bot) | [Get Support](https://discord.gg/NcmqF)

#### Features
+ Display events on dedicated schedule channels.
+ Send announcements when event begins / ends.
+ Send reminders before an event begins.
+ Configure timezone per schedule.
+ Sync schedules to Google Calendars

#### Roadmap
+ Improved user experience
+ Auto-sort entries

#### Command Overview
<div style="overflow:auto;"> 
<table>
  <thead>
    <th>Command</th>
    <th>Action</th>
  </thead>
  <tbody>
      <tr>
      <td>!init</td>
      <td>Initializes a new schedule</td>
    </tr>
    <tr>
      <td>!create</td>
      <td>Adds a new event entry to the specified schedule</td>
    </tr>
    <tr>
      <td>!edit</td>
      <td>Modifies a scheduled event with a new configuration</td>
    </tr>
    <tr>
      <td>!delete</td>
      <td>Used to delete events and schedules</td>
    </tr>
    <tr>
      <td>!config</td>
      <td>May be used to show a schedule's settings and change those settings</td>
    </tr>
    <tr>
      <td>!zones</td>
      <td>Shows all timezones that the bot understands</td>
    </tr>
    <tr>
      <td>!help</td>
      <td>Direct messages the user the list of commands as well as additional information</td>
    </tr>
    <tr>
      <td>!sync</td>
      <td>Sync a schedule to load events from a Google Calendar</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### Quick Start

1. Invite Saber-Bot and create a channel named #saber_control
  </br>
2. Use ``!init in #saber_control`` to create a schedule.
    * If a channel named #new_schedule is not created, give Saber-Bot Manage Channel permissions.
      </br>
3. Use ``!config #new_schedule`` to view schedule settings
  </br>
4. Use ``!zones [region/country]`` to view available timezone codes
  </br>
5. Use ``!config #new_schedule zone [timezone]`` to configure the schedule's timezone
  </br>
6. Use ``!create #new_schedule "Hi mom!" 5:45pm`` to create a new event
    * If no message appears in #new_schedule, check to insure Saber-Bot has read, write, and manage message perms
      </br>
7. To delete the test schedule and event use !delete [schedule|eventID] |or delete the message/channel in discord  
  </br>

Make use of !help, read the docs, or ask in the support server to learn more about the commands. I hope Saber fulfills your scheduling guild's needs!

<br>

### Server Setup

Saber bot is designed to save events of schedule on dedicated "schedule channels." 

Scheduling channels require Saber be given some permissions, which should already have been requested if Saber joined your server using the above oath link.  Insure that Saber has the Manage Channels permission and the ability to read/write on any channel you plan to have her announce on.

In addition to schedule channels, Saber bot is configured to listen for scheduling commands only on a dedicated channel.  Create a channel with the name "saber_control," and allow Saber to view and send messages to it.

<br>

### Commands

Saber commands are of the form ``!command <arguments>``; an argument is any space separated, quotation enclosed phrase -- with the exception of single word phrases which may drop the quotations. 

Here's an example : ``!create #event_schedule "Rampage on Monday" 8:00am 9:00pm``. Saber will parse out four tokens from that command: ``#event_schedule``, ``Rampage on Monday``, ``8:00am``, and ``9:00pm``.

For each of the following commands, ``<argument>`` denotes an argument and ``[argument(s)]`` denotes optional arguments.
<br />

+ ``!create <#channel> <title> <start> [<end>|date <mm/dd>|repeat <Su,Mo,Tu,We,Th,Fr,Sa>|<comment>]``
  
  Every new entry MUST be initialized with a title and a starting time.  Start and end times should be of form h:mm with optional am/pm appended on the end (ex. ``10:20pm``).
  
  Entries can optionally be configured with comments, event repeat settings, and/or to begin on a specific date.
  
  * Ex1. ``!create #event_schedule "Party in the Guild Hall" 19:00 2:00 date 04/10`` 
  * Ex2. ``!create "#event_channel Reminders" "Sign up for Raids" 4:00pm``
  * Ex3. ``!create "#event_channel Raids" "Weekly Raid Event" 7:00pm 12:00pm repeat "Fr,Sa" "Healers and tanks always in demand." "DM @RaidCaptain with your role and level if attending."``
  <br />
  
+ ``!edit <id> <title|start|end|date|repeat|comment> <changes>``

  This command can be used to change any parameter of an event given the event's ID. The first argument is always the event ID, the second argument is the parameter you wish to change, and the third argument what the parameter should be changed to. 
  
  ``comment`` is the only exception to this rule.  When 'comment' is the second argument, the third argument needs to be either ``add`` or ``remove`` (to denote the which action to take). The fourth argument should then either be the new comment to add or the number of the comment to remove.
  
  * Ex1: ``!edit 3fa0 comment add "Attendance is mandatory"``
  * Ex2: ``!edit 0abf start 21:15``
  * Ex3: ``!edit 49af end 2:15pm``
  * Ex4: ``!edit 80c0 comment remove 1``
   <br />
 
+ ``!delete <id|#channel|all>``

  This command can be used to delete an event or schedule. Passing the event ID as the first argument will delete the individual event, passing a channel mention to a schedule's channel will delete the schedule, and passing the word 'all' will result in the deletion of every scheduled event on the server.  This command is not necessary to safely delete events and schedules.  Guild administrators can delete the discord message or discord channel which represents the event or schedule to safely remove both.
    <br />

+ ``!config <#channel> <msg|chan|zone|clock|style|sync|remind> <new_config>``

  When only the first argument (#channel) is provided, the currently configured settings for that schedule is return. Those settings can be modified by issuing the settings name as the second argument and the new configuration as the third argument.
  
  * Ex1: ``!config #schedule msg "@here Event %a: %t"``
  * Ex2: ``!config #schedule chan general``
  * Ex3: ``!config #schedule clock 12``
  * Ex4: ``!config #schedule remind "30, 10, 5 min"``
    <br />

+ ``!sync <#channel> <calendar address>``

  This command will replace all events in the specified channel with events imported from a public google calendar. Up to the next 7 days of events will be imported. To learn more, see the **Synchronize a Schedule with Google Calendar** guide below. The schedule will re-import from the google calendar once per day automatically.

  * Ex: ``!sync #schedule [. . .]``
  <br />

+ ``!zones <filter>``

  This command will output all timezones which match the provided filter. The filter is a character or string, any timezone whose name contains the the filter will be matched. The filter is required.
  
  * Ex: ``!zones us``
  
  <br />

+ ``!help [command]``

  Direct messages the user a list of commands that can be used in Saber's dedicated control channel. If a command is supplied as the optional first argument, additional usage information for that command is provided.

<br>

### Synchronize with Google Calendar

1. Create a public calendar with Google Calendar. To set the calendar public, you should find a sharing setting near that looks something like this: 

 <br />
 <img src="https://nmathe.ws/assets/MakePublic.JPG" alt="Make calendar public" style="max-width:80%;">
 <br />

2. (optional) If you already have a calendar setup, but not yet made it public, you can toggle the calendar's share settings in the 'Calendar settings'>>'Share this calendar tab' It should look something like this: 
  
  <br />
  ![Change calendar share settings](%base_url%/assets/ChangeShareSettings.JPG)
  <br />
  
3. Next, you'll need to find the calendar's public address.  The calendar's public address is listed near the end in the calendar's settings webpage under the 'Calendar details' tab. It should look something like this: 

 <br />
 <img src="https://nmathe.ws/assets/PublicAddress.JPG" alt="Your calendar's public address" style="max-width:80%;">
 <br />

4. Finally, use the ``!sync <#channel> <address>`` command in your discord server's saber_control channel to sync the events in your public calendar to the schedule. 
  
  The timer is automatically setup to resync the channel to your calendar once every day. However, if changes are made to the Google Calendar the channel will not show such changes until resync. Either wait until auto-sync, or reuse the ``sync`` command.
  
  <br />

5. If you wish to unsync the channel from your google calendar, use the ``config`` command (ex. ``!config #channel sync off``).

<br />

### Schedule Config Options

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

<br>

#### Setting a Custom Announcement Message
Every schedule channel is configured with it's own message to announce to a specified channel when an event begins or ends. With the ``config`` command the message can be configured.

Saber will announce the message string verbatum unless a '%' character is encountered.  When a '%' character is encountered, Saber will read the next character(s) and substitute the token with whatever value is associated that character combination.

<div style="overflow:auto;"> 
<table>
  <thead>
    <th>% token</th>
    <th>Text Substituted in</th>
    <th>Example msg : Possible Results</th>
  </thead>
  <tbody>
    <tr>
      <td>%t</td>
      <td>Title of event announced</td>
      <td><code>@here Event: %t</code> : <code>@here Event: PoE Cut-throat League</code></td>
    </tr>
    <tr>
      <td>%c[x]</td>
      <td>The [x]th comment of the event</td>
      <td><code>@everyone %c1</code> : <code>@everyone Dont forget to signup for our weekly raids!</code></td>
    </tr>
    <tr>
      <td>%a</td>
      <td>"begins [in x minutes]" or "ends [in x minutes]"</td>
      <td><code>@here %t %a</code> : <code>@here Raid practice begins in 5 minutes</code></td>
    </tr>
  </tbody>
</table>
</div>
