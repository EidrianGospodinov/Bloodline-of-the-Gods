# Bloodline of the Gods: The Wrath of the Demi-God

**Bloodline of the Gods** is a solo-developed third-person action-adventure combat prototype built in Unity using C#. Inspired by Greek mythology, the game centres around two demigods, Thalia and Orion, connected through a unique mechanic known as the **Divine Tether**.

The project explores how real-time character switching, elemental abilities, and tactical enemy encounters can create depth within a fast-paced combat system without relying heavily on traditional RPG mechanics.

Developed as a final-year university project, the game features a modular, data-driven architecture designed to support complex gameplay systems while maintaining flexibility and maintainability.

## Features

### Divine Tether & Dual-Hero Combat

The central mechanic allows players to switch between two demigods during active combat, preserving attack momentum and maintaining the flow of combat.

- Instantaneous switching between Thalia and Orion.
- Shared movement, dodging, and melee combat mechanics.
- Switch cooldown to prevent repetitive switching.
- Shared animation architecture supporting seamless character transitions.
- Distinct elemental abilities and combat specialisations.

**Thalia – Lightning**
- Lightning-based ranged attacks.
- Applies Burn through sustained elemental damage.
- Thunder Ultimate, delivering high burst damage against a focused target.

**Orion – Water**
- Water-based ranged attacks.
- Applies Freeze, slowing enemy movement and attack pacing.
- Water Blast Ultimate, delivering area damage against multiple enemies.

### Melee Combat System

- Data-driven melee attacks and combo sequences.
- Light and heavy attack combinations.
- Timed combo windows rewarding rhythmic inputs.
- Generic Finite State Machine controlling combat transitions.
- Animation layering and Avatar Masks for independent character and weapon animations.
- Hit pauses, attack anticipation, and recovery states.

### Enemy AI

A reusable AI architecture supports multiple enemy types through a shared generic state machine.

- Wander, Chase, and Attack states.
- Vision cone and line-of-sight detection.
- Distance-based state transitions.
- Unity NavMesh pathfinding.
- Weighted attack selection to reduce repetitive behaviour.
- Configurable attack types, wind-up delays, attack speeds, and critical hit probabilities.
- Enemy attack telegraphs providing visual warnings before incoming attacks.

The vertical slice features encounters involving mythological enemies, including the Minotaur, Cyclops, and Boar.

### Dynamic Targeting

- Target selection based on enemy proximity and camera direction.
- Automatic retargeting for high-impact abilities.
- Target visualisation through enemy outlines.
- Automatic target reassignment when the current target is defeated.

### Progression & Upgrade Systems

- Data-driven player statistics using Scriptable Objects.
- Upgradeable player attributes and abilities.
- Skill tree interface with upgrade costs and stat previews.
- Dynamic tooltips displaying current and upgraded values.
- Experience-based charging of Ultimate abilities.
- Teleportation between unlocked locations.

### Dialogue & Quest Systems

- Modular dialogue manager supporting sequential conversations.
- Branching dialogue choices.
- Asynchronous dialogue execution using C# Tasks.
- NPC interactions and dialogue-driven progression.
- Event-driven quest and objective management.
- Dynamic UI updates when objectives are completed.
- NPC command architecture designed to support more complex interactions.

### Elemental Status Effects

- Data-driven status effect architecture.
- Burn and Freeze effects.
- Configurable effect behaviour and duration.
- Event-driven communication between gameplay logic and visual effects.

## Technical Architecture

A significant focus of this project was building reusable systems rather than implementing individual gameplay mechanics through tightly coupled scripts.

### Generic Finite State Machine

Developed a custom generic Finite State Machine in C# to manage both player and enemy behaviour.

The same underlying architecture is reused across multiple systems, including:

- Player locomotion and combat.
- Nested attack combo state machines.
- Enemy AI behaviour.
- Attack anticipation, execution, and recovery.

The nested state machine architecture allows complex behaviours to be broken into smaller, independently managed states while maintaining consistent transition logic.

### Event-Driven Architecture

Implemented a custom, type-safe Global Event Bus using C# generics.

The system allows gameplay components to communicate without maintaining direct references to one another.

For example:
- Hero switching triggers events consumed by relevant gameplay and presentation systems.
- Enemy death events notify quest and progression systems.
- Status effect events update associated visual effects.
- Gameplay interactions can notify other systems without requiring direct dependencies.

This reduces coupling and makes individual systems easier to extend and maintain.

### Data-Driven Design

Unity Scriptable Objects are used extensively to separate configuration data from gameplay logic.

Custom data structures include:

- `AttackData`
- `AttackComboData`
- Enemy configuration data
- Player statistics and upgrade data
- Quest and progression data
- Status effect configuration

This approach allows gameplay values such as damage, attack delays, animation references, and upgrade parameters to be adjusted directly within the Unity Editor without modifying the underlying logic.

### Dependency Injection

Integrated Zenject to manage dependencies and object construction across the project.

- Centralised dependency registration through Game Installers.
- Interface-based service injection.
- Reduced reliance on direct object references and singletons.
- Runtime prefab instantiation through the dependency injection container.
- Dedicated services for functionality such as player respawning.

### Animation Architecture

Implemented a layered animation architecture to separate gameplay decisions from visual presentation.

- Multi-layered Animator Controllers.
- Avatar Masks for independent animation layers.
- Blend Trees for enemy locomotion.
- Synchronisation between FSM transitions and animation triggers.
- Shared animation logic supporting the dual-hero combat system.

## Performance & Testing

Testing was integrated throughout development to validate both gameplay functionality and runtime performance.

- Functional testing of core gameplay systems.
- Verification of state transitions and event propagation.
- Combat testing involving multiple enemy AI agents.
- Unity Profiler and Editor Stats used to monitor CPU, GPU, and memory performance.
- Performance benchmarking against a 60 FPS target.
- User experience playtesting to evaluate combat responsiveness, readability, and overall gameplay flow.

Optimisation work included staggering enemy NavMesh calculations to reduce CPU overhead and managing duplicate particle effects to avoid unnecessary GPU overdraw.

## Technologies & Tools

| Category | Technologies |
|---|---|
| Game Engine | Unity |
| Programming Language | C# |
| IDE | JetBrains Rider |
| Architecture | Generic FSM, Event Bus, Dependency Injection |
| Dependency Injection | Zenject |
| Data Management | Scriptable Objects |
| AI & Navigation | Unity NavMesh |
| Animation | Unity Animator, Avatar Masks, Blend Trees |
| Camera | Cinemachine |
| Input | Unity New Input System |
| UI | TextMeshPro |
| 3D Modelling | Blender |
| Animation Pipeline | Mixamo, Autodesk MotionBuilder |
| Asset Generation | Hunyuan3D, Meshy |
| Version Control | Git, GitHub |

## Development

Developed independently as my BSc Computer Games Development final-year project at the University of Westminster.

The project was delivered as a playable vertical slice, prioritising the implementation and evaluation of its core combat mechanics and underlying software architecture over the breadth of a complete commercial game.

The primary development focus was on C# programming, reusable gameplay systems, combat architecture, enemy AI, and modular software design.
