# ⚽ Penalty Shootout — Flask + Three.js + Bootstrap

A browser-based 3D penalty shootout game built with **Flask** (backend), **Three.js** (3D rendering), and **Bootstrap 5** (UI). Pick a corner, take your shot, and see if you beat the keeper across 5 penalties.

## Demo Preview

- Aim at one of 6 goal zones (top-left, top-center, top-right, bottom-left, bottom-center, bottom-right)
- Watch a 3D ball arc toward the goal while a keeper dives to make a save
- Track your score across 5 shots, then get a final result in a popup

## Tech Stack

| Layer      | Technology                     |
|------------|---------------------------------|
| Backend    | Flask (Python)                  |
| Frontend   | HTML5, Bootstrap 5 (CDN)        |
| 3D Engine  | Three.js r128 (CDN)             |
| Styling    | Bootstrap utility classes only (no custom CSS) |

## Project Structure

session2/
├── app.py # Flask application entry point
└── templates/
└── index.html # Game UI + inline Three.js game logic


## Prerequisites

- Python 3.7+
- pip

## Installation & Setup

1. **Clone or download this project**

```bash
   cd session2
```

2. **Install Flask**

```bash
   pip install flask
```

3. **Run the app**

```bash
   python app.py
```

4. **Open your browser**

   Navigate to:

http://127.0.0.1:5000/


## How to Play

1. Click one of the six **aim buttons** to choose where you want to shoot (e.g. Top Left, Bottom Center).
2. Click **Take Shot** to kick the ball.
3. The ball animates toward your chosen corner while the goalkeeper randomly dives to defend a zone.
   - If the keeper dives to the **same zone** you aimed at → **Saved** 🧤
   - Otherwise → **Goal** ⚽
4. Repeat for **5 shots total**.
5. After the 5th shot, a modal displays your final score with an option to **Play Again**.

## Game Logic Overview

- **Ball movement**: linearly interpolated from the penalty spot to the target zone, with an added sine-wave arc on the Y-axis to simulate a kick trajectory.
- **Keeper AI**: randomly selects one of the 6 zones to dive toward on each shot (uniform probability).
- **Save detection**: a shot is saved if the keeper's randomly chosen zone matches the player's selected aim zone.
- **Scene objects**: goalposts, crossbar, net, keeper, and ball are all built using primitive Three.js geometries (`BoxGeometry`, `CylinderGeometry`, `SphereGeometry`) — no external 3D model files required.

## Customization Ideas

- **Adjust difficulty**: weight the keeper's zone selection (e.g. favor the center) instead of uniform random.
- **Add sound effects**: crowd cheer on goal, whistle on save.
- **Add shot power/curve controls**: let the player adjust ball trajectory before shooting.
- **Multiplayer mode**: alternate turns between two players and compare scores.
- **Persist scores**: add a Flask route + simple database to save high scores across sessions.

## File Reference

### `app.py`
Minimal Flask server with a single route (`/`) that renders `templates/index.html`.

### `templates/index.html`
Contains:
- Bootstrap-based layout (navbar, status bar, game card, aim controls, result modal)
- Inline `<script>` block with all Three.js scene setup, animation loop, and game state logic (no external JS files)

## License

Free to use and modify for learning, demos, or personal projects.
