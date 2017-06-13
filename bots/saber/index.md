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
+ Users can RSVP to events

#### Roadmap
+ Bug Fixes and Patches
+ Feature Complete

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
    <tr>
      <td>!test</td>
      <td>Test an event's notification message</td>
    </tr>
    <tr>
      <td>!list</td>
      <td>View list of users who have rsvp'ed for an event</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### Quick Start

1. Invite Saber-Bot and create a channel named #saber_control

2. Use ``!init in #saber_control`` to create a schedule.
    * If a channel named #new_schedule is not created, give Saber-Bot Manage Channel permissions.
    
3. Use ``!config #new_schedule`` to view schedule settings

4. Use ``!zones [region/country]`` to view available timezone codes

5. Use ``!config #new_schedule zone [timezone]`` to configure the schedule's timezone

6. Use ``!create #new_schedule "Hi mom!" 5:45pm`` to create a new event
    * If no message appears in #new_schedule, check to insure Saber-Bot has read, write, and manage message perms
    
7. To delete the test schedule and event use !delete [schedule|eventID] |or delete the message/channel in discord  
   
Make use of !help, read the docs, or ask in the support server to learn more about the commands. I hope Saber fulfills your guild's scheduling needs!

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

+ ``!create <#channel> <title> <start> [<end> <option(s)>]``
  
  Every new entry MUST be initialized with a title and a starting time.  Start and end times should be of form h:mm with optional am/pm appended on the end (ex. ``10:20pm``). The ``<end>`` parameter may be ommitted to create an event which does not end at any particular time.
  
  Events can be created with a variety of extra options by adding specific keywords followed by a required value to the ``<option(s)>`` section. Comments are the only exception to the previous rule. Comments may be added to an event's description by simply appending quotation enclosed phrases to the end of the command (see examples). A list of ``<option>`` keywords can be found later in this document.
  
  * Ex1. ``!create #event_schedule "Party in the Guild Hall" 19:00 2:00 date 04/10`` 
  * Ex2. ``!create "#event_channel Reminders" "Sign up for Raids" 4:00pm``
  * Ex3. ``!create "#event_channel Raids" "Weekly Raid Event" 7:00pm 12:00pm repeat "Fr,Sa" "Healers and tanks always in demand." "DM @RaidCaptain with your role and level if attending."``
  <br />
  
+ ``!edit <id> <option> <changes>``

  This command can be used to change any parameter of an event given the event's ID. The first argument is always the event ID, the second argument should be the keyword for the parameter you wish to change, and the third argument is the new value. The edit command uses the same option keywords as the create command.
  
  ``comment`` is the only exception to this rule.  When 'comment' is the second argument, the third argument needs to be either ``add`` or ``remove`` (to denote the which action to take). The fourth argument should then either be the new comment to add or the number of the comment to remove.
  
  * Ex1: ``!edit 3fa0 comment add "Attendance is mandatory"``
  * Ex2: ``!edit 0abf start 21:15``
  * Ex3: ``!edit 49af end 2:15pm``
  * Ex4: ``!edit 80c0 comment remove 1``
   <br />
 
+ ``!delete <id|#channel|all>``

  This command can be used to delete an event or schedule. Passing the event ID as the first argument will delete the individual event, passing a channel mention to a schedule's channel will delete the schedule, and passing the word 'all' will result in the deletion of every scheduled event on the server.  This command is not necessary to safely delete events and schedules.  Guild administrators can delete the discord message or discord channel which represents the event or schedule to safely remove both.
  
    <br />

