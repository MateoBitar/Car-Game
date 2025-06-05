# Python Car Game

## Table of Contents
- [Project Overview](#project-overview)
- [Features](#features)
- [Game Mechanics](#game-mechanics)
- [Getting Started](#getting-started)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Assets & Audio](#assets--audio)
- [Controls](#controls)

---

## Project Overview
**Python Car Game** is a lane-based arcade-style driving game developed using Pygame. The player must avoid oncoming cars and shoot bullets to destroy them while progressing through increasingly challenging levels. The game features dynamic difficulty, responsive controls, collision detection, and a retro car sound for immersion.

---

## Features
- 🎮 Smooth player movement using arrow keys or A/D.
- 🚗 Enemies spawn in multiple lanes and increase with levels.
- 🔫 Bullet firing mechanism to destroy enemy cars.
- 💥 Collision detection and game over screen.
- 🟢 Dynamic level progression.
- 🔊 Background engine sound (looped via pygame.mixer).
- 🎨 Basic graphics and animations using pygame.Surface and sprites.

---

## Game Mechanics
- **Player Car**: Moves left/right within the defined road lanes.
- **Enemy Cars**: Move downward and respawn when destroyed or passed.
- **Bullets**: The player can shoot up to 10 bullets per level. Bullets collide with enemy cars to remove them.
- **Leveling**: Player advances to the next level after reaching a certain score.
- **Game Over**: Triggered on collision with an enemy car.

---

## Getting Started
To get the game running on your system, follow the instructions below.

---

## Prerequisites
- Python 3.7+
- Pygame

---

## Installation

Clone the repository:
```bash
git clone https://github.com/your-username/python-car-game
cd python-car-game
```

Install dependencies:
```bash
pip install pygame
```

Make sure you have the following assets:
- `red_car.png` (player)
- `blue_car.png` (enemy)
- A `.wav` file for car engine sound

---

## Usage

Run the game using:
```bash
python car_game.py
```
Replace `car_game.py` with the filename of your script if different.

---

## Assets & Audio

The following files should be placed in accessible paths:

| Type  | File Name                                | Example Path                          |
|-------|-------------------------------------------|----------------------------------------|
| Image | `red_car.png` (player)                    | Car game/red_car.png                   |
| Image | `blue_car.png` (enemy)                    | Car game/blue_car.png                  |
| Audio | `.wav` car sound file (e.g., engine revving) | Downloads/339703__ffkoenigsegg20012017__audi-v8.wav |

🔧 You may modify the paths in the code to match your system or project structure.

---

## Controls

| Action        | Key(s)                         |
|---------------|--------------------------------|
| Move Left     | Left Arrow / A                 |
| Move Right    | Right Arrow / D                |
| Shoot         | Space                          |
| Quit          | X on window                    |
| Restart       | Click "Restart" on game over   |
| Next Level    | Click "Next Level" after winning |

---

Feel free to fork and enhance the game with power-ups, better visuals, or multiplayer support. Pull requests are welcome!
