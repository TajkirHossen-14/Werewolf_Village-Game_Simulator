<div align="center">
<p align="center">
  <img src="Assets/Banner/WVGS Banner 2.png" alt="Werewolf Village – Game Simulator Banner" width="100%">
</p>
 
*A peaceful village is hiding a dangerous secret...*

Among the villagers, two players are secretly Werewolves. Every night, the Werewolves
silently attack a villager. During the day, the villagers try to guess who the Werewolves
are and vote to remove the suspect. The villagers know that danger exists – but they do
not know who the Werewolves are. The game continues until both Werewolves are eliminated,
or the Werewolves equal or outnumber the remaining Villagers.

> A text-based **Werewolf** game simulation built in Python.

</div>

<img src="https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/colored.png" width="100%"/>
 
## 📸 Sample Output
 
```
 ---- WEREWOLF GAME START ----
 
[ Day :  1 ]
 
< Night Phase >
Shome was attacked.
 
< Day Phase >
Ronaldo was voted out.
____________________
 
[ Day :  2 ]
 
< Night Phase >
Custom Event : Dense fog covered the village.
Werewolves got lost and attacked nobody.
 
< Day Phase >
Nahid was voted out.
____________________
 
Winner :  Villagers
 
Result saved into result.txt
```
 
---
 
## 📁 Project Structure
 
```
Werewolf_Village-Game_Simulator/
│
├── Werewolf Game Simulator/
│    ├── Werewolf_Game.ipynb         # Main notebook — All code lives here
│    ├── players.txt                 # Input  — One player name per line
│    ├── result.txt                  # Output — Game result (Auto-generated after each run)
│    └── WVGS Code [Text].txt
│
├── Assets/
└── README.md
```
 
---
 
## 🎮 How the Game Works
 
### Roles
 
| Role | Count | Goal |
|---|---|---|
| 🧑 **Villager** | All except 2 | Find and vote out both werewolves |
| 🐺 **Werewolf** | 2 | Outnumber or equal the remaining villagers |
 
### Win Conditions
 
- 🎉 **Villagers Win** – Both werewolves are eliminated
- 🐺 **Werewolves Win** – Werewolves are equal to or outnumber remaining villagers

### Game Flow

<!--
Game Start
    │
    ▼
🌙 Night Phase
    ├── Roll random event (1–10)
    ├── If event = 1 → Dense Fog    (Nobody is attacked)
    ├── If event = 2 → Lucky Escape (Target survives)
    └── Otherwise    → Werewolves eliminate a random villager
    │
    ▼
Check Winner → if Yes, END
    │
    ▼
☀️ Day Phase
    └── Village randomly votes out one alive player
    │
    ▼
Check Winner → if Yes, END
    │
    └──── Repeat ────┘
-->

<img src="Assets/Game Flow/WVGS - Game Flow.png" alt="Game Flow" width="85%">
 
---
 
## ✨ Features
 
| Feature | Details |
|---|---|
| 🎭 **2 Classes** | `Player` and `Game` |
| ⚙️ **10 Methods** | Across both classes (see breakdown below) |
| 📂 **File Reading** | Player names read from `players.txt` |
| 📝 **File Writing** | Game result saved to `result.txt` |
| 🎲 **Random Module** | Role assignment, night attacks, day votes, event rolls |
| 📋 **List of Objects** | `self.players` – A list of `Player` instances |
| 🔁 **Loop Gameplay** | `while True` loop drives the full game |
| 🌫️ **Custom Event 1** | **Dense Fog** – Werewolves get lost, nobody is attacked |
| 🍀 **Custom Event 2** | **Lucky Escape** – The chosen victim escapes the attack |
 
---
 
## 🏗️ Code Overview
 
### `Player` Class
 
Represents a single player in the game.
 
```python
class Player:
    def __init__(self, name):
        self.name  = name          # Player's name
        self.role  = "Villager"    # Default role
        self.alive = True          # Alive status
```
 
