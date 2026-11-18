# Changelog

All notable changes in the Namnarak continuation of OpSec are documented here.

This project is an unofficial, independently maintained continuation of [aurickk/OpSec](https://github.com/aurickk/OpSec). Changes below describe work in this repository and do not imply that the upstream project made these changes.

## [1.1.7.2] - 2026-11-17

### Added
- Added a dedicated Minecraft 26.3 version target.
- Registered Minecraft 26.3 in the Stonecutter multi-version build and aggregate `buildAll` task.
- Added a GitHub Actions workflow to build all supported targets, upload JAR artifacts, and publish a GitHub pre-release when a version tag is pushed.
- Added a dedicated Minecraft 26.3 Gradle properties file with its loader, Fabric API, Mod Menu, and version-range settings.

### Minecraft 26.3 compatibility
- Updated the Fabric Loom toolchain and Gradle wrapper for the Minecraft 26.3 build environment.
- Added version-specific handling for APIs removed or reshaped in 26.3:
  - Open release links through `Blaze3D.openUri` instead of the removed `Util.OS.openUri`.
  - Read mouse state through Minecraft's `MouseHandler` rather than direct LWJGL GLFW calls, matching the SDL input change.
  - Adapt resource-pack access to the new `Pack.ResourcesSupplier` / stream-based resource API.
  - Resolve Authlib 10 user API and friends services through the new Minecraft services API, accounting for the removal of the legacy Yggdrasil package.
  - Use Java file dialogs where the previous TinyFD path is unavailable.
- Updated telemetry mixin targeting so telemetry blocking continues to target the Minecraft 26.3 user API service.
- Added version gates around legacy Yggdrasil mixin classes and configuration entries so older targets retain their existing implementation.

### Chat signing
- Adapted the outbound chat packet mixin for Minecraft 26.3, where the packet is a record and its signature is represented by `Optional<MessageSignature>`.
- On 26.3, clear the signature through a constructor-argument modifier and return `Optional.empty()` from the accessor.
- Kept the existing shadow-field implementation for older Minecraft targets.
- Made the constructor modifier static because it runs before the record constructor's `super()` call.
- Omitted the refmap entry for unobfuscated 26.x builds, while preserving the generated refmap for older remapped targets.

### Privacy protection fixes
- Fixed vanilla translation-key detection on Minecraft 26.3. Vanilla language resources now identify correctly by their pack ID as well as their resource type.
- This fixes vanilla keybind translations such as `key.forward` being incorrectly treated as mod keys, which could cause false exploit-preventer detections and incorrect protected results.
- Verified against a local Paper 26.3 server with CheckHacks 1.3.2: all 14 checks reported `NOT_DETECTED`, and `key.forward` resolved to `W`.

### Account and configuration maintenance
- Updated account-related compatibility paths for the newer Authlib service layout.
- Adjusted the configuration screen and supporting warning/update screens for the new version-specific code paths.
- Updated resource-pack and language mixins to account for changed Minecraft APIs.

### Build and verification
- The 26.3 compatibility work was verified with `./gradlew buildAll`; the recorded build produced all 12 target JARs.
- The 26.3 development client was launched to verify mixin application, joining a test server, passing Sonar, and loading a server resource pack without mixin errors.
- Chat-signature behavior and the vanilla translation fix were additionally checked in-game. These checks are documented as development verification, not a guarantee that every mod combination is compatible.

### Documentation and licensing
- Clarified in the README that Namnarak/OpSec is an unofficial independent continuation and is not affiliated with Mojang, Microsoft, or the upstream author.
- Restored the canonical, unmodified GNU GPL-3.0 license text and added a README license section.
- Updated the documented Minecraft support range and build matrix for 26.3.

---

## Earlier upstream functionality

Features inherited from the original OpSec project include client fingerprinting protection, channel spoofing, known-pack filtering, resource-pack cache isolation, local URL blocking, server-pack controls, shader override filtering, key-resolution protection, mod whitelisting, chat-signing controls, account management, and telemetry blocking.

For the original project's history, see [aurickk/OpSec commits](https://github.com/aurickk/OpSec/commits/main/).
