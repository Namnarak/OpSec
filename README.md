<div align="center">

<img src="https://github.com/user-attachments/assets/9adba640-2570-4c22-9355-4f13aa5d4507" alt="OpSec logo" width="120" />

# OpSec

**Privacy and fingerprinting protection for Minecraft.**

A client-side Fabric mod that helps protect players against client fingerprinting, tracking techniques, resource-pack abuse, and other privacy-invasive server-side probes.

<p>
  <a href="https://github.com/Namnarak/OpSec/releases/latest"><img src="https://img.shields.io/github/v/release/Namnarak/OpSec?display_name=tag&logo=github&label=Latest%20release" alt="Latest release"></a>
  <a href="https://github.com/Namnarak/OpSec/releases"><img src="https://img.shields.io/github/downloads/Namnarak/OpSec/total?logo=github&label=GitHub%20downloads" alt="GitHub downloads"></a>
  <a href="https://modrinth.com/mod/opsec"><img src="https://img.shields.io/modrinth/dt/opsec?logo=modrinth&label=Modrinth&color=00AF5C" alt="Modrinth downloads"></a>
  <a href="https://www.curseforge.com/minecraft/mc-mods/opsec"><img src="https://img.shields.io/curseforge/dt/1519411?logo=curseforge&label=CurseForge&color=F16436" alt="CurseForge downloads"></a>
</p>
<p>
  <a href="#features">Features</a> ·
  <a href="#installation">Installation</a> ·
  <a href="#configuration">Configuration</a> ·
  <a href="#building-from-source">Build</a> ·
  <a href="CHANGELOG.md">Changelog</a>
</p>

</div>

> [!IMPORTANT]
> **Download safely.** Use this repository's [GitHub Releases](https://github.com/Namnarak/OpSec/releases) for builds of this continuation. The original upstream project is maintained separately at [aurickk/OpSec](https://github.com/aurickk/OpSec). Do not download builds from unofficial mirrors, phishing sites, or Discord attachments.

