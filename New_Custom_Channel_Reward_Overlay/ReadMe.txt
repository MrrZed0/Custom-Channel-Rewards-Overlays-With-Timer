REWARD STUDIO — Twitch & Kick channel reward overlay for Streamer.bot
=====================================================================

TIMERS
  Put the duration in brackets at the END of the channel reward
  description in Twitch or Kick:

      Turn off your crosshair for the round (5:00)

      (0:30)     30 seconds
      (5:00)     5 minutes
      (1:00:00)  1 hour
      (1:30:00)  1 hour 30 minutes

  No tag = alert only, no countdown.
  The countdown is named after the reward and plays your chosen
  alarm sound when it hits 00:00.

FILES
  customizer.html  Open in a browser to design the look, then press
                   "Export Overlay" to download the OBS file.
  overlay.html     The OBS browser source. Add it in OBS as
                   Browser Source -> Local file, 1920 x 1080.

STREAMER.BOT SETUP (3 steps, no C# required)
  1. Servers/Clients -> WebSocket Server -> enable on 127.0.0.1:8080
  2. Make 4 Actions, each with one sub-action
     Twitch/Kick -> Chat -> Send Message to Channel
     Message text: %rewardMessage%   (on redeemed)
                   %timerMessage%    (on timer finished)
  3. Pick those Actions on the Connect tab, then export the overlay.

KEYBOARD SHORTCUTS (in customizer.html)
  Space     preview the current alert
  R         randomize every style
  Ctrl+Z    undo the last randomize
  E         export the OBS overlay
  S         saved presets
  C         clear running timers
  1-7       switch tabs
  ?         help panel
