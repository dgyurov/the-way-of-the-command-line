---
theme: ./.themes/dracula.json
author: Dimitar Gyurov | MMM24
date: dd/MM/YYYY
paging: Page %d / %d
---

# The Way of the Command Line
Taking Full Advantage of Your Terminal as a Mobile Engineer

---

## Agenda for today
0. Introduction
1. Developer Experience is more than just a buzzword
2. Recipe: Make the Command Line yours
3. Collection of tools
4. Leveling up with TUIs
5. Making your own TUIs
6. Take away from today and some additional tips
7. Questions and Answers

---

## 0. Introduction

> There are 10 types of software engineers. Those that want to spend as much time as possible in the terminal and those that don't.

___ 
- Why `Developer Experience` is important?
___
- Does better `Developer Experience` make us happier?
___
- How does `Developer Experience` extend to the command line?
___
- How can we improve our `Developer Experience` in the terminal?

---

## 1. Developer Experience is more than just a buzzword

___

- Developers who report **fast feedback** times feel `20% more innovative`.
___
- Developers who carve out significant time for **deep work** enjoy a `50% productivity boost`.
___
- Developers who have **intuitive processes** feel they are `50% more innovative`.
___
- Developers who find their work **engaging** feel `30% more productive`.

___
```bash
# From "DevEx in Action: A study of its tangible impacts" - GitHub Next - 2024 [1]
```
---

### How does `Developer Experience` extend to the command line?
___
- The command line provides **instant feedback**.
___
- A simpler environment can have a positive effect on **being in The Flow**.
___
- Integration between tools in the command line can be **very intuitive**.
___
- Personalization can make the command line a lot **more engaging**.

---

## 2. Recipe: Make the Command Line yours

#### Ingredients
- 1 Terminal emulator
- 1 Shell
- 1 Modern prompt
- 1 Terminal multiplexer (Optional, but recommended) 
- Season with configuration to taste

#### Instructions
1. Choose a terminal emulator
2. Choose a shell
3. Enhance your shell
4. Choose a prompt
5. Choose a multiplexer

---

### Choose a terminal emulator

| Feature | Terminal•app | Alacritty | Kitty | WezTerm |
| ------- | ------- | ------- | ------- |------- |
| Tabs/ Splits support | ✅|🔴|✅|✅|
| Hardware accelerated | 🔴|✅|✅|✅|
| Performance oriented | 🔴|✅|✅|✅|
| Personalization Focused | 🔴|✅|✅|✅|
| Easily Scriptable | 🔴|🔴|✅|✅|
| Can display images | 🔴|🔴|✅|✅|
| Comes with a multiplexer | 🔴|🔴|🔴|✅|

___

