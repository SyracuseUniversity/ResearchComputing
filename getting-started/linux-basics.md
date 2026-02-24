---
layout: default
title: Linux CLI Basics
parent: Getting Started
nav_order: 3
---

# Linux Command Line Basics

The clusters run Linux and use a command-line interface. There's no clicking, no windows - just commands.

---

## Essential Commands

| Command | What It Does | Example |
|:--------|:-------------|:--------|
| `pwd` | Print working directory (where am I?) | `pwd` |
| `ls` | List files in current directory | `ls -l` (detailed list) |
| `cd` | Change directory | `cd my_project` |
| `mkdir` | Make a new directory | `mkdir results` |
| `cp` | Copy files | `cp script.py backup.py` |
| `mv` | Move or rename files | `mv old.txt new.txt` |
| `rm` | Remove files | `rm temp.txt` |
| `cat` | Display file contents | `cat output.txt` |
| `nano` | Simple text editor | `nano script.py` |

---

## File Paths

- `/home/netid/` - Your home directory
- `.` - Current directory
- `..` - Parent directory
- `~` - Shortcut for your home directory

---

## Navigation Example
```bash
# Navigate to home
cd ~

# Create a project directory
mkdir my_research
cd my_research

# List all files including hidden ones
ls -la

# Go up one directory
cd ..
```

---

## Editing Files

Use `nano` for simple text editing:
```bash
nano my_script.py
# Edit your file, then:
# Ctrl+O to save
# Ctrl+X to exit
```