+ ``!config <#channel> <option> <new_config>``

  When only the first argument (#channel) is provided, the currently configured settings for that schedule is return. Those settings can be modified by issuing the settings name as the second argument and the new configuration as the third argument. The list of ``<option>`` keywords are detailed later in this documentation.
  
  * Ex1: ``!config #schedule msg "@here Event %a: %t"``
  * Ex2: ``!config #schedule chan general``
  * Ex3: ``!config #schedule clock 12``
  * Ex4: ``!config #schedule remind "30, 10, 5 min"``
  
    <br />

+ ``!sync <#schedule_channel> <calendar address>``

  This command will replace all events in the specified channel with events imported from a public google calendar. Up to the next 7 days of events will be imported. To learn more, see the **Synchronize a Schedule with Google Calendar** guide below. The schedule will re-import from the google calendar once per day automatically. While a schedule is synchronizing, the schedule can not be modified and new events may not be added.

  * Ex: ``!sync #schedule [. . .]``
  
  <br />

+ ``!zones <filter>``

  This command will output all timezones which match the provided filter. The filter is a character or string, any timezone whose name contains the the filter will be matched. The filter is required.
  
  * Ex: ``!zones us``
  
  <br />
  
+ ``!test <event_id>``

  The test command will send an test announcement for the event to the bot control channel. The announcement message format is controlled by the schedule to which the event belongs to, and can be changed using the config command.  
  
  <br />
 
+ ``!list <event_id>``

  The list command will show all users who have rsvp'ed for an event. The command takes a single argument which should be the ID of the event you wish query. The schedule holding the event must have 'rsvp' turned on in the configuration settings. RSVP can be enabled on a channel using the config command as followed, ``!config #channel rsvp on``
  
  <br />

+ ``!sort <#schedule_channel>``

  The sort command will re-sort the entries in a schedule. Entries are reordered so that the top event entry is the next event to begin. The schedule cannot be modified while in the process of sorting. Schedules with more than 10 entries will not be sorted.
  
  <br />

+ ``!help [command]``

  Direct messages the user a list of commands that can be used in Saber's dedicated control channel. If a command is supplied as the optional first argument, additional usage information for that command is provided. The information is <code>help</code> is likely to be more up-to-date than the documentation here.

<br>

### Synchronize with Google Calendar

1. Create a public calendar with Google Calendar. To set the calendar public, you should find a sharing setting near that looks something like this: 

 <br />
 <img src="%base_url%/assets/MakePublic.JPG" alt="Make calendar public" style="max-width:90%;">
 <br />

2. (optional) If you already have a calendar setup, but not yet made it public, you can toggle the calendar's share settings in the 'Calendar settings'>>'Share this calendar tab' It should look something like this: 
  
  <br />
  <img src="%base_url%/assets/ChangeShareSettings.JPG" alt="Change calendar share settings" style="max-width:90%;">
  <br />
  
3. Next, you'll need to find the calendar's public address.  The calendar's public address is listed near the end in the calendar's settings webpage under the 'Calendar details' tab. It should look something like this: 

 <br />
 <img src="%base_url%/assets/PublicAddress.JPG" alt="Your calendar's public address" style="max-width:90%;">
 <br />

4. Finally, use the ``!sync <#channel> <address>`` command in your discord server's saber_control channel to sync the events in your public calendar to the schedule. 
  
  The timer is automatically setup to resync the channel to your calendar once every day. However, if changes are made to the Google Calendar the channel will not show such changes until resync. Either wait until auto-sync, or reuse the ``sync`` command.
  
  <br />

5. If you wish to unsync the channel from your google calendar, use the ``config`` command (ex. ``!config #channel sync off``).

<br />

### Create and Edit Options

<div style="overflow:auto;"> 
<table>
  <thead>
    <th>Keyword</th>
    <th>Aliases</th>
    <th>Values</th>
  </thead>
  <tbody>
    <tr>
      <td>repeat</td>
      <td>r</td>
      <td>A comma separated list of days of week to repeat</td>
    </tr>
    <tr>
      <td>interval</td>
      <td>i</td>
      <td>A (reasonably sized) number</td>
    </tr>
    <tr>
      <td>date</td>
      <td>d</td>
      <td>A date in the format of yyyy/mm/dd</td>
    </tr>
    <tr>
      <td>start-date</td>
      <td>sd</td>
      <td>A date in the format of yyyy/mm/dd</td>
    </tr>
    <tr>
      <td>end-date</td>
      <td>ed</td>
      <td>A date in the format of yyyy/mm/dd</td>
    </tr>
    <tr>
      <td>url</td>
      <td>u</td>
      <td>The url address for the event message's title</td>
    </tr>
    <tr>
    <td><em>Edit Command Only</em></td>
    </tr>
    <tr>
      <td>title</td>
      <td>t</td>
      <td>The name given to the event</td>
    </tr>
    <tr>
      <td>start</td>
      <td>s</td>
      <td>The time of day the event begins, formatted as hh:mm</td>
    </tr>
    <tr>
      <td>end</td>
      <td>e</td>
      <td>The time of day the event ends, formatted as hh:mm</td>
    </tr>
    <tr>
      <td>comment</td>
      <td>c</td>
      <td>"add" or "remove" followed by the comment encapsulated in quotations.</td>
    </tr>
    <tr>
      <td>quiet-start</td>
      <td>qs</td>
      <td>No arguments. This silences the start announcement.</td>
    </tr>
    <tr>
      <td>quiet-end</td>
      <td>qs</td>
      <td>No arguments. This silences the end announcement.</td>
    </tr>
    <tr>
      <td>quiet-remind</td>
      <td>qs</td>
      <td>No arguments. This silences any reminders.</td>
    </tr>    
  </tbody>
</table>
</div>

### Schedule Config Options

<div style="overflow:auto;"> 
<table>
  <thead>
    <th>Keyword</th>
    <th>Aliases</th>
    <th>Values</th>
  </thead>
  <tbody>
    <tr>
      <td>Announcement Settings</td>
    </tr>
    <tr>
      <td>msg</td>
      <td>m</td>
      <td>A message format phrase</td>
    </tr>
    <tr>
      <td>chan</td>
      <td>ch</td>
      <td>The target channel for event announcements</td>
    </tr>
    <tr>
      <td>end-msg</td>
      <td>m</td>
      <td>A message format phrase. This overrides <code>msg</code> for end announcements.</td>
    </tr>
    <tr>
      <td>end-chan</td>
      <td>ch</td>
      <td>The target channel for event announcements. This overrides <code>chan</code> for end announcements.</td>
    </tr>
    <tr>
      <td>Reminder Settings</td>
    </tr>
    <tr>
      <td>remind</td>
      <td>r</td>
      <td>List of comma separated numbers</td>
    </tr>
    <tr>
      <td>remind-msg</td>
      <td>rm</td>
      <td>A message format phrase. This overrides <code>msg</code> for reminders.</td>
    </tr>
    <tr>
      <td>remind-chan</td>
      <td>rch</td>
      <td>The target channel for event reminders. This overrides <code>chan</code> for reminders.</td>
    </tr>
    <tr>
      <td>Miscellaneous Schedule Settings</td>
    </tr>
    <tr>
      <td>clock</td>
      <td>cl</td>
      <td>For 12 hour format use "12", for 24 hour format use "24"</td>
    </tr>
    <tr>
      <td>zone</td>
      <td>z</td>
      <td>A zone from !zones</td>
    </tr>  
    <tr>
      <td>rsvp</td>
      <td>rs</td>
      <td>Use "on" to enable rsvp, "off" to disable rsvp</td>
    </tr>
    <tr>
      <td>style</td>
      <td>st</td>
      <td>Use "full" for the full event display, "narrow" for a shortened display format.</td>
    </tr>  
    <tr>
      <td>sort</td>
      <td>so</td>
      <td>Use "asc" to auto-sort the entries in ascending order, "desc" for descending order, and "off" to disable auto-sort.</td>
    </tr> 
    <tr>
      <td>Schedule Sync Settings</td>
    </tr>
    <tr>
      <td>sync</td>
      <td>s</td>
      <td>A valid address, anything else will result in "off".</td>
    </tr>
    <tr>
      <td>time</td>
      <td>t</td>
      <td>The time of day to schedule Google Calendar sync.</td>
    </tr>
    <tr>
      <td>length</td>
      <td>l</td>
      <td>The number of days to sync from the Google Calendar</td>
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
      <td>%c[n]</td>
      <td>The [n]th comment of the event</td>
      <td><code>@everyone %c1</code> : <code>@everyone Dont forget to signup for our weekly raids!</code></td>
    </tr>
    <tr>
      <td>%a</td>
      <td>"begins [in x minutes]" or "ends [in x minutes]"</td>
      <td><code>@here %t %a</code> : <code>@here Raid practice begins in 5 minutes</code></td>
    </tr>
    <tr>
      <td>%b</td>
      <td>"begins" or "ends"</td>
      <td><code>@here %t %b</code> : <code>@here Raid practice begins</code></td>
    </tr>
    <tr>
      <td>%x</td>
      <td>"in [x] minutes"</td>
      <td><code>@here %t %x</code> : <code>@here Raid practice in 5 minutes</code></td>
    </tr>
  </tbody>
</table>
</div>

<br>

### Self-Hosting Saber Bot

1. Saber-bot has been developed using the Java 8 programming language. To run this application, you will need to download and install the [Java 8 runtime environment](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) for your system.

2. Saber-bot uses MongoDB to store the persistent event and schedule data. Install [the latest version of MongoDB](https://docs.mongodb.com/manual/installation/) on your system. I suggest you setup MongoDB to run on system startup as well.

3. With the prequisite software installed, you should now be able to launch the bot application. Download the latest version of the bot from [here](https://drive.google.com/drive/folders/0B0zQK1JmyZGJdVdFQ1IxUi1haXc?usp=sharing), or compile from the bot from source using Maven. 

4. Running the .jar file for the first time should cause the application to generate a fresh configuration file and close. Add your discord bot token and your discord user ID to the configuration file and restart the bot. 

5. To have Google Calendar integration, you need to generate new credentials on the [Google Developer Console](https://console.developers.google.com/apis/credentials). Generate a new 'service account key' and download the key as a JSON file type. Modify the configuration file's 'google_service_key' settings to indicate the location of your service key file.

Documentation last updated: 2017-06-13
