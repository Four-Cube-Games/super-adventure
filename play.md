---
layout: default
title: Play
description: Add Super Adventure to your Discord server, open the adventure with /activity, or ask to join the beta.
prose: true
permalink: /play/
---

# Play

Super Adventure is a Discord Activity: an adventure that opens inside Discord, on a computer, in a
browser or on a phone, where you walk your server's world tile by tile. It runs as two bots.
**Super Adventure** is the stable game, for any server. **Super Adventure (beta)** gets new features
first, and plays in one test server.

## Add Super Adventure to your server {#stable}

<p><a class="button" href="https://discord.com/oauth2/authorize?client_id={{ site.stable_client_id }}">Add to Discord</a></p>

1. **Check you can.** Adding a bot needs the *Manage Server* permission in that server. If you
   don't have it, send this page to someone who does.
2. **Press "Add to Discord"** and pick the server. The bot asks for four permissions: *View
   Channels*, *Send Messages*, *Embed Links* and *Attach Files*. It needs Attach Files to draw
   battles and maps, and the rest to post announcements. It never reads your messages. The
   Activity needs nothing more: Discord asks each player who opens it to let the game know who they
   are.
3. **Wait to be approved.** Every server is approved by hand while the game is young, so we know
   who's playing. Until then, the bot answers any command with a note that the server is waiting.
   The server's owner gets a direct message when the request arrives, and another with the answer.
4. **Play.** Once approved, anyone in the server types `/activity` in a channel, and the adventure
   opens right there. The first time, they choose a partner and set off. The
   [rules]({{ '/rules/' | relative_url }}) explain the rest.
{:.steps}

### Setting it up for your server

These need *Manage Server*. All of them are optional.

| Command | Does |
|---|---|
| `/announcements here` | posts the server's news in this channel |
| `/announcements level` | quiet, normal or chatty; `/announcements event` switches one kind on or off |
| `/timezone set` | when the day turns over; midnight UTC until you set it |
| `/pace set` | relaxed, standard, brisk or sprint: how many new stretches a day, and how long a season runs |

If a request is turned down, the owner is told why, and the bot leaves. You're welcome to ask
again later.

## Join the beta {#beta}

The beta is where new features land first: you'll play them before anyone else and tell us what's
wrong with them. It lives in one Discord server, and the beta bot can't be added anywhere else.

<div class="callout">Beta saves can be reset when a change needs it, with a warning first. They don't carry over to the stable game.</div>

To ask for a place, fill this in. It goes privately to Mark, not onto the public board. You'll get
an invite to the beta server, by email if you give one, or else a friend request on Discord.

<form class="request" action="{{ site.beta_form }}" method="POST">
  <input type="hidden" name="_subject" value="Beta access request">
  <label>Discord username
    <input name="discord" required autocomplete="off" placeholder="e.g. trainer_ada">
  </label>
  <label>Email <span>Optional. The invite goes here if you give one.</span>
    <input type="email" name="email" autocomplete="email">
  </label>
  <label>How did you find the game?
    <input name="found">
  </label>
  <label>Anything else? <span>What you'd like to test, the server you'd bring along, anything.</span>
    <textarea name="note" rows="4"></textarea>
  </label>
  <label class="trap">Leave this empty <input name="_gotcha" tabindex="-1" autocomplete="off"></label>
  <button class="button" type="submit">Ask to join</button>
</form>
