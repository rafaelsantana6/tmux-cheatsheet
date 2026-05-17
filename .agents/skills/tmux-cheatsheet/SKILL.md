---
name: tmux-cheatsheet
description: "Use when the user asks how to use Rafael's personal tmux configuration, tmux shortcuts, panes, windows, sessions, copy mode, or the Tmux Cheatsheet web app. Answers must be based on Rafael's current keybindings: Ctrl+Space prefix, Alt window/session navigation, Ctrl+Alt pane navigation, and vi copy mode."
---

# Tmux Cheatsheet Skill

Use this skill to answer questions about Rafael's tmux setup and to give practical commands based on his actual configuration.

## Source of truth

Rafael's current tmux config was read from:

- `~/.config/tmux/tmux.conf`
- tmux version observed: `tmux 3.6a`
- static cheatsheet page: `~/tutorial-tmux.html`
- published site, if available: GitHub Pages for this repository

If the user asks whether the config changed, inspect `~/.config/tmux/tmux.conf` before answering.

## Mental model

- **Session**: workspace inteiro que pode continuar rodando em segundo plano.
- **Window**: aba dentro da sessão.
- **Pane**: divisão da tela dentro de uma janela.

Example structure:

```text
Sessão: trabalho
  Janela 1: editor
    Pane 1: nvim
    Pane 2: servidor
  Janela 2: git
  Janela 3: logs
```

## Prefix keys

Rafael's prefix keys:

- Primary: `Ctrl+Espaço`
- Secondary/traditional: `Ctrl+b`

When explaining `Prefix + x`, say: press `Ctrl+Espaço`, release, then press `x`.

## Essential commands

### Starting and returning

```bash
tmux new -s trabalho
tmux ls
tmux attach -t trabalho
tmux kill-session -t trabalho
```

- `Prefix + d`: detach without killing processes.

### Windows

| Shortcut | Action |
|---|---|
| `Prefix + c` | new window in current directory |
| `Prefix + r` | rename window |
| `Prefix + k` | kill current window |
| `Alt + 1..9` | select window by number |
| `Alt + ←/→` | previous/next window |
| `Alt + Shift + ←/→` | move current window left/right |

Notes:

- `base-index` is `1`, so the first window is window `1`.
- Windows are automatically renamed from the current path.

### Panes

| Shortcut | Action |
|---|---|
| `Prefix + h` | split top/bottom (`split-window -v`) |
| `Prefix + v` | split side-by-side (`split-window -h`) |
| `Prefix + x` | kill current pane |
| `Ctrl + Alt + Setas` | move focus between panes |
| `Ctrl + Alt + Shift + Setas` | resize panes by 5 cells |

### Sessions

| Shortcut | Action |
|---|---|
| `Prefix + R` | rename session |
| `Prefix + C` | create new session in current directory |
| `Prefix + K` | kill current session |
| `Prefix + P` | previous session |
| `Prefix + N` | next session |
| `Alt + ↑/↓` | previous/next session without prefix |

### Copy mode

Rafael uses vi copy mode.

| Shortcut | Action |
|---|---|
| `Prefix + [` | enter copy mode |
| `h j k l` | navigate like Vim |
| `/` | search forward |
| `?` | search backward |
| `n` / `N` | next/previous match |
| `v` | begin selection |
| `y` | copy selection and exit |
| `q` | quit copy mode |

### Config reload

- `Prefix + q`: reload `~/.config/tmux/tmux.conf` and display “Configuration reloaded”.
- Equivalent command:

```bash
tmux source-file ~/.config/tmux/tmux.conf
```

## Recommended workflow

For a beginner using Rafael's config:

```bash
tmux new -s dev
```

1. `Prefix + c` to create a new window.
2. `Prefix + r` to rename it, e.g. `editor`, `git`, or `logs`.
3. `Prefix + v` to split side-by-side.
4. `Ctrl+Alt+←/→` to move between panes.
5. `Alt+1` / `Alt+2` to move between windows.
6. `Prefix+d` to detach.
7. `tmux attach -t dev` to return.

## Answering style

- Answer in Portuguese unless the user asks otherwise.
- Prefer Rafael's custom shortcuts over tmux defaults.
- Mention destructive shortcuts clearly: `Prefix+x`, `Prefix+k`, and `Prefix+K` close pane/window/session.
- For beginner questions, give one short explanation plus the exact key sequence.
- If asked to change tmux config, inspect `~/.config/tmux/tmux.conf`, edit safely, then reload with `Prefix+q` or `tmux source-file ~/.config/tmux/tmux.conf`.
