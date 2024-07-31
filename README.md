# Install a New Mac (ARM)

This is a checklist to help you install all the essentials to start coding with a new computer.

## Warp (Optional)

I recommend using the amazing termnial `Wrap`. You can download it from their website [here](https://www.warp.dev/).

## Install ZSH

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

<details>
    <summary>Upadate .zshrc</summary>

```bash
# If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:$HOME/.local/bin:/usr/local/bin:$PATH

# Path to your Oh My Zsh installation.
export ZSH="$HOME/.oh-my-zsh"

# Set name of the theme to load --- if set to "random", it will
# load a random theme each time Oh My Zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
ZSH_THEME="robbyrussell"

# Set list of themes to pick from when loading at random
# Setting this variable when ZSH_THEME=random will cause zsh to load
# a theme from this variable instead of looking in $ZSH/themes/
# If set to an empty array, this variable will have no effect.
# ZSH_THEME_RANDOM_CANDIDATES=( "robbyrussell" "agnoster" )

# Uncomment the following line to use case-sensitive completion.
# CASE_SENSITIVE="true"

# Uncomment the following line to use hyphen-insensitive completion.
# Case-sensitive completion must be off. _ and - will be interchangeable.
# HYPHEN_INSENSITIVE="true"

# Uncomment one of the following lines to change the auto-update behavior
# zstyle ':omz:update' mode disabled  # disable automatic updates
# zstyle ':omz:update' mode auto      # update automatically without asking
# zstyle ':omz:update' mode reminder  # just remind me to update when it's time

# Uncomment the following line to change how often to auto-update (in days).
# zstyle ':omz:update' frequency 13

# Uncomment the following line if pasting URLs and other text is messed up.
# DISABLE_MAGIC_FUNCTIONS="true"

# Uncomment the following line to disable colors in ls.
# DISABLE_LS_COLORS="true"

# Uncomment the following line to disable auto-setting terminal title.
# DISABLE_AUTO_TITLE="true"

# Uncomment the following line to enable command auto-correction.
ENABLE_CORRECTION="true"

# Uncomment the following line to display red dots whilst waiting for completion.
# You can also set it to another string to have that shown instead of the default red dots.
# e.g. COMPLETION_WAITING_DOTS="%F{yellow}waiting...%f"
# Caution: this setting can cause issues with multiline prompts in zsh < 5.7.1 (see #5765)
# COMPLETION_WAITING_DOTS="true"

# Uncomment the following line if you want to disable marking untracked files
# under VCS as dirty. This makes repository status check for large repositories
# much, much faster.
# DISABLE_UNTRACKED_FILES_DIRTY="true"

# Uncomment the following line if you want to change the command execution time
# stamp shown in the history command output.
# You can set one of the optional three formats:
# "mm/dd/yyyy"|"dd.mm.yyyy"|"yyyy-mm-dd"
# or set a custom format using the strftime function format specifications,
# see 'man strftime' for details.
# HIST_STAMPS="mm/dd/yyyy"

# Would you like to use another custom folder than $ZSH/custom?
# ZSH_CUSTOM=/path/to/new-custom-folder

# Which plugins would you like to load?
# Standard plugins can be found in $ZSH/plugins/
# Custom plugins may be added to $ZSH_CUSTOM/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(git)

source $ZSH/oh-my-zsh.sh

# User configuration

# Export PATH environment variable
export PATH="/opt/homebrew/bin:$PATH:$HOME/bin:/usr/local/bin:$PATH"

# You may need to manually set your language environment
# export LANG=en_US.UTF-8

# Preferred editor for local and remote sessions
if [[ -n $SSH_CONNECTION ]]; then
  export EDITOR='vim'
else
  export EDITOR='nano'
fi

# Compilation flags
# export ARCHFLAGS="-arch $(uname -m)"

# Set personal aliases, overriding those provided by Oh My Zsh libs,
# plugins, and themes. Aliases can be placed here, though Oh My Zsh
# users are encouraged to define aliases within a top-level file in
# the $ZSH_CUSTOM folder, with .zsh extension. Examples:
# - $ZSH_CUSTOM/aliases.zsh
# - $ZSH_CUSTOM/macos.zsh
# For a full list of active aliases, run `alias`.

# Example aliases
alias ll='ls -l'
alias la='ls -la'
alias ..='cd ..'

```

</details>

When uptaing `.zshrc`, always update it by:

```bash
source ~/.zshrc
```

## Install Brew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

<details>
    <summary>Update .zshrc</summary>

Add to the `.zshrc`:

Export PATH environment variable

```bash
export PATH="/opt/homebrew/bin:$PATH:$HOME/bin:/usr/local/bin:$PATH"
```

</details>

## Install git

```bash
brew install git
```

# Download and Install vsCode

[Here](https://code.visualstudio.com/docs/setup/mac)

## `code` as a shortcut

1. Install Visual Studio Code Command Line Tool: Open Visual Studio Code, then open the Command Palette by pressing Cmd + Shift + P and type Shell Command: Install 'code' command in PATH. Select it and hit Enter. This will install the code command to your PATH.

2. Add an alias to the `.zshrc` file: `alias .code="code"`

## Connect to Github by SSH

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### Generate a new SSH key (if you don't have one):

```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

### Add the SSH key to the ssh-agent:

Start the ssh-agent in the background:

```bash
eval "$(ssh-agent -s)"
```

Add your SSH private key to the ssh-agent:

```bash
ssh-add ~/.ssh/id_ed25519
```

### Add the SSH key to your GitHub account:

Copy the SSH key to your clipboard:

```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

Paste the public key in
[https://github.com/settings/keys](https://github.com/settings/keys)

Run the following command to verify the SSH connection to GitHub:

```bash
ssh -T git@github.com
```

When you get

```bash
The authenticity of host 'github.com (xxx.xx.xxx.x)' can't be established. This key is not known by any other names. Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Type yes and press Enter, and you should then see a message like this:

```bash
Warning: Permanently added 'github.com,140.82.121.3' to the list of known hosts.
```

The connection will then proceed, and you should see the authentication success message if everything is set up correctly:

```bash
Hi yourusername! You've successfully authenticated, but GitHub does not provide shell access.
```

### VsCode

Sigin to sync your accounts.

# languages:

For running specific programming languages, you need to install additional software. For me, it is mostly:

- Node
- Python 3
- Go

But you might want to install other programming languages :)

# Other

- Rectangle
- AltTab
- Spotify
- Slack
- Whatsapp
