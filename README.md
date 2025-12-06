# Candy Crush — Semester 1 Project

A simple Candy Crush–style match-3 game implemented in C++ using SFML.  
This project is a semester assignment that implements core match-3 mechanics (matching, special candies, cascades), a start menu, save/load, and a simple UI.

---

## Table of Contents
- About
- Features
- How it works (brief)
- Requirements
- Build & Run
- Controls
- Save / Load
- File / Asset layout
- Known issues & TODO
- License & Credits

---

## About
This is a desktop clone of Candy Crush written in C++ with SFML for graphics and input. The board is a 9×9 grid of candies with multiple special candies supported:
- Striped candies (horizontal / vertical)
- Wrapped candies (3×3 explosion)
- Color bomb (removes or converts candies)
Special interactions (striped + wrapped, color bomb combos, etc.) are handled in the game logic.

---

## Features
- Match-3 detection with cascade processing
- Creation of special candies for matches of length 4+ and L/T shapes
- Special-candy interactions (striped + striped, wrapped + wrapped, color bomb interactions)
- Save and load game state to/from `game_save.txt`
- Start screen with Play / Load / Exit
- In-game UI: Score, Moves left, Target
- Simple end-game screen (Win / Game Over)
- Assets-based sprites and fonts for visuals

---

## How it works (brief)
- The board is represented by a 2D array of `Candy` structs (color, special, stripeDir).
- Matches are detected horizontally and vertically; L/T shapes create wrapped candies.
- Specials are placed at match centers and marked so they won't be removed.
- After removals, the board refills and the engine checks for new matches (cascade).
- Save file format: each board row is written as tokens (asset file names or single color letters) separated by spaces, followed by a final line containing `score movesLeft`. Example token: `R`, `S-B-H`, `C`, etc.

---

## Requirements
- C++17 compatible compiler (g++, clang++, MSVC)
- SFML 2.5+ (Graphics, Window, System)
- Assets (images and fonts) in an `assets/` folder (see layout below)

---

## Build & Run

Linux / macOS (example with g++)
1. Install SFML (package manager / build from source).
2. From project root:
   g++ -std=c++17 main.cpp -o CandyCrush -lsfml-graphics -lsfml-window -lsfml-system
3. Ensure `assets/` is next to the executable and run:
   ./CandyCrush

Windows (MinGW)
1. Install SFML and configure include/lib paths.
2. Example:
   g++ -std=c++17 main.cpp -o CandyCrush.exe -lsfml-graphics -lsfml-window -lsfml-system
3. Place `assets/` next to the .exe and run.

IDE (Visual Studio, CLion, Code::Blocks)
- Create a project, add `main.cpp`, and link SFML libraries (Graphics, Window, System).
- Ensure runtime finds the `assets/` folder.

Note: The file name in the code is `main.cpp` (or whatever your file is named). Adjust build commands if there are additional source files.

---

## Controls
- Mouse click on a candy to select it. Click an adjacent candy to swap.
- Home button — return to start screen (starts a new game if you press Play again).
- Save button — writes current state to `game_save.txt`.
- Load button (start screen or end screen) — loads a saved game and resumes.
- Quit/Exit — close the game.

Win condition: reach score 5000 before running out of moves (default maxMoves = 20).

---

## Save / Load
- Save file path (relative): `game_save.txt`
- Format:
  - First 9 lines: board rows, tokens separated by spaces (each token maps to an asset name or single color letter)
  - Final non-empty line: "<score> <movesLeft>"
- Example tokens: `R G B Y O S-B-H W-G C`
- Use the Load button on the start screen (or the end screen) to restore the saved state.

---

## File / Asset layout
A suggested repository layout:
- main.cpp (game source)
- README.md (this file)
- assets/
  - red-candy.png
  - green-candy.png
  - blue-candy.png
  - yellow-candy.png
  - orange-candy.png
  - S-*-H/V.png (striped)
  - W-*.png (wrapped)
  - C.png (color bomb)
  - start.png, bg1.png, end.png (background images)
  - play_optimized.png, load_optimized.png, quit_optimized.png (menu buttons)
  - home.png, save.png, exit.png (in-game buttons)
  - Lobster-Regular.ttf, ALBAS___.ttf (fonts)
- game_save.txt (created when saving)

Make sure the `assets/` folder contains all files referenced in the source or the game will fail to load textures/fonts.

---

## Known issues & TODO
- No sound effects; consider adding SFML audio support.
- Collision / animation smoothing is basic; candy movement is instant (no animated swaps).
- The save file format is simple and fragile — could switch to JSON for robustness.
- Some special-combo interactions may not match official Candy Crush behavior exactly.
- Add unit tests and CI (GitHub Actions) for builds.
- Improve window resizing / layout to be responsive.

---

## Contributing
- Feel free to open issues and pull requests.
- When adding assets or code, keep images organized in `assets/` and update README with any new files or changes.
- If adding features, provide a short description and test instructions in the PR.

---

## Credits
- Project author: Ahmad-Arif-584
- SFML: https://www.sfml-dev.org/
- Any art/font assets used should be checked for license and credited accordingly.

---

