# 🧟 Zombie Arena

A top-down zombie survival shooter built in **C++ with SFML**, developed while working through **Beginning C++ Game Programming, 3rd Edition by John Horton**.

The goal is simple: survive increasingly difficult waves of zombies, collect health and ammunition, improve your abilities, and achieve the highest score possible.

![C++](https://img.shields.io/badge/C++-17-blue?style=for-the-badge\&logo=cplusplus)
![SFML](https://img.shields.io/badge/SFML-2.x-green?style=for-the-badge)
![Visual Studio](https://img.shields.io/badge/Visual%20Studio-2022-purple?style=for-the-badge)

---

## 🎮 About the Game

**Zombie Arena** is a top-down survival shooter where the player fights against increasingly large hordes of zombies.

Each wave increases the size of the arena and the number of zombies. After clearing a wave, the player can choose an upgrade before continuing.

The game includes four major game states:

* **PLAYING** — actively playing the game
* **PAUSED** — temporarily stops gameplay
* **LEVELING UP** — choose an upgrade between waves
* **GAME OVER** — player has been defeated

These states are managed through an enum-based game-state system.

---

## ✨ Features

### 🧟 Zombie Waves

* Zombies spawn in increasingly larger hordes.
* The number of zombies increases with each wave.
* Zombies track and move toward the player.
* The next wave begins after all zombies from the current wave are defeated.

The number of zombies is calculated based on the current wave:

```cpp
numZombies = 5 * wave;
```

---

### 🔫 Shooting System

The player aims using the mouse crosshair and fires using the left mouse button.

The game features:

* Bullet management
* Fire-rate control
* Magazine capacity
* Spare ammunition
* Automatic bullet-slot recycling
* Shooting sound effects

The project maintains an array of **100 bullets** and reuses bullet objects instead of continuously allocating new ones.

---

### 🔄 Reloading

Press **R** to reload.

The game handles:

* Full magazine reloads
* Partial reloads when ammunition is low
* Failed reloads when no ammunition remains
* Reload sound effects

---

### ❤️ Health System

The player has a health bar displayed on the HUD.

When zombies collide with the player, damage is applied. If the player's health reaches zero, the game enters the **GAME OVER** state.

---

### 🎁 Pickups

Two different pickups are available:

* ❤️ **Health Pickup**
* 🔫 **Ammo Pickup**

Picking them up increases the player's health or available ammunition.

## Both pickups can also be upgraded during the leveling phase.

### ⬆️ Level-Up System

After clearing a wave, the player chooses one of six upgrades:

| Key | Upgrade                 |
| --- | ----------------------- |
| `1` | Increase rate of fire   |
| `2` | Increase clip size      |
| `3` | Increase maximum health |
| `4` | Increase running speed  |
| `5` | Improve health pickups  |
| `6` | Improve ammo pickups    |

The selected upgrade determines how the player becomes stronger in subsequent waves.

---

### 🏆 Score & High Score

Players receive **10 points for every zombie killed**.

The game tracks:

* Current score
* High score
* Current wave
* Remaining zombies

The high score is loaded from:

```text
gamedata/scores.txt
```

## and saved when the player dies.

### 🎯 Mouse Crosshair & Camera

The mouse position is converted from screen coordinates into world coordinates so that the player can aim correctly regardless of the camera position.

The camera follows the player as they move around the arena.

---

### 🖥️ HUD

The game displays:

* ❤️ Health bar
* 🔫 Current ammunition
* 🏆 Score
* 👑 High score
* 🧟 Remaining zombies
* 🌊 Current wave

## The HUD uses a separate SFML view, allowing it to remain fixed on the screen while the game world moves.

### 🔊 Sound Effects

The game includes sound effects for:

* Shooting
* Reloading
* Failed reload
* Zombie/player hits
* Zombie deaths
* Power-ups
* Pickups

---

## 🕹️ Controls

| Input               | Action                   |
| ------------------- | ------------------------ |
| `W`                 | Move Up                  |
| `S`                 | Move Down                |
| `A`                 | Move Left                |
| `D`                 | Move Right               |
| `Left Mouse Button` | Shoot                    |
| `R`                 | Reload                   |
| `1`                 | Increase Fire Rate       |
| `2`                 | Increase Clip Size       |
| `3`                 | Increase Health          |
| `4`                 | Increase Run Speed       |
| `5`                 | Upgrade Health Pickups   |
| `6`                 | Upgrade Ammo Pickups     |
| `Enter`             | Start / Pause / Continue |
| `Escape`            | Exit Game                |

The movement and shooting controls are handled directly through SFML keyboard and mouse input.

---

## 🛠️ Technologies Used

* **C++**
* **SFML**

  * SFML Graphics
  * SFML Audio
* **Visual Studio**
* Object-Oriented Programming
* Dynamic memory management
* Collision detection
* Game loops
* Delta-time based movement
* 2D coordinate systems
* File I/O

The main game integrates several custom classes including:

```text
Player
ZombieArena
TextureHolder
Bullet
Pickup
```

---

## 🧠 C++ Concepts Practiced

This project helped me put several C++ concepts into practice:

### Object-Oriented Programming

The game is divided into separate classes responsible for different game entities and systems.

### Pointers & Dynamic Memory

Zombie hordes are dynamically allocated and cleaned up when no longer needed:

```cpp
zombies = createHorde(numZombies, arena);

delete[] zombies;
```

### Arrays

The game maintains a reusable array of 100 bullets:

```cpp
Bullet bullets[100];
```

### File I/O

The high score is persisted using C++ file streams:

```cpp
std::ifstream
std::ofstream
```

### Enumerations

Game states are represented using a strongly typed enumeration:

```cpp
enum class State
{
    PAUSED,
    LEVELING_UP,
    GAME_OVER,
    PLAYING
};
```

### Collision Detection

The game uses bounding rectangles to determine collisions between:

* Bullets and zombies
* Zombies and player
* Player and health pickups
* Player and ammo pickups

### Delta Time

Movement and updates use delta time to make gameplay independent of frame rate.

---

## 📂 Project Structure

A typical project structure is:

```text
ZombieArena/
│
├── ZombieArena.cpp
├── Player.cpp
├── Player.h
├── Zombie.cpp
├── Zombie.h
├── Bullet.cpp
├── Bullet.h
├── Pickup.cpp
├── Pickup.h
├── TextureHolder.cpp
├── TextureHolder.h
├── ZombieArena.cpp
├── ZombieArena.h
│
├── graphics/
│   ├── background.png
│   ├── background_sheet.png
│   ├── crosshair.png
│   ├── ammo_icon.png
│   └── ...
│
├── sound/
│   ├── shoot.wav
│   ├── reload.wav
│   ├── hit.wav
│   ├── splat.wav
│   ├── powerup.wav
│   └── pickup.wav
│
├── fonts/
│   └── zombiecontrol.ttf
│
└── gamedata/
    └── scores.txt
```

> **Note:** Adjust the structure above if your local repository contains additional or differently named files.

---

## ⚙️ How to Run

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/ZombieArena.git
```

### 2. Open the project

Open the Visual Studio solution/project.

### 3. Configure SFML

Make sure SFML is correctly configured for your Visual Studio environment.

The project requires the SFML graphics and audio libraries.

### 4. Check the asset folders

Make sure these directories are located where the executable can access them:

```text
graphics/
sound/
fonts/
gamedata/
```

The game loads assets using relative paths such as:

```cpp
graphics/background_sheet.png
sound/shoot.wav
fonts/zombiecontrol.ttf
gamedata/scores.txt
```

### 5. Build & Run

Build the project in Visual Studio and run the application.

---

## 🎯 Gameplay Loop

The core gameplay follows this cycle:

```text
Start Game
    ↓
Choose Upgrade
    ↓
Enter Arena
    ↓
Fight Zombies
    ↓
Collect Health / Ammo
    ↓
Kill All Zombies
    ↓
Choose Upgrade
    ↓
Next Wave
    ↓
Repeat
    ↓
Player Dies
    ↓
Game Over
```

## The main game loop continuously handles **input → update → collision detection → rendering**, which forms the foundation of the game architecture.

## 📚 Learning Source

This project was developed while studying:

**Beginning C++ Game Programming, 3rd Edition**
**Author:** John Horton

This project was particularly useful for understanding how individual C++ programming concepts come together to create a complete interactive application.

---

## 🚀 Possible Future Improvements

Some ideas for expanding the project:

* Add different zombie types
* Add multiple weapons
* Add weapon switching
* Add boss zombies
* Add more pickup types
* Add a main menu
* Add difficulty settings
* Add background music
* Add particle effects
* Add animated zombie death effects
* Add configurable controls
* Add a persistent leaderboard
* Improve enemy AI
* Add additional maps
* Add a minimap
* Add controller support

---

## 💡 What I Learned

Building **Zombie Arena** was a big step beyond writing small C++ programs.

The project required me to think about how multiple systems work together:

**Input → Player → Weapons → Bullets → Zombies → Collision → Score → Waves → Upgrades → HUD → Game State**

Instead of treating the game as one large program, I learned how to divide functionality into different classes and systems and make them communicate with each other.

Most importantly, I got more comfortable with the **C++ game loop, object-oriented programming, pointers, arrays, collision detection, SFML, file I/O, and real-time game development**.

---

## ⭐ Acknowledgment

This project was created as part of my learning journey through:

**Beginning C++ Game Programming, 3rd Edition — John Horton**

The project was used as a practical way to learn and apply C++ game-development concepts.

---

## 👤 Author

**Sanjarbek Jumaboev**

Software Engineering | C++ | Game Development | AI

---

⭐ If you find this project interesting, feel free to explore the code and follow my progress as I continue building projects in C++ and AI.
