# Tmux Cheatsheet do Rafael

Este repositório publica um cheatsheet estático para consultar os atalhos de tmux configurados em `~/.config/tmux/tmux.conf`.

- Página HTML: `index.html`
- Skill para agentes: `.agents/skills/tmux-cheatsheet/`
- Config base: tmux `3.6a`, prefix principal `Ctrl+Espaço`, prefix secundário `Ctrl+b`

## Conceitos básicos

| Conceito | O que é |
|---|---|
| Sessão | Um workspace inteiro do tmux. Pode continuar rodando em segundo plano. |
| Janela | Como uma aba dentro da sessão. Boa para separar editor, git, logs e servidor. |
| Pane | Divisão da tela dentro de uma janela. Ideal para comandos lado a lado. |

Exemplo:

```text
Sessão: trabalho
  Janela 1: editor
    Pane 1: nvim
    Pane 2: servidor
  Janela 2: git
  Janela 3: logs
```

## Abrir, sair e voltar

```bash
tmux new -s trabalho
```

Listar sessões:

```bash
tmux ls
```

Voltar para uma sessão:

```bash
tmux attach -t trabalho
```

Matar uma sessão pelo terminal:

```bash
tmux kill-session -t trabalho
```

Sair sem matar processos:

```text
Prefix + d
```

## Prefix

O prefix principal é:

```text
Ctrl + Espaço
```

O prefix alternativo é:

```text
Ctrl + b
```

Quando este guia diz `Prefix + c`, aperte `Ctrl+Espaço`, solte, depois aperte `c`.

## Janelas

| Atalho | Ação |
|---|---|
| `Prefix + c` | Criar nova janela no diretório atual |
| `Prefix + r` | Renomear janela |
| `Prefix + k` | Fechar janela atual |
| `Alt + 1..9` | Ir direto para janela pelo número |
| `Alt + ←/→` | Janela anterior/próxima |
| `Alt + Shift + ←/→` | Mover janela para esquerda/direita |

A configuração usa `base-index 1`, então a primeira janela é `1`, não `0`.

## Panes

| Atalho | Ação |
|---|---|
| `Prefix + h` | Dividir em cima/baixo (`split-window -v`) |
| `Prefix + v` | Dividir lado a lado (`split-window -h`) |
| `Prefix + x` | Fechar pane atual |
| `Ctrl + Alt + Setas` | Navegar entre panes |
| `Ctrl + Alt + Shift + Setas` | Redimensionar panes de 5 em 5 células |

## Sessões

| Atalho | Ação |
|---|---|
| `Prefix + R` | Renomear sessão |
| `Prefix + C` | Criar nova sessão no diretório atual |
| `Prefix + K` | Matar sessão atual |
| `Prefix + P` | Sessão anterior |
| `Prefix + N` | Próxima sessão |
| `Alt + ↑/↓` | Sessão anterior/próxima sem prefix |

## Modo cópia / scroll

A configuração usa modo vi:

```tmux
setw -g mode-keys vi
```

| Atalho | Ação |
|---|---|
| `Prefix + [` | Entrar no modo cópia |
| `h j k l` | Navegar como no Vim |
| `/` | Buscar para frente |
| `?` | Buscar para trás |
| `n` | Próxima ocorrência |
| `N` | Ocorrência anterior |
| `v` | Começar seleção |
| `y` | Copiar seleção e sair |
| `q` | Sair do modo cópia |

## Mouse

A configuração contém:

```tmux
set -g mouse on
```

Isso permite clicar em panes, clicar em janelas na barra, rolar o histórico e redimensionar panes com o mouse.

## Recarregar configuração

```text
Prefix + q
```

Alternativa pelo terminal:

```bash
tmux source-file ~/.config/tmux/tmux.conf
```

## Fluxo recomendado

```bash
tmux new -s dev
```

1. `Prefix + c`: crie uma janela nova.
2. `Prefix + r`: renomeie para `editor`, `git` ou `logs`.
3. `Prefix + v`: divida lado a lado.
4. `Ctrl + Alt + ←/→`: alterne entre panes.
5. `Alt + 1/2`: alterne entre janelas.
6. `Prefix + d`: saia sem matar nada.
7. `tmux attach -t dev`: volte depois.

## Cheat sheet rápido

| Categoria | Comando |
|---|---|
| Prefix | `Ctrl+Espaço` ou `Ctrl+b` |
| Nova janela | `Prefix+c` |
| Renomear janela | `Prefix+r` |
| Fechar janela | `Prefix+k` |
| Ir para janela | `Alt+1..9` |
| Dividir cima/baixo | `Prefix+h` |
| Dividir lado a lado | `Prefix+v` |
| Fechar pane | `Prefix+x` |
| Navegar panes | `Ctrl+Alt+Setas` |
| Redimensionar panes | `Ctrl+Alt+Shift+Setas` |
| Modo cópia | `Prefix+[` |
| Selecionar/copiar | `v`, depois `y` |
| Recarregar config | `Prefix+q` |
| Desanexar | `Prefix+d` |
