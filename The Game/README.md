# 🎮 The Game — TryHackMe Challenge Writeup

> Room: [The Game](https://tryhackme.com/room/hfb1thegame)
> Difficulty: Easy  
> Type: Reverse Engineering / CTF

---

## 📝 Challenge Brief

> Cipher has gone dark, but intel reveals he’s hiding critical secrets inside Tetris, a popular video game. Hack it and uncover the encrypted data buried in its code.

We were given a standalone `.exe` game file (no source, no engine info) and tasked with locating a flag hidden within it.

---

## 🧠 Initial Thoughts

The lack of context pointed toward one of three likely approaches:
- Reverse engineering with a disassembler/debugger (e.g., Ghidra, IDA, x64dbg)
- Static string extraction
- File structure analysis or unpacking

Given the simplicity of the challenge and time constraints, I went with the most direct route first.

---

## 🛠️ Method Used: Strings-Based Recon

Using Windows PowerShell:

```powershell
strings .\Tetrix.exe > extracted.txt
strings .\extracted.txt | findstr "THM"
