# Modern Dotfiles

Modern, minimal dotfiles managed with [chezmoi](https://www.chezmoi.io/).

## What's Included

- **Shell**: zsh with oh-my-zsh, starship prompt, autosuggestions, syntax highlighting, fzf
- **Editor**: vim with vim-plug, minimal essential plugins
- **Git**: Clean configuration with useful aliases
- **Tools**: mise (version manager), direnv

## Prerequisites

Install these tools first:

```bash
# macOS (Homebrew)
brew install chezmoi starship fzf ripgrep fd mise direnv

# Install oh-my-zsh if not already installed
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## Installation

### Fresh Setup

1. Install dotfiles with chezmoi:

```bash
chezmoi init --apply https://github.com/ardell/modern_dotfiles.git
```

You'll be prompted for:
- Git user name
- Git email address
- GPG signing key (optional, leave empty to skip)

2. Install oh-my-zsh plugins:

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

3. Install vim-plug:

```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

4. Install vim plugins:

```bash
vim +PlugInstall +qall
```

5. Install fzf key bindings:

```bash
$(brew --prefix)/opt/fzf/install
```

6. Restart your shell or source the config:

```bash
exec zsh
```

### Updating

To pull the latest dotfiles:

```bash
chezmoi update
```

To edit a dotfile:

```bash
chezmoi edit ~/.zshrc    # Opens the source file
chezmoi apply            # Applies changes
```

## Features

### Shell (zsh)

- **Starship prompt**: Modern, fast prompt with git status and language versions
- **fzf**: Fuzzy finder (Ctrl+R for history, Ctrl+T for files)
- **zsh-autosuggestions**: Fish-like suggestions as you type
- **zsh-syntax-highlighting**: Real-time command syntax highlighting
- **Vi mode**: Vim keybindings in the shell

### Vim

**Key Mappings:**
- `8` / `9` - Previous/next tab
- `Shift+W`, `Shift+E`, `Shift+B` - CamelCase word motions
- `Ctrl+P` - Fuzzy file search
- `,b` - Buffer list
- `,r` - Ripgrep search
- `,<space>` - Clear search highlight
- `,w` - Quick save

**Plugins:**
- vim-surround - Easily change surrounding quotes/brackets
- vim-commentary - Comment/uncomment with `gc`
- fzf.vim - Fuzzy finding
- CamelCaseMotion - Navigate CamelCase and snake_case
- vim-polyglot - Syntax for 600+ languages
- ALE - Async linting (Elixir, JS, Python, etc.)

### Git

**Aliases:**
- `git st` - status
- `git ci` - commit
- `git co` - checkout
- `git br` - branch
- `git lg` - pretty log graph
- `git recent` - recent commits from reflog

**Features:**
- Auto-prune on fetch
- Histogram diff algorithm
- zdiff3 merge conflict style
- Auto-setup remote on push

### Mise (Version Manager)

Replaces pyenv, nvm, rbenv, etc. with a single tool.

Usage:
```bash
# In project directory
mise use node@20 python@3.12

# Install what's in .tool-versions or .mise.toml
mise install

# See what's active
mise current
```

## Customization

### Machine-Specific Settings

Chezmoi templates handle machine-specific config. To change your git info:

```bash
chezmoi data    # View current values
chezmoi init    # Re-run setup prompts
```

### Adding Aliases

Edit the zsh config:
```bash
chezmoi edit ~/.zshrc
```

Add your aliases in the "Aliases" section, then:
```bash
chezmoi apply
exec zsh
```

### Vim Customization

To add vim plugins:
```bash
chezmoi edit ~/.vimrc
```

Add a `Plug 'author/plugin'` line, then run `:PlugInstall` in vim.

## Structure

```
modern_dotfiles/
├── .chezmoi.toml.tmpl          # Setup prompts
├── .chezmoiignore              # Files not to install
├── dot_zshrc.tmpl              # ZSH config
├── dot_vimrc                   # Vim config
├── dot_gitconfig.tmpl          # Git config
├── dot_gitignore_global        # Global gitignore
└── dot_config/
    ├── direnv/
    │   └── direnv.toml         # Direnv settings
    ├── mise/
    │   └── config.toml         # Mise settings
    └── starship.toml           # Starship prompt
```

## Troubleshooting

**Oh-my-zsh plugins not loading:**
- Make sure you installed zsh-autosuggestions and zsh-syntax-highlighting
- Check they're in `~/.oh-my-zsh/custom/plugins/`

**Vim plugins missing:**
- Run `:PlugInstall` inside vim
- Check vim-plug is installed: `ls ~/.vim/autoload/plug.vim`

**fzf Ctrl+R not working:**
- Run `$(brew --prefix)/opt/fzf/install` to install key bindings

**Starship not showing:**
- Make sure starship is installed: `which starship`
- Check it's initialized in `~/.zshrc` (should be last line)

## License

MIT
