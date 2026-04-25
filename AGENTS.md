# AI Coding Agent Guidelines for Simulated Project

## Project Overview
This is a multi-module Minecraft mod suite extending Create with physics-based contraptions. The project consists of three mods:
- **Simulated**: Core mod providing assembly tools, redstone components, and physics simulation framework
- **Aeronautics**: Flying contraptions (balloons, propellers, levitite)
- **Offroad**: Land vehicles and wheeled contraptions

Built on NeoForge for Minecraft 1.21.1, using the Sable physics engine for realistic contraption behavior.

## Architecture
- **Multi-module structure**: Each mod has `:common` (shared code) and `:neoforge` (loader-specific) subprojects
- **Common code pattern**: Platform-agnostic logic in `:mod:common`, loader implementations in `:mod:neoforge`
- **Custom Gradle plugins**: `multiloader-common` and `multiloader-loader` in `buildSrc/` handle cross-platform builds
- **Physics integration**: Sable engine handles physics ticks via `SableEventPlatform.INSTANCE.onPhysicsTick()`

## Key Dependencies & Integration Points
- **Create**: Primary mod being extended - use `AllBlocks`, `AllItems`, stress system, etc.
- **Sable**: Physics engine - contraptions implement physics bodies, use `SableEventPlatform` for tick hooks
- **Registrate**: Registration framework - all blocks/items use `Simulated.getRegistrate()` builder pattern
- **Veil**: Rendering library for advanced graphics effects
- **Flywheel**: GPU-accelerated rendering for kinetic animations
- **Ponder**: In-game documentation system - scenes in `content/ponder/`

## Registration Patterns
- **Lazy initialization**: Use `NonNullSupplier.lazy()` for registrate instance (`Simulated.java`)
- **Index classes**: All registrations in `index/` package (e.g., `SimBlocks.register()`)
- **Deferred registration**: NeoForge-specific registrations use `DeferredRegister` in mod constructor
- **Creative tabs**: Each mod has its own tab, registered in NeoForge main class

## Build & Development Workflow
- **Build command**: `./gradlew build` - compiles all modules and runs tests
- **Run datagen**: `./gradlew :simulated:common:runData` - generates assets, lang, recipes
- **Version management**: Versions in root `gradle.properties`, mod-specific props in `mod/gradle.properties`
- **Publishing**: Maven publishing configured for private repo with env vars (`local_maven_*`)

## Code Conventions
- **Package structure**: `dev.simulated_team.{modname}` (e.g., `dev.simulated_team.simulated`)
- **Resource locations**: Use `Simulated.path("texture")` for mod-prefixed IDs
- **Mixin usage**: Extensive Create modifications in `mixin/` packages with custom plugins
- **Event handling**: Common events in `events/` package, loader-specific in `neoforge/events/`
- **Config system**: Server configs in `config/server/`, registered via `NeoForgeSimConfigService`

## Common Patterns
- **Block behaviors**: Extend Create's `Block` classes, implement custom `MovementBehaviour` for physics
- **Contraption entities**: Use Sable's `PhysicsContraptionEntity` for movable structures
- **Redstone integration**: Custom redstone components extend Create's signal system
- **Data components**: Custom item/block data via `SimDataComponents.register()`
- **Network packets**: All networking through `SimPacketManager` with custom packet types

## Key Files to Reference
- `simulated/common/src/main/java/dev/simulated_team/simulated/Simulated.java` - Main init and registrate setup
- `buildSrc/src/main/groovy/multiloader-common.gradle` - Common build logic and dependencies
- `simulated/common/src/main/java/dev/simulated_team/simulated/index/SimBlocks.java` - Block registration examples
- `gradle.properties` - Version and dependency management
- `settings.gradle.kts` - Module structure definition</content>
<parameter name="filePath">C:\Users\berth\Desktop\Aeronautics\Repos\Simulated-Project\AGENTS.md
