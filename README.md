# Forgeclicker 

**Forgeclicker** is my submission for a technical assignment where the goal is to create a game centered around a button and to make clicking that button feel as juicy, satisfying, and polished as possible.

Instead of simply adding visual or sound effects, I chose to create a simple yet creative experience where the press of a single button starts a satisfying production chain: mining, smelting, forging, and selling gear to earn upgrades. The more you click, the faster you mine and the more rewards you earn, so smash that button to your heart's content!

---

## Controls

**This game features two control modes:**

- **Cursor Mode**  
  - Default mode: Enables the mouse cursor letting you interact with the UI and press the central button using  <img src="ReadMeResources/mouse_left.png" width="30"/>. 
  
- **Movement Mode**  
  - Hold <img src="ReadMeResources/mouse_right.png" width="30"/> to switch into movement mode.  
  - While holding <img src="ReadMeResources/mouse_right.png" width="30"/>:
    - Use <img src="ReadMeResources/keyboard_w.png" width="30"/><img src="ReadMeResources/keyboard_a.png" width="30"/><img src="ReadMeResources/keyboard_s.png" width="30"/><img src="ReadMeResources/keyboard_d.png" width="30"/> to move
    - Move <img src="ReadMeResources/mouse_move.png" width="30"/> to rotate the camera

---

## How to Play
Just smash the big central button!
- Each click triggers a pickaxe swing at the mining site.
- Every few swings produce ore that travels on a conveyor belt to the furnace.
- Ores are smelted into ingots, which then continue to the forge.
- At the forge, ingots are processed into gear based on their type (iron swords, golden shields, diamond armor).
- Selling gear earns you currency to unlock new ore types and purchase upgrades.
- There are multiple environmental effects making the experience more satisfying and immersive for example try standing near the mining site while clicking and you'll feel the screen shake from the impact!
 
---

## Main Features
Rather than relying solely on VFX or SFX to create juiciness, I focused on making each button click meaningful and rewarding. Every press contributes to a chain of visual and systemic feedback, from ore production to gear crafting. Watching your efforts physically move through a system, evolve, and pay off as upgrades makes the experience rewarding in a satisfying way. The more you smash that button, the more your earn ! Multiple Vfx and Sfx elements have also been designed and implemented to add immersiveness and juiciness to the gameplay like impact sparks, furnace flames, smoke, different mining audios...

- A fully animated, juicy central button that starts a full production chain.
- A multi-stage factory system:
  - **Mining Site** → **Furnace** → **Forge**
- Dynamic conveyor belts that visually deliver materials across the map.
- Unlockable ore types:
  - Iron, Gold, Diamond 
- Gear types: swords, shields, armor, automatically crafted from smelted ingots.
- Currency system tied to gear sales.
- Upgrades:
  - **Speed Up**: increases conveyor belt speed.
  - **Size Up**: comically increases button size for over-the-top satisfaction.

---
## Project Structure
🔹 1. The project uses BP_GameState as a centralized controller for gameplay logic and cross-system communication. It acts as a high-level mediator between the UI and gameplay actors.
UI interactions pass through the GameState, which then routes the relevant information to the appropriate actor.
This design keeps all major systems decoupled and independent: Mining Site, Furnace, Forge, and other actors hold no references to UI or each other. They only communicate with the GameState via Event Dispatchers.

🔹 2. A major architectural decision I made was adopting a data table–driven recipe system. Instead of hardcoding inputs and outputs in the Furnace or Forge: Each recipe (eg Iron Ore → Iron Ingot → Iron Sword) is stored as a row in a DataTable. Machines read from these tables and act accordingly. This enhances the project's scalability avoiding if/else repetitions and allowing for easy extensions for future new ore additions.

🔹 3. The same data-driven philosophy powers the UI system:
Upgrade buttons (like “Speed Up” or ore unlocks) are built dynamically from DataTables.
This makes the UI auto-extending:
To add a new upgrade, I just insert a row in the data table and the UI will build itself, no changes to the UI blueprint are required.

##  Optimization
 1. Object Pooling Design Pattern
Instead of spawning and destroying actors at runtime, I used a custom Object Pooling Component.
Items like ores, ingots, and gear are reused from a class-based pool. They are called when needed and returned to the pool effectively hiding and disabling them instead of destroyed only to be recreated again.
This reduces memory churn and avoids costly garbage collection cycles.

 2. DataTable-Driven Systems
The DataTable design was a life-saver during my work on Forgeclicker. It greatly enhances the project's scalability and modularity making the extension of gameplay as easy as creating a new data table row.

 3. Event-Driven Design
Event Dispatchers are used extensively for all inter-system communication:
Systems are reactive and most actors do not rely on Tick to update. GameState acts as an event router, invoking functionality only when needed keeping CPU usage low.

## [Play the game or watch the demo video on Google Drive!](https://drive.google.com/drive/folders/1AWWP3TOk2nXVlMQepD7KZb3-zbzvGOfd?usp=drive_link) Have Fun !!


