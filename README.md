# Lamb Lanterns

[![Modrinth](https://img.shields.io/modrinth/dt/lamb-lanterns?logo=modrinth&label=Modrinth&color=00AF5C)](https://modrinth.com/mod/lamb-lanterns)
[![CurseForge](https://cf.way2muchnoise.eu/full_1539815_downloads.svg)](https://www.curseforge.com/minecraft/mc-mods/lamb-lanterns)
[![Minecraft](https://img.shields.io/modrinth/game-versions/lamb-lanterns?label=Minecraft)](https://modrinth.com/mod/lamb-lanterns)

## What this fork adds:
- Disable or enable lantern physics
- Put torches into the lantern slot

A NeoForge companion mod for [LambDynamicLights](https://lambdaurora.dev/projects/lambdynamiclights),
Minecraft **1.21.1**. Wear a vanilla lantern (or soul lantern) in a Curios
dedicated **lantern** slot — it hangs from the right hip (configurable), swings
on a damped 2D pendulum, and emits real dynamic light through the LDL API.

## Requirements

| What                | Version            |
| ------------------- | ------------------ |
| Minecraft           | 1.21.1             |
| NeoForge            | 21.1.228+          |
| Curios              | 9.0.0+             |
| LambDynamicLights   | 3.0.0+ — required, client-only (the whole point) |
| Iris                | 1.8.0+ — optional, client-only (shader support) |

The mod must be installed on **both server and client**:

- **Server** registers the belt slot and accepts lanterns into it (Curios
  inventory is server-authoritative).
- **Client** renders the lantern on the body and handles the
  LambDynamicLights light emission. LambDynamicLights is only required
  on the client; a dedicated server runs without it.

## Features

- Adds a Curios `lantern` slot attached to the player, accepting any item
  in the `#curios:lantern` tag (vanilla lantern + soul lantern out of the box).
  The slot has its own faint lantern silhouette icon.
- Renders the lantern hanging from the hip with chain attachment. The
  placement is configurable — see [Configuration](#configuration).
- 2D damped-spring pendulum: swings forward/back when you walk and
  side-to-side when you strafe; gets a kick when you start sneaking.
- LambDynamicLights integration via the LDL API and the Yumi entrypoint
  system — the worn lantern emits dynamic light as if held. The entrypoint
  class is loaded lazily, so the mod still loads on a dedicated server
  (where LambDynamicLights is absent).
- Iris/shader compatible: a small mixin keeps the worn lantern rendering
  correctly under shaderpacks when Iris is installed.

## Configuration

Open **Mods → Lamb Lanterns → Config** in-game, or edit
`config/lamblanterns-client.toml`. The settings are client-side and
per-player, and apply live without a restart.

| Option             | Default | Effect                                                                                     |
| ------------------ | ------- | ------------------------------------------------------------------------------------------ |
| `horizontalOffset` | `1.0`   | Side placement. `0` = centred, positive = right hip, negative = left hip (`±1.0` = a hip). |
| `verticalOffset`   | `-1.55` | Height. Higher raises the lantern toward the chest, lower drops it toward the belt.         |
| `depthOffset`      | `-1.0`  | Depth. Higher moves it toward the front of the body, lower toward the back.                 |

Set `horizontalOffset` to a negative value (e.g. `-1.0`) to wear the
lantern on the left hip — handy if it clashes with a satchel or another
belt/back item.

## Installation

Drop `lamblanterns-<version>.jar` into the `mods/` folder of both your
server and your client. Make sure Curios is also installed.

## Building from source

Requires JDK 21.

```sh
./gradlew build
```

The output jar lands in `build/libs/lamblanterns-<version>.jar`.

## Tagging more items as wearable belt items

You can extend `#curios:lantern` from another datapack to make any item
belt-eligible. The lantern renderer only renders vanilla lanterns; other
items will sit invisibly in the slot unless they ship their own
`ICurioRenderer`.

## Credits

The body-part anchored rendering technique and the pendulum physics
shape are adapted from
[ImmersiveLanterns](https://modrinth.com/mod/immersive-lanterns)
by Toni — go check it out, it's a much fuller implementation.

## License

[MIT](LICENSE)