- Terminal.app
- `Alacritty` [→](https://alacritty.org)
- Kitty [→](https://sw.kovidgoyal.net/kitty/)
- WezTerm [→](https://wezfurlong.org/wezterm/)

---

### Choose a shell
| Feature | zsh | fish | bash
| ------- | ------- | ------- | ------- |
| Default (since macOS Catalina) | ✅|🔴|🔴|
| Support for auto-completion | 🟡 |✅|🟡 |
| Support for auto-suggestions | 🟡 |✅|🟡 |
| Easily Customizable | ✅|✅|🟡|
| Actively developed | ✅|✅|🟡|
| Familiar scripting language | 🟡|🔴|✅|
| Compatibility with CLI tools | ✅|🟡|✅|

- `zsh` [→](https://www.zsh.org/)
- fish [→](https://fishshell.com/)
- bash [→](https://gnu.org/software/bash)

---

### Enhance your shell

Frameworks for managing zsh/bash plugins, themes and configurations.
- `ohmyzsh` [→](https://ohmyz.sh)
- ohmybash [→](https://ohmybash.github.io/)

Plugin package manager for ZSH. Simplifies plugin installation.
- `antigen` [→](https://antigen.sharats.me)

```bash
antigen use oh-my-zsh
antigen bundle git
antigen bundle macos
antigen bundle brew
antigen bundle tmux
antigen bundle zsh-users/zsh-autosuggestions
antigen apply
```

---

### Choose a prompt
Prompt applications help you with the following:
- Support for different prompt layout on success/error
- Can display the status of a git repo if you are in one
- Option to display the version of language runtimes
- Full control over which characters are printed on each prompt
- Support for multiline prompts
___
Couple of well maintained prompt apps:
- `starship` [→](https://starship.rs)
- powerlevel10k [→](https://github.com/romkatv/powerlevel10k)
- promptline [→](https://github.com/edkolev/promptline.vim)

---

### Choose a multiplexer

Multiplexers can be extremely valuable and generally provide:
- Multiple terminal sessions in a single window
- Detach from and reattach to existing sessions
- **Persistent sessions!**
- Support for tab/splits
- Keyboard/ shortcut centric
___

- `tmux` [→](https://github.com/tmux/tmux)
- Zellij [→](https://zellij.dev/)
- WezTerm [→](https://wezfurlong.org/wezterm/)

---

## 3. Collection of tools

- zoxide
- fzf
- ripgrep
- fd
- bat
- delta

---

### zoxide

A better `cd` command, inspired by z.
- Keeps track of the most frequently visited directories.
- Jumps to the closest visited directory matching a string.
- Supports interactive selection.

```bash
z foo              # cd into highest ranked directory matching foo
z foo bar          # cd into highest ranked directory matching foo and bar
z foo /            # cd into a subdirectory starting with foo
z ~/foo            # z also works like a regular cd command
z ..               # cd one level up
z -                # cd into previous directory
```

[→](https://github.com/ajeetdsouza/zoxide)

---

### fzf

A powerful command-line fuzzy finder that will make you forget about the TAB key.

```
~~~graph-easy --as=boxart
[ STDIN\n Input lines ] - fzf -> [ STDOUT\n User Selection ]
~~~
```
___

```bash
ls | fzf | xargs wc                                    # Get the word count of a file
find * | fzf | xargs md5sum                            # Get the checksum of a file
git ls-files | fzf | xargs git log                     # See the history of a git file
ps -ef | sed 1d | fzf | awk '{print $2}' | xargs kill  # Kill a proccess
```

[→](https://junegunn.github.io/fzf/)

---

### ripgrep

Search tool that recursively searches the current directory for a regex pattern.
- 10 to 30 times faster than `grep`.
- Supports highlighting.
- Respects gitignore and dotfiles by default.
- Integrates really well with other modern tools like `fzf` and `fd`.
___
```bash
# Let's see it in action
grep -r 'dart'
rg dart
```

[→](https://github.com/BurntSushi/ripgrep)

---

### fd

A simpler and faster alternative to `find`.

- Up to 20 times faster.
- Regex support by default.
- Personally, I find the syntax more intuitive.
- Can run commands for each result in parallel.
- Friendly towards gitignore and hidden files.
- Supports highlighting as well.

___
```bash
fd -e swift
fd -e swift -x wc | sort
fd -e swift -x wc | awk '{sum+=$1} END {print sum}'
```

[→](https://github.com/sharkdp/fd)

---

### bat

A `cat` clone with wings. 

- Code highlighting.
- Integration with git status.
- Automatic pagination.
- Support for line numbers.

[→](https://github.com/sharkdp/bat)

---

### delta

A modern diff-viewer in your terminal.

- Fantastic integration with `bat`.
- Supports side-by-side comparison with line wrapping.
- Can emulate `diff-so-fancy`.
- Extremely customizable.

[→](https://github.com/dandavison/delta)

---

## 4. Leveling up with TUIs
- lazygit
- nnn
- gum

---

### lazygit

A fully-featured interactive git TUI. A great middle ground if you want to switch from a GUI based git client.

[→](https://github.com/jesseduffield/lazygit)

---

### nnn

> n³ The unorthodox terminal file manager

A fully-featured TUI terminal file manager.
- Comes with batteries included
- Cross-platform
- Supports editor-based batch renaming

[→](https://github.com/jarun/nnn)

---

### gum

A library of TUI components that can be used in bash scripts.

Some of the components included:
- Confirmation dialog
- Fuzzy finder
- Input prompt
- Text are input
- File picker
- Pager
- Loading indicator
- Tables

[→](https://github.com/charmbracelet/gum)

---

## 5. Making your own TUIs
**Couple of demo use-cases:**

- `ib` - TUI tool chain for common actions for our InsideBusiness project.
___
- `pr` - Azure pull request integration in the terminal.
___
- `story` - Azure Backlog Story creation in the terminal.
___
- `mods` - My personal assistant.

---

## 6. Take away from today and some additional tips
`Personalize` your terminal to your taste. It pays off in the long run.
___
Focus on mastering a `single tool` at a time.
___
Give it some time. Being `persistent` is everything.
___
Consider using `vim` keybindings, they are everywhere.
___
You don't have to do everything in the terminal, it's just a `tool` in your toolbox.

---

## 7. Questions and Answers

```dart
  _____  _                    _                           _ 
 |_   _|| |__    __ _  _ __  | | __  _   _   ___   _   _ | |
   | |  | '_ \  / _` || '_ \ | |/ / | | | | / _ \ | | | || |
   | |  | | | || (_| || | | ||   <  | |_| || (_) || |_| ||_|
   |_|  |_| |_| \__,_||_| |_||_|\_\  \__, | \___/  \__,_|(_)
                                     |___/                  
```
---

#### References
- **[1]** [DevEx in Action - A study of its tangible impacts](https://queue.acm.org/detail.cfm?id=3639443)

---
#### Additional tools
**tree**
A simple file-system visualization tool for the command line. 

[→](https://github.com/Old-Man-Programmer/tree)
___
 
**glow**
A fancy markdown reader in your terminal.

[→](https://github.com/charmbracelet/glow)

___
**cowsay**
Your personal cow greeter in the terminal.

[→](https://github.com/tnalpgge/rank-amateur-cowsay)
___
**slides**
A program that can visualize markdown files as slides.

[→](https://github.com/maaslalani/slides)
