# 🧩 Godot Tetris Game – TryHackMe Challenge Writeup

> Room: [The Game](https://tryhackme.com/room/hfb1thegamev2)
> Difficulty: Easy
> Type: Reverse Engineering / Game Modding  

---

## 📝 Challenge Summary

We were given an executable of a Tetris-style game created with the **Godot Engine**. The challenge hinted at encrypted or hidden data embedded in the gameplay. Our goal was to locate and reveal a secret flag.

> *"The game is never over."*

---

## 🛠️ Tools Used

- 🧩 **GDRE Tools** – To extract the `.pck` contents and recover the full Godot project  
- 🕹 **Godot Engine** – To open, edit, and rebuild the recovered game   
- 🔍 `strings` – Used in early recon

---

## 🔍 Step-by-Step Breakdown

### 1. Identify the Game Engine

The game displayed a robot-face logo, which hinted at the **Godot Engine**. This immediately narrowed the toolset I needed for further inspection.

---

### 2. Extract and Recover the Project

Godot executables bundle assets into `.pck` files. I used the **GDRE Tools** to:

- Extract the `.pck` data from the game executable
- Recover the Godot project structure
- Load it into the **Godot Engine** for inspection

---

### 3. Analyze Game Logic

Inside the recovered project, a script file: `gui.gd`. It contained this score-checking logic:

```gdscript
if score >= 999999:
    var a_node = get_node("A")
    if a_node:
        a_node.visible = true
```

a simple change in logic to always pass:

```
if score >= 0:
    var a_node = get_node("A")
    if a_node:
        a_node.visible = true
```
