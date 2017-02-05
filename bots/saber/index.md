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

### In Development
+ Setup notification with custom message leading up to the start of an event
+ Sync with Google Calendar

[Invite to Discord](https://discordapp.com/api/oauth2/authorize?client_id=250801603630596100&scope=bot&permissions=0) | [Saber on GitHub](https://github.com/notem/Saber-Bot)

<div style="overflow:auto;"> 
<table>
  <thead>
    <th>Command</th>
    <th>Action</th>
    <th>Example</th>
  </thead>
  <tbody>
    <tr>
      <td>s!create</td>
      <td>Generates a new event entry and sends it to the specified schedule channel.</td>
      <td></td>
    </tr>
    <tr>
      <td>s!edit</td>
      <td>Modifies a schedule entry, either changing parameters or adding/removing comment fields.</td>
      <td>s!edit 129c start 10:30am</td>
    </tr>
    <tr>
      <td>s!destroy</td>
      <td>Removes an entry.</td>
      <td>s!destroy a902</td>
    </tr>
    <tr>
      <td>s/set</td>
      <td>Used to set channel-wide schedule settings.</td>
      <td>s/set msg "Announce message"</td>
    </tr>
    <tr>
      <td>s!timezones</td>
      <td>Shows all available timezones.</td>
      <td>s!timezones us</td>
    </tr>
    <tr>
      <td>s!setup</td>
      <td>Message the guide to preparing your a server for Saber</td>
      <td>s!setup</td>
    </tr>
    <tr>
      <td>s!help</td>
      <td>Messages the user the commands list and additional information.</td>
      <td>s!help destroy</td>
    </tr>
  </tbody>
</table>
</div>

### Server Setup

### Command Usage

### Sync'ing a Channel with a Google Calendar

1. Create a public calendar with Google Calendar. To set the calendar public, you should find a sharing setting near that looks something like this: [img]

2. (optional) If you already have a calendar setup, but not yet public, you can toggle the calendar's share settings in the 'Calendar settings'>>'Share this calendar tab' It should look something like this: [img]

3. Next, you'll need to find the calendar's public address.  The calendar's public address is listed near the end in the calendar's settings webpage under the 'Calendar details' tab. It should look something like this: [img] [img]

4. Finally, use the ``!sync [channel] [address]`` command in your discord server's saber_control channel to sync the events in your public calendar to the Saber schedule channel. [img]
