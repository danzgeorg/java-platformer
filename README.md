# Pixel Adventure

A three-level 2D platformer written in **Java**, using Swing for the window and **CityEngine** (City, University of London's teaching wrapper around the JBox2D physics engine) for physics and collisions.

<!-- Replace with a gameplay screenshot or GIF: upload it to docs/screenshot.png -->
[Gameplay screenshot](Gameplay.png)

## How to play

Run and jump across the platforms, collect fruit and stomp on enemies. Your score and health carry over from one level to the next, and you lose if your health runs out.

| Key | Action |
|---|---|
| A / D | Move left / right |
| W or Space | Jump |
| S | Drop down |
| Q or Shift | Dash |

| Level | Enemy | Score needed to finish |
|---|---|---|
| 1 | Snails | 3 |
| 2 | Chickens | 5 |
| 3 | Pigs (faster) | 8 |

Landing on an enemy from above destroys it and bounces you up, but still costs 10 health. Running into one from the side costs 20 health and knocks you back.

## Running it

The game needs the CityEngine library, which is included in this repo as `CityEngine40.zip`.

1. Clone the repo and open the folder in **IntelliJ IDEA**.
2. Unzip `CityEngine40.zip` to get `CityEngine.jar`.
3. Go to **File > Project Structure > Modules > Dependencies**, click **+**, choose **JARs or Directories** and select `CityEngine.jar`.
4. Right-click the project root folder and choose **Mark Directory as > Sources Root**, so the `game` package is found.
5. Run `game.Game`. The working directory must be the project root, so the game can find the `data/` folder.

## How it works

- **Level structure.** `GameLevel` is an abstract base class holding the shared setup (character, platforms, timers and the win check). `Level1`, `Level2` and `Level3` each add their own layout, enemy type and score target.
- **Collisions.** `GenericCollisionListener` works out whether the player hit an enemy from above or from the side and applies different damage, bounce and knockback for each. `PlatformEnemyListener` turns enemies around at the edges of their platforms.
- **Pickups.** Fruit spawns on a timer at a series of positions, and a new pickup appears shortly after one is collected.
- **Level transitions.** When the score target is reached, the level stops its timers, cleans up and starts the next level on the Swing event thread, passing score and health across.
- **Rendering and sound.** `GameView` draws a looping scrolling background per level plus the HUD. `SoundManager` is a singleton that handles background music and sound effects.

## Project structure

```
game/Game.java        Entry point and level switching
game/levels/          GameLevel base class and the three levels
game/character/       Player movement, jumping, dashing, health and score
game/enemies/         Patrolling enemies
game/collisions/      Collision handling for enemies, pickups and platforms
game/pickups/         Collectible fruit
game/ui/              Game view, background and HUD
game/input/           Keyboard and mouse controls
game/utils/           Polygon editor tool for drawing collision shapes
data/                 Sprites, backgrounds and sounds
```

## Credits

Built by Daniel Georgiev as a university project at City, University of London. Physics engine: CityEngine (City, University of London), built on JBox2D.
Character, enemy, item and background art: [Pixel Adventure 1 and 2](https://pixelfrog-assets.itch.io/pixel-adventure-1) by [Pixel Frog](https://x.com/PixelFrogStudio)