> [!WARNING]
> This is an **unofficial, independently maintained continuation** of [OpSec by aurickk](https://github.com/aurickk/OpSec). It is not affiliated with Mojang Studios, Microsoft, or the upstream author. This project is developed with AI-assisted tooling and reviewed/maintained independently.

## Overview

Minecraft servers can use several client-visible behaviors to infer which mods a player has installed or to correlate players across sessions. OpSec provides configurable protections against these techniques while allowing users to keep the mods and server features they actually need.

OpSec is a privacy tool—not a guarantee of anonymity. Protection depends on the Minecraft version, installed mods, server behavior, and selected configuration.

## Features

| Feature | What it does |
| --- | --- |
| **Vanilla brand spoofing** | Presents a vanilla-like client brand and blocks mod-specific detection paths where supported. |
| **Channel spoofing** | Conditionally blocks mod network channels that could reveal installed mods. |
| **Known-pack filtering** | Removes non-whitelisted mod pack identifiers from the known-packs handshake. |
| **Resource-pack cache isolation** | Separates downloaded server resource-pack caches by account UUID to reduce cross-account correlation. |
| **Local URL blocking** | Blocks resource-pack requests or redirects targeting local and private network addresses. |
| **Server pack controls** | Lets users control whether required server resource packs are applied. |
| **Shader override filtering** | Prevents server resource packs from replacing shader files belonging to non-whitelisted mods. |
| **Key-resolution protection** | Controls how translation-key probes from server packets are resolved. |
| **Meteor compatibility fix** | Disables Meteor's conflicting legacy key-resolution protection so OpSec can handle the probe consistently. |
| **Mod whitelist** | Automatically or manually exempts selected mods from relevant protections. |
| **Chat-signing control** | Configures when Minecraft chat messages are signed. |
| **Account manager** | Manages saved Minecraft sessions and account switching. |
| **Telemetry blocking** | Disables Minecraft telemetry transmission to Mojang when enabled. |

For examples of servers and plugins associated with tracking-related exploits, see the [ExploitPreventer Hall of Shame](https://github.com/NikOverflow/ExploitPreventer/blob/master/HALL_OF_SHAME.md).

## Compatibility

| Component | Support |
| --- | --- |
| Minecraft | 1.20 – 26.3 (see available release assets) |
| Mod loader | Fabric |
| Fabric Loader | 0.16.0+; 0.18.5+ for MC 26.1.x; 0.19.5+ for MC 26.3 |
| Fabric API | Required; use a build matching your Minecraft version |

> [!NOTE]
> Always choose the JAR whose Minecraft version is listed in its filename. Availability of a build does not imply that every feature behaves identically across all Minecraft versions.

## Installation

1. Install [Fabric Loader](https://fabricmc.net/use/) for your Minecraft version.
2. Install the matching [Fabric API](https://modrinth.com/mod/fabric-api).
3. Open the [OpSec Releases page](https://github.com/Namnarak/OpSec/releases).
4. Download the JAR matching your Minecraft version (for example, `opsec-26.3+v1.1.7.3.jar`).
5. Place the OpSec JAR and Fabric API in your `.minecraft/mods` folder.
6. Start Minecraft with the Fabric profile.

To update, replace the previous OpSec JAR with the new version. Avoid keeping multiple OpSec versions in the mods folder.

## Configuration

Open the **OpSec** button in the multiplayer server selection screen, or use [Mod Menu](https://modrinth.com/mod/modmenu) when installed.

<img src="https://github.com/user-attachments/assets/c69a768b-60ac-4f78-9705-184f6c4e4495" alt="OpSec configuration screen" width="100%" />

Reconnect to the server after changing settings while connected to ensure that the changes are applied.

### Protection

| Setting | Description |
| --- | --- |
| **Spoof as vanilla** | Enables or disables vanilla-brand behavior. |
| **Isolate Pack Cache** | Separates server resource-pack caches by account. |
| **Block Local Pack URLs** | Blocks local/private-network resource-pack URLs. |
| **Bypass Server Pack Requirement** | Selects how required server resource packs are handled. |
| **Strip Mod Shader Overrides** | Filters server-provided shader overrides for non-whitelisted mods. |
| **Clear Cache** | Deletes cached server resource packs. |
| **Key Resolution Spoofing** | Enables or disables key-resolution protection. |
| **Fake Default Keybinds** | Returns default vanilla keybind values instead of the player's actual bindings. |
| **Meteor Fix** | Disables Meteor's conflicting legacy key-resolution protection when Meteor is installed. |
| **Signing Mode** | Selects chat-signing behavior: OFF, ON, or AUTO. |
| **Disable Telemetry** | Enables or disables telemetry blocking. |

**Server pack modes**

- **MANUAL** — Default vanilla behavior when a pack is pushed. The user can still toggle server packs.
- **ASK** — Keeps the pushed server pack from being applied automatically and displays a consent prompt.
- **ALWAYS ON** — Server packs are not applied by default; the user can still toggle them back on.

### Whitelist

| Setting | Description |
| --- | --- |
| **Whitelist Mode** | Selects BLOCK ALL, AUTO, or CUSTOM behavior. |
| **Installed Mods** | In CUSTOM mode, choose which installed mods are exempted from protection. |

- **BLOCK ALL** — Blocks mod content covered by the whitelist system.
- **AUTO** — Automatically whitelists mods that register network channels. This is the default.
- **CUSTOM** — Lets the user select individual installed mods.

When whitelist mode is active (AUTO or CUSTOM), vanilla brand spoofing is disabled because exposing Fabric mod functionality requires the client brand to match accordingly.

> [!NOTE]
> CUSTOM mode lists installed mods. AUTO mode focuses on mods that register network channels.

### Miscellaneous

| Setting | Description |
| --- | --- |
| **Show Alerts** | Displays chat messages when tracking or probing is detected. |
| **Show Toasts** | Displays popup notifications for important events. |
| **Log Detections** | Writes detection events to the game log. |
| **Debug Alerts** | Displays alerts for all probed keys, including unchanged values. |
| **Debug Command** | Enables the `/opsec` command. Disabled by default. |

### Accounts

| Setting | Description |
| --- | --- |
| **Saved Accounts** | Lists saved accounts with login, logout, and remove actions. |
| **Refresh All** | Revalidates saved account tokens; invalid tokens are marked red. |
| **Add Session Token** | Adds an account using a session access token. |
| **Import / Export** | Imports or exports saved accounts using JSON files. |

> [!WARNING]
> Session and access tokens are sensitive credentials. Never share them, upload them to public issue trackers, or give them to untrusted tools. Only use tokens for accounts you own or are authorized to manage.

## Feature details

### Vanilla brand spoofing

Servers may query a client's brand to identify whether it is running a modded client. OpSec can present a vanilla-like brand and apply related protections to mod key resolutions, network channels, and known-pack identifiers while retaining vanilla entries.

- **ON** — Enables vanilla-like behavior and blocks mod-specific detection paths covered by OpSec.
- **OFF** — Uses the regular Fabric client brand. This is the default and supports automatic mod whitelisting.

### Channel spoofing

Servers can query registered network channels to infer which mods are installed. OpSec can conditionally block mod channels registered with the server. The behavior is controlled by the whitelist configuration so that mods requiring server communication can remain functional.

### Known-pack filtering

Some mods expose pack identifiers that servers can query. OpSec intercepts the outgoing `ServerboundSelectKnownPacks` response and removes entries belonging to non-whitelisted mods. Vanilla and automatically whitelisted packs remain.

This protection is active only where the relevant Fabric known-packs hook is available (Minecraft 1.21.11+ with a compatible modern Fabric API).

### Resource-pack cache isolation

Server-required resource packs can be used to correlate a client instance across accounts. Instead of sharing the usual `~/.minecraft/downloads/` cache, OpSec stores server resource packs in separate directories associated with each account UUID.

Based on the cache-isolation approach in [LiquidBounce](https://github.com/CCBlueX/LiquidBounce/blob/nextgen/src/main/java/net/ccbluex/liquidbounce/injection/mixins/minecraft/util/MixinDownloadQueue.java). Background reading: [Cytooxien resource-pack tracking](https://alaggydev.github.io/posts/cytooxien/).

### Block local URLs

A malicious server may provide a resource-pack URL that redirects to a local or private-network address, potentially probing devices and services on the player's network. OpSec checks resource-pack destinations and redirects and blocks requests targeting local addresses.

Derived from the relevant protection approach in [ExploitPreventer](https://github.com/NikOverflow/ExploitPreventer).

### Bypass server pack requirement

Servers can mark resource packs as required. OpSec provides client-side controls so users can decide whether server pack content should be applied.

Minecraft still handles pack downloads normally. OpSec exposes server packs as user-toggleable entries and preserves the server pack language data. This matters because servers may probe translation keys to infer whether a pack is active.

The available modes are **MANUAL**, **ASK**, and **ALWAYS ON**; see [Server pack modes](#server-pack-modes) above.

### Strip mod shader overrides

Some mods load GUI shaders through Minecraft's resource manager. A server resource pack could attempt to replace a mod's shader files, potentially disrupting the interface, causing crashes, or revealing that a particular mod is installed.

OpSec strips shader overrides under `assets/<modid>/shaders/` for installed mods that are not whitelisted. Vanilla (`minecraft`) shaders are not modified. Whitelisting a mod allows the server's shader overrides through.

### Key-resolution protection

Servers can send translatable text containing keys such as `key.attack` or `key.hide_icons` in server packets. The resolved result may reveal player keybinds or installed mod UI elements.

OpSec tracks translation-key resolution during server packet processing and controls which keys may resolve according to the selected protection and whitelist settings.

- With **Spoof as vanilla ON**, mod keys are blocked and vanilla keys can return default keybind values.
- With **Spoof as vanilla OFF**, Fabric API and whitelisted mod keys may resolve, while other mod keys are blocked.
- When **Fake Default Keybinds** is disabled, vanilla keybinds resolve to their actual configured values.

Example of a mod key being withheld:

```text
[key.meteor-client.open-commands] '.'         -> 'key.meteor-client.open-commands'
[key.meteor-client.open-gui]      'Right Shift' -> 'key.meteor-client.open-gui'
```

Example with fake default keybinds enabled:

```text
[key.hotbar.6] 'Q' -> '6'
[key.hotbar.7] 'E' -> '7'
[key.hotbar.8] 'R' -> '8'
```

Background reading: [Wurst Wiki — Sign Translation Vulnerability](https://wurst.wiki/sign_translation_vulnerability).

### Meteor compatibility fix

Meteor Client has a legacy key-resolution protection implementation that can conflict with OpSec's handling of translation-key probes. In some fallback-based probes, Meteor may return the raw key where a vanilla client would return the fallback value.

OpSec's compatibility fix disables Meteor's conflicting `AbstractSignEditScreenMixin` so OpSec can handle the resolution and fallback behavior.

<img src="https://github.com/user-attachments/assets/e157ae3f-6beb-4823-aca0-9c61573264e2" alt="Meteor key-resolution example" width="100%" />
<img src="https://github.com/user-attachments/assets/506b9c73-6747-40f8-9a56-52c0353034b4" alt="OpSec fallback behavior example" width="100%" />

### ExploitPreventer compatibility

OpSec can be installed alongside [ExploitPreventer](https://github.com/NikOverflow/ExploitPreventer). When both are present, overlapping protections are deferred to ExploitPreventer. These OpSec features are then unavailable while ExploitPreventer handles them:

- Brand spoofing
- Channel spoofing
- Known-pack filtering
- Resource-pack cache isolation
- Local URL blocking
- Key-resolution protection
- Mod whitelist

The corresponding settings are disabled in the configuration screen, but saved preferences are preserved and restored if ExploitPreventer is removed. Non-overlapping OpSec features—including alerts, chat signing, account management, telemetry blocking, shader override filtering, and Meteor compatibility—remain available.

### Chat-signing control

Based on [No Chat Reports](https://modrinth.com/mod/no-chat-reports).

Minecraft can attach cryptographic signatures to chat messages. OpSec lets users choose when messages are signed:

- **OFF** — Removes chat signatures. Servers enforcing secure chat may prevent unsigned messages from being sent.
- **AUTO** — Signs messages only when the server requires secure chat.
- **ON** — Uses default Minecraft behavior and signs every message.

### Account manager

The account manager is based on account-management concepts from [Meteor Client](https://github.com/MeteorDevelopment/meteor-client). It provides:

- **Session token login** — Add accounts using access tokens.
- **Token refresh** — Fetch new session tokens when supported for expired accounts.
- **Offline accounts** — Add username-only accounts without online authentication.
- **Account switching** — Switch to a saved account without restarting the game.
- **Token validation** — Refresh/check token validity; invalid tokens are marked red.
- **Import / export** — Back up and restore accounts through JSON files.

> [!WARNING]
> Account tokens grant access to accounts. Keep exported account files private and store them securely.

### Telemetry blocking

Based on [No Chat Reports](https://modrinth.com/mod/no-chat-reports).

Minecraft may send telemetry data to Mojang, including game events, performance metrics, client configuration, and usage statistics. When enabled, OpSec blocks the telemetry transmission covered by this feature. This is not intended to change normal gameplay.

## Alerts and debug commands

### Understanding alerts

| Alert | Meaning |
| --- | --- |
| **Key Resolution Exploit Detected** | The server appears to be probing translation keys or keybinds. |
| **Resource Pack Fingerprinting Detected** | A suspicious resource-pack URL was detected. |
| **Local URL Scan Detected** | A resource-pack destination targets a local or private address. |

### `/opsec` debug command

The command is **disabled by default**. Enable it in **Miscellaneous → Debug Command**.

| Command | Description |
| --- | --- |
| `/opsec` | Shows available commands. |
| `/opsec info` | Shows an overview of tracked mods. |
| `/opsec info <mod>` | Shows details for a mod, including translation keys, keybinds, channels, known packs, and shaders. |
| `/opsec channels` | Lists tracked network channels and their whitelist status. |

## Building from source

### Prerequisites

- Java 17 for Minecraft 1.20.1–1.20.4
- Java 21 for Minecraft 1.20.6–1.21.11
- Java 25 for Minecraft 26.1+
- Gradle wrapper (included in the repository)

### Build

```bash
git clone https://github.com/Namnarak/OpSec.git
cd OpSec

# Build all configured targets
./gradlew build
```

On Windows, use `gradlew.bat build`.

To build an individual configured target:

```bash
./gradlew :1.20.1:build
./gradlew :1.20.2:build
./gradlew :1.20.4:build
./gradlew :1.20.6:build
./gradlew :1.21.1:build
./gradlew :1.21.4:build
./gradlew :1.21.6:build
./gradlew :1.21.9:build
./gradlew :1.21.11:build
./gradlew :26.1:build
./gradlew :26.2:build
./gradlew :26.3:build
```

Build outputs are written under each target's `versions/<minecraft_version>/build/libs/` directory.

| Build target | Minecraft versions |
| --- | --- |
| `1.20.1` | 1.20–1.20.1 |
| `1.20.2` | 1.20.2 |
| `1.20.4` | 1.20.3–1.20.4 |
| `1.20.6` | 1.20.5–1.20.6 |
| `1.21.1` | 1.21–1.21.1 |
| `1.21.4` | 1.21.2–1.21.5 |
| `1.21.6` | 1.21.6–1.21.8 |
| `1.21.9` | 1.21.9–1.21.10 |
| `1.21.11` | 1.21.11 |
| `26.1` | 26.1–26.1.2 |
| `26.2` | 26.2 |
| `26.3` | 26.3 |

## Releases and changelog

- **Latest release:** [GitHub Releases](https://github.com/Namnarak/OpSec/releases/latest)
- **All versions:** [Release history](https://github.com/Namnarak/OpSec/releases)
- **Detailed changes:** [CHANGELOG.md](CHANGELOG.md)
- **Source history:** [Commits](https://github.com/Namnarak/OpSec/commits/main)

Release assets in this repository are built for this continuation. The original upstream releases remain available separately at [aurickk/OpSec Releases](https://github.com/aurickk/OpSec/releases).

## Credits and references

OpSec is a continuation of the original project by [aurickk](https://github.com/aurickk/OpSec). The following projects and resources informed specific features or integrations:

- [ExploitPreventer](https://github.com/NikOverflow/ExploitPreventer) — Local URL blocking and key-resolution protection approaches.
- [LiquidBounce](https://github.com/CCBlueX/LiquidBounce/blob/nextgen/src/main/java/net/ccbluex/liquidbounce/injection/mixins/minecraft/util/MixinDownloadQueue.java) — Resource-pack cache isolation reference.
- [Meteor Client](https://github.com/MeteorDevelopment/meteor-client) — Account-management reference and compatibility work.
- [No Chat Reports](https://modrinth.com/mod/no-chat-reports) — Chat-signing control and telemetry-blocking references.
- [No Prying Eyes](https://github.com/Daxanius/NoPryingEyes) — Secure-chat enforcement detection reference.
- [MixinSquared](https://github.com/Bawnorton/MixinSquared) — Mixin cancellation support.
- [Stonecutter](https://stonecutter.kikugie.dev/) — Multi-version build system.
- [Fabric API](https://github.com/FabricMC/fabric-api) — Fabric translation and keybind integration.

## License

OpSec is licensed under the [GNU General Public License v3.0](LICENSE).

## Disclaimer

OpSec is an unofficial community project and is not affiliated with, endorsed by, or sponsored by Mojang Studios or Microsoft. Minecraft is a trademark of Microsoft.

This repository continues [OpSec by aurickk](https://github.com/aurickk/OpSec) independently. The original idea and upstream implementation belong to their respective author(s); this continuation maintains its own changes, compatibility work, and releases.

OpSec is intended to help users understand and control client-side privacy exposure. It is not intended to bypass server rules, evade bans, or provide an unfair gameplay advantage. Users are responsible for following the rules and terms of service of the servers they join.
