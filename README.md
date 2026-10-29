⚡ Streamer.bot Channel Reward Overlay Studio & OBS Reward Dock
![Streamer.bot](https://img.shields.io/badge/Streamer.bot-WebSocket%20Ready-10b981?style=for-the-badge&logo=twitch&logoColor=white)
![Platforms](https://img.shields.io/badge/Platforms-Twitch%20%26%20Kick-9146FF?style=for-the-badge)
![OBS Studio](https://img.shields.io/badge/OBS%20Studio-Overlay%20%26%20Custom%20Dock-302E31?style=for-the-badge&logo=obsstudio&logoColor=white)
![Zero Dependencies](https://img.shields.io/badge/Single--File-HTML5%20%2F%20JS-06b6d4?style=for-the-badge)
A complete, self-contained HTML5 suite powered by Streamer.bot WebSockets for managing and displaying Twitch and Kick Channel Point Rewards in OBS Studio.
This project consists of two tools that work together seamlessly:
🎨 OBS Channel Reward Overlay & Customizer Studio — Displays animated on-screen reward alerts, user avatars, and stacked countdown timers directly on your stream, and triggers automated Twitch/Kick chat announcements.
📋 OBS Studio Channel Reward Dock Dashboard — A compact, real-time streamer dashboard inside OBS Studio with Green Active Bubbles, Red Deactivated Bubbles, Idle Timer Effects, Activated Timestamps, and 1-Click Hover Dismiss controls.
---
📑 Table of Contents
✨ Overview: What Each Tool Does
1. OBS Channel Reward Overlay & Studio Customizer
2. OBS Studio Reward Dock Dashboard
⏱️ How Automatic Timer Detection Works
🚀 Complete Setup Guide
Step 1: Enable the Streamer.bot WebSocket Server
Step 2: Add Timer Codes to Your Twitch / Kick Rewards
Step 3: Add the Reward Dock to OBS Studio
Step 4: Customize & Export the OBS Stream Overlay
Step 5: Configure Automated Twitch & Kick Chat Messages
Step 6: (Optional) Custom C# Broadcast Script
🛠️ Troubleshooting
---
✨ Overview: What Each Tool Does
1. OBS Channel Reward Overlay & Studio Customizer
The Overlay Studio gives you a live 16:9 interactive preview canvas to design your on-screen channel point alerts and countdown timers, then exports a single ready-to-use HTML file for your OBS Browser Source.
Multi-Platform Support (Twitch & Kick): Automatically listens for `Twitch.RewardRedemption`, `Kick.RewardRedemption`, and custom Streamer.bot broadcasts.
Clear Visual Hierarchy:
Top: Channel Reward Title
Middle: Channel Reward Description & User Input
User Badge: Redeemer's Twitch or Kick Profile Picture, Username, and Platform Badge
Automatic Countdown Timers & Smart Stacking:
Scans the reward description for time codes like `(5:00)` or `(1:00:00)` and automatically spawns a live countdown card after/alongside the alert.
If multiple timed rewards are active at once, the newest timed reward automatically moves to the top of the timer stack.
600+ Built-In Visual & Audio Presets:
108+ In/Out Motion Effects (plus a 🎲 Random on Every Alert & Timer toggle)
108+ Alert Card Styles
108+ Timer Card Styles
108+ Master Display Layouts
108+ Alert Notification Sounds & 108+ Timer Completion Sounds (WebAudio synthesized — no external MP3 files required)
Flexible Screen Positioning & Timing:
Choose from 9 screen anchor positions (Top-Left, Top-Center, Top-Right, Middle-Left, Center, Middle-Right, Bottom-Left, Bottom-Center, Bottom-Right).
Set a Custom Alert Display Duration (e.g., `3s` to `600s`) with an optional visual countdown bar showing when the popup will disappear.
Automated Chat Messages via Streamer.bot Actions:
Select separate Streamer.bot Actions from a live dropdown for Twitch and Kick when a reward is Redeemed and when a Timer Finishes, passing formatted message arguments directly to Streamer.bot.
---
2. OBS Studio Reward Dock Dashboard
The OBS Reward Dock is a lightweight, compact dashboard designed specifically for OBS Custom Browser Docks so you never miss or lose track of redeemed channel rewards while streaming.
Bubble State	Visual Style	Behavior
🟢 Active (Timed Reward)	Glowing Green Bubble + Idle Effect	Plays a smooth breathing emerald glow & shimmer wave while counting down (`MM:SS` or `HH:MM:SS`). Automatically turns Red when the timer hits `00:00`.
🟢 Active (No Timer)	Glowing Green Bubble (`120s` Hold)	Stays Green at the top of the dock for 120 seconds (configurable) with a live `120s` countdown badge, then automatically turns Red.
🔴 Not Active (Expired / Dismissed)	Deactivated Red Bubble	Moves below all active Green rewards so active tasks always remain pinned to the top.
Key Dock Features:
Pinned Top Priority: Every new reward enters at the top of the dock and pushes older rewards down, keeping all Green Active Bubbles grouped at the top above Red Deactivated Bubbles.
Exact Activated Timestamp: Every card displays the exact time it was triggered (`🕒 5:25:14 PM`) alongside the platform badge (`TWITCH` / `KICK`), user avatar, username, reward title, and description.
Hover Dismiss (`Turn Red`): Hover your mouse over any active Green bubble and click `Dismiss • Turn Red` to immediately mark the reward as completed/inactive.
Hover Reactivate (`Turn Green`): Accidentally dismissed a reward? Hover over any Red bubble and click `Turn Green` to restart it, or click `✕` to remove it from the list.
Clean Startup: Starts completely empty on reload—no demo clutter—and includes a collapsible Settings / Test drawer for quick testing.
---
⏱️ How Automatic Timer Detection Works
Both the OBS Overlay and the OBS Dock automatically scan your channel reward's description (or title) for a time value inside parentheses `(...)`.
Time Code in Description	Meaning	Example Reward Description
`(MM:SS)`	Minutes : Seconds	`Play with no HUD and inverted mouse! (5:00)` $\rightarrow$ 5m 00s timer
`(HH:MM:SS)`	Hours : Minutes : Seconds	`Wear the banana suit on stream! (1:00:00)` $\rightarrow$ 1h 00m 00s timer
`(H:M:S)`	Shorthand Hours : Mins : Secs	`Speak in an accent! (1:0:0)` $\rightarrow$ 1h 00m 00s timer
No time code	Instant / Non-Timed Reward	`Hydrate and sit up straight!` $\rightarrow$ Shows alert (120s green hold in Dock)
---
🚀 Complete Setup Guide
Prerequisites
OBS Studio (v28 or newer recommended)
Streamer.bot (v0.2.x or v1.0+) connected to your Twitch and/or Kick account
---
Step 1: Enable the Streamer.bot WebSocket Server
Open Streamer.bot.
Navigate to the `Servers/Clients` tab $\rightarrow$ `WebSocket Server`.
Check `Auto Start WebSocket Server`.
Set Address to `127.0.0.1` and Port to `8080` (the default `ws://127.0.0.1:8080/`).
Ensure `Authentication` is unchecked (or localhost-accessible) and click `Start Server`.
---
Step 2: Add Timer Codes to Your Twitch / Kick Rewards
Open your Twitch Creator Dashboard (Viewer Rewards $\rightarrow$ Channel Points $\rightarrow$ Manage Rewards) or Kick Dashboard.
For any reward that should trigger a countdown timer, add the duration in parentheses at the end of the Reward Description:
5 Minutes: `Mute microphone for 5 minutes (5:00)`
90 Seconds: `Drop primary weapon right now (1:30)`
1 Hour: `Hardcore mode enabled (1:00:00)`
Rewards without parentheses will behave as standard alerts (and stay Green for `120s` in the OBS Dock before turning Red).
---
Step 3: Add the Reward Dock to OBS Studio
Save the dock HTML file (`index.html` or click Save Dock HTML inside the dock header to download `streamerbot-obs-reward-dock.html`) to a permanent folder on your PC (e.g., `C:\OBS-Overlays\streamerbot-obs-reward-dock.html`).
In OBS Studio, go to the top menu bar and click `Docks` $\rightarrow$ `Custom Browser Docks...`.
Under Dock Name, enter:
```text
   Channel Rewards
   ```
Under URL, enter the local file path (or click `...` if available):
```text
   file:///C:/OBS-Overlays/streamerbot-obs-reward-dock.html
   ```
Click `Apply`. The new dock window will open—drag and snap it anywhere into your OBS Studio layout!
(Optional) Click `Settings / Test` at the top of the dock if your Streamer.bot WebSocket uses a custom port or if you want to adjust the default `120s` green hold time.
---
Step 4: Customize & Export the OBS Stream Overlay
Open the Overlay Customizer Studio in your browser.
Position/WS Tab:
Choose your Screen Anchor Position (e.g., `Top Right`, `Bottom Right`).
Set your Alert Display Time (Seconds Before It Goes Away) (default: `6` seconds).
100+ Styles & 100+ Timers/Effects Tabs:
Select your favorite Master Layout, Alert Style, Timer Style, In/Out Animation (or enable 🎲 Random In/Out on Every Alert & Timer), Alert Sound, and Timer End Sound.
Click `Export OBS Overlay HTML` in the top bar to download `streamerbot-reward-overlay.html`.
In OBS Studio, under Sources, click `+` $\rightarrow$ `Browser`:
Check `Local file` and select your downloaded `streamerbot-reward-overlay.html`.
Set Width to `1920` and Height to `1080`.
Click `OK`.
---
Step 5: Configure Automated Twitch & Kick Chat Messages
The overlay can automatically announce in your Twitch or Kick chat when a reward is redeemed and when its timer finishes using native Streamer.bot Actions:
In Streamer.bot, create an Action (or two separate Actions) such as:
`Reward Redeemed Chat`
`Reward Timer Finished Chat`
Inside your Action, add a Sub-Action:
For Twitch: `Twitch` $\rightarrow$ `Chat` $\rightarrow$ `Send Message to Channel`
For Kick: `Kick` $\rightarrow$ `Chat` $\rightarrow$ `Send Message to Channel`
In the message box of that Sub-Action, enter `%chatMessage%` (or `%rewardMessage%` for the redeemed action / `%timerMessage%` for the timer finished action).
In the Overlay Studio under `Position/WS` $\rightarrow$ `Streamer.bot Chat Actions`:
Click `Refresh` to load your Streamer.bot actions list.
Select your actions in the dropdowns for Twitch and/or Kick.
Customize your message templates:
On Reward Redeemed: `{user} redeemed {reward} - {description}`
On Timer Finished: `{reward} Is Over After {duration}`
Available Arguments Passed to Streamer.bot `DoAction`:
Argument Variable	Description	Example Output
`%rewardMessage%`	Formatted "On Reward Redeemed" message	`KaiCenat redeemed No HUD - Play without HUD (5:00)`
`%timerMessage%`	Formatted "On Timer Finished" message	`No HUD Is Over After 5 Mins`
`%chatMessage%`	Always contains the active event's formatted message	(Matches either `%rewardMessage%` or `%timerMessage%`)
`%user%`	Username of the viewer who triggered the reward	`KaiCenat`
`%reward%`	Title of the channel reward	`No HUD`
`%description%`	Description + user input of the reward	`Play without HUD (5:00)`
`%duration%`	Human-readable timer length	`5 Mins`
`%platform%`	Platform where the reward was triggered	`twitch` or `kick`
---
Step 6: (Optional) Custom C# Broadcast Script
Both the Overlay and the Dock work out of the box with native Streamer.bot `Twitch.RewardRedemption` and `Kick.RewardRedemption` WebSocket events. However, if you want to trigger custom rewards from chat commands, bits, donations, or enrich user avatars server-side, you can add a `Execute C# Code` sub-action in Streamer.bot:
```csharp
using System;
using System.Text.RegularExpressions;
using Newtonsoft.Json;

public class CPHInline
{
    public bool Execute()
    {
        string platform = args.ContainsKey("broadcastPlatform") ? args["broadcastPlatform"].ToString() : "twitch";
        string user = args.ContainsKey("user") ? args["user"].ToString() : "Viewer";
        string userLogin = args.ContainsKey("userName") ? args["userName"].ToString() : user;
        string avatar = args.ContainsKey("targetUserProfileImageUrl") ? args["targetUserProfileImageUrl"].ToString() : "";
        string title = args.ContainsKey("rewardName") ? args["rewardName"].ToString() : "Channel Reward";
        string prompt = args.ContainsKey("rewardPrompt") ? args["rewardPrompt"].ToString() : "";
        string rawInput = args.ContainsKey("rawInput") ? args["rawInput"].ToString() : "";

        string description = !string.IsNullOrEmpty(prompt) && !string.IsNullOrEmpty(rawInput)
            ? $"{prompt} - {rawInput}"
            : (!string.IsNullOrEmpty(prompt) ? prompt : rawInput);

        int durationSeconds = 0;
        Match m = Regex.Match(description + " " + title, @"\(\s*(\d+)\s*:\s*(\d+)(?:\s*:\s*(\d+))?\s*\)");
        if (m.Success)
        {
            if (m.Groups[3].Success)
                durationSeconds = int.Parse(m.Groups[1].Value) * 3600 + int.Parse(m.Groups[2].Value) * 60 + int.Parse(m.Groups[3].Value);
            else
                durationSeconds = int.Parse(m.Groups[1].Value) * 60 + int.Parse(m.Groups[2].Value);
        }

        var payload = new
        {
            overlayType = "channelRewardAlert",
            platform = platform,
            user = user,
            userLogin = userLogin,
            avatar = avatar,
            title = title,
            description = description,
            durationSeconds = durationSeconds
        };

        CPH.WebsocketBroadcastJson(JsonConvert.SerializeObject(payload));
        return true;
    }
}
```
---
🛠️ Troubleshooting
WebSocket Status Shows `WS: Standby (127.0.0.1:8080)`:
Verify Streamer.bot is running and the WebSocket Server is started under `Servers/Clients -> WebSocket Server`.
If you changed your port in Streamer.bot, open `Settings / Test` in the Dock (or `Position/WS` in the Studio) and update the WebSocket URL to match your port.
No Audio in OBS Studio:
Right-click your Browser Source in OBS $\rightarrow$ `Properties` $\rightarrow$ check `Control audio via OBS`, then set Audio Monitoring to `Monitor and Output` in OBS Advanced Audio Properties.
Timer Did Not Start:
Make sure the reward description includes parentheses around the time format, such as `(5:00)` for 5 minutes or `(1:00:00)` for 1 hour.
