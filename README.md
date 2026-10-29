<div align="center">

# ⚡ Streamer.bot Channel Reward Overlay Studio & OBS Reward Dock

[![Streamer.bot](https://img.shields.io/badge/Streamer.bot-WebSocket_Ready-10b981?style=for-the-badge&logo=twitch&logoColor=white)](https://streamer.bot/)
[![Platforms](https://img.shields.io/badge/Platforms-Twitch_%26_Kick-9146FF?style=for-the-badge)](https://twitch.tv/)
[![OBS Studio](https://img.shields.io/badge/OBS_Studio-Overlay_%26_Custom_Dock-302E31?style=for-the-badge&logo=obsstudio&logoColor=white)](https://obsproject.com/)
[![License](https://img.shields.io/badge/Single--File-HTML5_%2F_JS-06b6d4?style=for-the-badge)](#)

**A self-contained HTML5 suite powered by Streamer.bot WebSockets for displaying, tracking, and managing Twitch & Kick Channel Point Rewards inside OBS Studio.**

[✨ Features](#-what-this-suite-does) • [⏱️ Timer Syntax](#️-automatic-timer-syntax) • [🚀 Setup Guide](#-how-to-set-up-step-by-step) • [💬 Chat Actions](#-setting-up-automated-chat-messages) • [🛠️ Troubleshooting](#️-troubleshooting)

![https://github.com/MrrZed0/Alerts_All_Platforms/blob/main/Preview.png](https://github.com/MrrZed0/Custom-Channel-Rewards-Overlays-With-Timer/blob/main/1.png?raw=true)
![https://github.com/MrrZed0/Alerts_All_Platforms/blob/main/Preview.png](https://github.com/MrrZed0/Custom-Channel-Rewards-Overlays-With-Timer/blob/main/2.png?raw=true)


</div>

---

> [!NOTE]
> Both the **OBS Stream Overlay** and the **OBS Studio Dock Dashboard** are single-file `.html` applications with **zero external dependencies**. They connect directly to your local Streamer.bot WebSocket server (`ws://127.0.0.1:8080/`).

---

## ✨ What This Suite Does

This repository includes two tools designed to work together during your live streams:

### 1. 🎨 OBS Channel Reward Overlay & Customizer Studio
The **Overlay Studio** provides a live 16:9 interactive preview stage to customize your on-screen channel point alerts and countdown timers, and exports a single HTML file for your OBS Browser Source.

- [x] **Twitch & Kick Support**: Listens to `Twitch.RewardRedemption`, `Kick.RewardRedemption`, and custom Streamer.bot broadcasts.
- [x] **Clear Reward Hierarchy**:
  - **Top**: Channel Reward Title
  - **Under Title**: Channel Reward Description & Viewer Input
  - **User Profile**: Redeemer's Twitch or Kick Profile Picture, Username, and Platform Badge
- [x] **Automatic Countdown Timers & Top-Stacking**:
  - Automatically scans reward descriptions for time codes like `(5:00)` or `(1:00:00)` and spawns a live countdown card.
  - When multiple timed rewards are active, **the newest timed reward automatically moves to the top of the stack**.
- [x] **600+ Built-In Presets**:
  - **108+ In/Out Motion Effects** (with a **Random on Every Alert & Timer** toggle)
  - **108+ Alert Card Styles** & **108+ Timer Card Styles**
  - **108+ Master Display Layouts**
  - **108+ Alert Sounds** & **108+ Timer Completion Sounds** (built-in WebAudio synthesizer)
- [x] **9-Point Screen Positioning & Custom Alert Duration**:
  - Anchor alerts to any corner, edge, or center of the screen.
  - Set a custom **Alert Display Duration** (`1s` to `600s`) before the alert animates away.
- [x] **Native Streamer.bot Chat Announcements**:
  - Triggers your chosen Streamer.bot Actions for **Twitch** and **Kick** when a reward is redeemed and when a timer finishes.

---

### 2. 📋 OBS Studio Channel Reward Dock Dashboard
The **OBS Reward Dock** (`index.html`) is a compact dashboard built for **OBS Custom Browser Docks** so you can track active, timed, and completed channel rewards in real time.

| Bubble State | Visual Appearance | How It Works |
| :--- | :--- | :--- |
| **🟢 Active (Timed)** | **Green Bubble + Idle Effect** | Displays a breathing emerald glow and shimmer animation while counting down (`MM:SS` or `HH:MM:SS`). Automatically turns **Red** when the timer reaches `00:00`. |
| **🟢 Active (No Timer)** | **Green Bubble (`120s` Hold)** | Stays **Green** at the top of the dock for **120 seconds** with a live countdown badge, then automatically turns **Red**. |
| **🔴 Not Active** | **Red Deactivated Bubble** | Expired or manually dismissed rewards turn **Red** and move below all active Green bubbles. |

#### Key Dock Highlights:
* **Top-Priority Sorting**: New rewards always insert at the top and push older rewards down, keeping all **Green Active Bubbles** grouped at the top above **Red Deactivated Bubbles**.
* **Activated Timestamp**: Every card displays the exact time it was triggered (e.g., `5:25:14 PM`) next to the viewer's username, avatar, and platform badge.
* **Hover to Dismiss (`Turn Red`)**: Hover your mouse over any active Green bubble and click <kbd>Dismiss • Turn Red</kbd> to immediately mark it as completed/not active.
* **Hover to Reactivate (`Turn Green`)**: Hover over any Red bubble and click <kbd>Turn Green</kbd> to restart it, or click <kbd>✕</kbd> to remove it from the dock.
* **Compact Layout & Clean Startup**: Designed with compact cards to fit narrow OBS docks and loads with a clean empty state on every startup.

---

## ⏱️ Automatic Timer Syntax

Both the **Overlay** and the **Dock** scan the end of your channel reward description (or title) for a time value inside parentheses `(...)`:

| Format in Description | Duration Parsed | Example Channel Reward Description |
| :---: | :---: | :--- |
| `(MM:SS)` | **Minutes : Seconds** | `Play with no HUD and inverted mouse! (5:00)` |
| `(HH:MM:SS)` | **Hours : Minutes : Seconds** | `Wear the banana suit on stream! (1:00:00)` |
| `(H:M:S)` | **Hours : Minutes : Seconds** | `Speak in an accent! (1:0:0)` |
| *(No parentheses)* | **No Timer (Instant Alert)** | `Hydrate and posture check!` |

> [!TIP]
> If a reward has **no timer code** in its description, the Stream Overlay shows the popup alert for your custom display duration, while the OBS Dock keeps the reward in a **Green Bubble for 120 seconds** before automatically turning it **Red**.

---

## 🚀 How to Set Up (Step-by-Step)

### Step 1: Enable the Streamer.bot WebSocket Server
1. Open **Streamer.bot**.
2. Go to <kbd>Servers/Clients</kbd> $\rightarrow$ <kbd>WebSocket Server</kbd>.
3. Check **Auto Start WebSocket Server**.
4. Set **Address** to `127.0.0.1` and **Port** to `8080`.
5. Leave **Authentication** unchecked (for local OBS connections) and click <kbd>Start Server</kbd>.

---

### Step 2: Add Timer Codes to Your Twitch or Kick Rewards
1. Open your **Twitch Creator Dashboard** (<kbd>Viewer Rewards</kbd> $\rightarrow$ <kbd>Channel Points</kbd> $\rightarrow$ <kbd>Manage Rewards</kbd>) or **Kick Dashboard**.
2. Edit any reward that needs a countdown timer and add `(MM:SS)` or `(HH:MM:SS)` to the end of its **Description**:
   ```text
   Mute my mic for 5 minutes! (5:00)
   ```

---

### Step 3: Add the Reward Dock to OBS Studio
1. Save `index.html` (or click <kbd>Save Dock HTML</kbd> in the dock header to save `streamerbot-obs-reward-dock.html`) to a folder on your PC, for example:
   ```text
   C:\OBS-Overlays\streamerbot-obs-reward-dock.html
   ```
2. Open **OBS Studio** and click <kbd>Docks</kbd> $\rightarrow$ <kbd>Custom Browser Docks...</kbd> in the top menu bar.
3. Add a new row with the following details:
   * **Dock Name**: `Channel Rewards`
   * **URL**: `file:///C:/OBS-Overlays/streamerbot-obs-reward-dock.html`
4. Click <kbd>Apply</kbd> and dock the panel anywhere inside your OBS workspace.

> [!IMPORTANT]
> Make sure to use forward slashes `/` in the `file:///` URL inside OBS Custom Browser Docks, or select the local file directly if your version of OBS includes the file browse button.

---

### Step 4: Customize & Add the OBS Stream Overlay
1. Open the **Overlay Customizer Studio** in your browser.
2. Under the <kbd>Position/WS</kbd> tab:
   * Select your **Screen Position** (e.g., `Top Right` or `Bottom Right`).
   * Set **Alert Display Time (Before It Goes Away)** in seconds.
3. Under <kbd>100+ Styles</kbd> and <kbd>100+ Timers & Effects</kbd>:
   * Choose your **Master Layout**, **Alert Style**, **Timer Style**, **In/Out Motion Effect** (or enable **Random In/Out on Every Alert & Timer**), and **Sounds**.
4. Click <kbd>Export OBS Overlay HTML</kbd> in the top bar to download `streamerbot-reward-overlay.html`.
5. In **OBS Studio**, go to **Sources** $\rightarrow$ click <kbd>+</kbd> $\rightarrow$ <kbd>Browser</kbd>:
   * Check **Local file** and select `streamerbot-reward-overlay.html`.
   * Set **Width**: `1920` and **Height**: `1080`.
   * Click <kbd>OK</kbd>.

---

## 💬 Setting Up Automated Chat Messages

The overlay triggers native **Streamer.bot Actions** when a reward is redeemed and when its countdown timer finishes:

1. In **Streamer.bot**, create two Actions (or one shared Action):
   * `Reward Redeemed Chat`
   * `Reward Timer Finished Chat`
2. Add a Sub-Action inside each Action:
   * **Twitch**: <kbd>Twitch</kbd> $\rightarrow$ <kbd>Chat</kbd> $\rightarrow$ <kbd>Send Message to Channel</kbd>
   * **Kick**: <kbd>Kick</kbd> $\rightarrow$ <kbd>Chat</kbd> $\rightarrow$ <kbd>Send Message to Channel</kbd>
3. Set the message text in the Sub-Action to `%chatMessage%` (or `%rewardMessage%` / `%timerMessage%`).
4. In the **Overlay Studio** (<kbd>Position/WS</kbd> tab), click <kbd>Refresh</kbd> next to **Streamer.bot Chat Actions** and select your Actions from the dropdowns for:
   * **Twitch • On Reward Redeemed Action**
   * **Twitch • On Timer Finished Action**
   * **Kick • On Reward Redeemed Action**
   * **Kick • On Timer Finished Action**

### Arguments Sent to Your Streamer.bot Action (`args`)

| Argument Variable | Description | Example Value |
| :--- | :--- | :--- |
| `%rewardMessage%` | Formatted message when the reward is triggered | `KaiCenat redeemed No HUD - Play without HUD (5:00)` |
| `%timerMessage%` | Formatted message when the countdown ends | `No HUD Is Over After 5 Mins` |
| `%chatMessage%` | Always populated with the active message | Matches `%rewardMessage%` or `%timerMessage%` |
| `%user%` | Username of the viewer who redeemed the reward | `KaiCenat` |
| `%reward%` | Name of the channel reward | `No HUD` |
| `%description%` | Description + user input of the reward | `Play without HUD (5:00)` |
| `%duration%` | Human-readable timer duration | `5 Mins` |
| `%platform%` | Platform identifier | `twitch` or `kick` |

---

<details>
<summary><b>💻 Optional: Custom C# Broadcast Script for Streamer.bot (Click to Expand)</b></summary>

<br>

Both the Overlay and the Dock work automatically with native `Twitch.RewardRedemption` and `Kick.RewardRedemption` WebSocket events. If you also want to trigger rewards from chat commands, bits, or custom triggers, add an <kbd>Execute C# Code</kbd> Sub-Action in Streamer.bot with the following code:

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

</details>

---

## 🛠️ Troubleshooting

<details>
<summary><b>Why does the status say <code>WS: Standby (127.0.0.1:8080)</code>?</b></summary>

* Make sure **Streamer.bot** is open and the WebSocket Server is running under <kbd>Servers/Clients</kbd> $\rightarrow$ <kbd>WebSocket Server</kbd>.
* If you use a port other than `8080`, click <kbd>Settings / Test</kbd> in the Dock (or <kbd>Position/WS</kbd> in the Studio), enter your custom `ws://127.0.0.1:PORT/` address, and click <kbd>Connect</kbd>.
</details>

<details>
<summary><b>Why can't I hear the alert or timer sounds in OBS Studio?</b></summary>

* Right-click your **Browser Source** in OBS Studio $\rightarrow$ <kbd>Properties</kbd> $\rightarrow$ check **Control audio via OBS**.
* Open **Advanced Audio Properties** in OBS and set the Browser Source's **Audio Monitoring** to **Monitor and Output**.
</details>

<details>
<summary><b>Why didn't my reward start a countdown timer?</b></summary>

* Check that the reward's description ends with the duration wrapped in parentheses, such as `(5:00)` for 5 minutes or `(1:00:00)` for 1 hour.
</details>