| Method | Description |
|---|---|
| `make_werewolf()` | Changes the player's role to `"Werewolf"` |
| `eliminate()` | Sets `alive = False` |
| `__str__()` | Returns a formatted string like `Alex (Villager) - Alive` |
 
---
 
### `Game` Class
 
Controls the full game – Setup, phases, events, win check, and file I/O.
 
```python
class Game:
    def __init__(self, filename):
        self.players   = []     # List of Player objects
        self.day_count = 1
        self.load_players(filename)
        self.assign_werewolves()
```
 
| Method | Description |
|---|---|
| `load_players(filename)` | Reads names from the text file and builds `Player` objects |
| `assign_werewolves()` | Randomly selects 2 players and sets their role to Werewolf |
| `alive_players()` | Returns a list of all players still alive |
| `alive_werewolves()` | Returns alive players whose role is `"Werewolf"` |
| `alive_villagers()` | Returns alive players whose role is `"Villager"` |
| `night_phase()` | Rolls a random event; werewolves attack a random villager |
| `day_phase()` | Village randomly votes out one alive player |
| `check_winner()` | Returns `"Villagers"`, `"Werewolves"`, or `None` |
| `save_result(winner)` | Writes the winner and all player statuses to `result.txt` |
| `start_game()` | Main loop – runs Night → Day until a winner is found |
 
---
 
## 🎲 Custom Events
 
Both events are triggered inside `night_phase()` using `random.randint(1, 10)`.
 
### 🌫️ Event 1 – Dense Fog  *(1 in 10 chance)*
> *"Dense fog covered the village. Werewolves got lost and attacked nobody."*
 
- The werewolves attempt to move but get completely lost in the fog
- No villager is eliminated that night
- The day phase still follows normally
### 🍀 Event 2 – Lucky Escape  *(1 in 10 chance)*
> *"Lucky Escape! [name] escaped from the attack."*
 
- A victim is randomly chosen as usual
- At the last moment, they manage to escape
- The player survives and the night ends with no elimination
---
 
## 💾 File Format
 
### `players.txt` (Input)
One player name per line. Minimum 4 players recommended.
 
```
Akbar
Hamza
Tajkir
Hamid
Shome
Messi
Ronaldo
Nahid
```
 
### `result.txt` (Output)
Auto-generated at the end of every game run.
 
```
Werewolf Game Result
--------------------
Winner : Villagers
 
Final Player Status :
Akbar (Villager) - Dead
Hamza (Werewolf) - Dead
Tajkir (Villager) - Alive
Hamid (Werewolf) - Dead
Shome (Villager) - Dead
Messi (Villager) - Alive
Ronaldo (Villager) - Alive
Nahid (Villager) - Dead
```
 
---
 
## 🚀 Getting Started
 
### Prerequisites
- Python 3.x (No external libraries needed)
### Run the Game
 
```bash
# 1. Clone the repository
git clone https://github.com/TajkirHossen-14/Werewolf_Village-Game_Simulator.git
cd Werewolf_Village-Game_Simulator
 
# 2. Make sure players.txt exists with at least 4 names
 
# 3. Open the notebook
jupyter notebook Werewolf_Game.ipynb
```
 
### Use Your Own Player Names
 
Just edit `players.txt` before running – One name per line:
 
```
Name1
Name2
Name3
Name4
...
```
 
---
 
## 📊 Requirements Coverage
 
| Requirement | Status | Where in Code |
|---|---|---|
| At least 2 classes | ✅ | `Player`, `Game` |
| At least 4 methods | ✅ | 10 methods total across both classes |
| File reading | ✅ | `load_players()` reads `players.txt` |
| File writing | ✅ | `save_result()` writes `result.txt` |
| Random module | ✅ | `random.sample()`, `random.choice()`, `random.randint()` |
| List of objects | ✅ | `self.players` – list of `Player` instances |
| Loop-based gameplay | ✅ | `while True` loop in `start_game()` |
 
---
 
## 🛠️ Tech Stack
 
![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat&logo=python&logoColor=white)
 
- **Language :** Python 3
- **Libraries :** `random` (Built-in only – no external dependencies)

