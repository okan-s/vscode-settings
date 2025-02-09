## Xcode setup
Open terminal.app
```
xcode-select --install
sudo xcodebuild -license accept
```

## Homebrew setup
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

brew tap homebrew/cask
brew tap homebrew/cask-versions
brew tap homebrew/cask-drivers
brew tap homebrew/cask-fonts
```

## Terminal / shell setup
```
# Nerd fonts
brew install --cask font-fira-code-nerd-font font-ubuntu-mono-nerd-font

# ZSH shell & zim framework setup
curl -fsSL https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh
zimfw install

# Shell prompt & theme customization
brew install starship
echo 'eval "$(starship init zsh)"' >> ~/.zshrc
mkdir -p ~/.config && touch ~/.config/starship.toml
starship preset no-runtime-versions >> ~/.config/starship.toml
echo 'command_timeout = 1200\n' | cat - ~/.config/starship.toml > temp && mv temp ~/.config/starship.toml
echo '\n[aws]\ndisabled=true\n\n[gcloud]\ndisabled=true\n' >> ~/.config/starship.toml
echo '[username]\nstyle_user = "green bold"\nstyle_root = "red bold"\nformat = "[$user]($style)"\ndisabled = false\nshow_always = true\n\n[hostname]\nssh_only = false\nformat =  "[@$hostname](green bold) "\ndisabled = false' >> ~/.config/starship.toml
echo '\n[git_status]\nahead = "⇡${count}"\ndiverged = "⇕⇡${ahead_count}⇣${behind_count}"\nbehind = "⇣${count}"' >> ~/.config/starship.toml

# Modern replacement for "cat" (display contents of file)
brew install bat
echo 'alias cat="bat"' >> ~/.zshrc

# Modern replacement for "ls" (list directories)
brew install exa
echo 'alias l="exa"' >> ~/.zshrc
echo 'alias la="exa -a"' >> ~/.zshrc
echo 'alias ll="exa -lah"' >> ~/.zshrc
echo 'alias ls="exa --color=auto"' >> ~/.zshrc

# Modern replacement for "nano" (editor)
brew install micro
echo 'alias nano="micro"' >> ~/.zshrc
git config --global core.editor "micro"
```

## zsh scripts
```
p() {
  if [[ -f bun.lockb ]]; then
    command bun "$@"
  if [[ -f pnpm-lock.yaml ]]; then
    command pnpm "$@"
  elif [[ -f yarn.lock ]]; then
    command yarn "$@"
  elif [[ -f package-lock.json ]]; then
    command npm "$@"
  else
    command pnpm "$@"
  fi
}
```


## Install Alacritty
```
brew install --cask --no-quarantine alacritty

touch ~/.alacritty.yml

micro ~/.alacritty.yml

# Paste & save this:
window:
    dimensions:
        columns: 128
        lines: 36

font:
    size: 14
    normal:
        family: UbuntuMono Nerd Font Mono

selection:
    save_to_clipboard: true

mouse:
    hints:
        launcher:
            program: open
        modifiers: Command

alt_send_esc: false

key_bindings:
    - { key: Left,     mods: Alt,     chars: "\x1bb"                       }
    - { key: Right,    mods: Alt,     chars: "\x1bf"                       }
    - { key: Left,     mods: Command, chars: "\x1bOH",   mode: AppCursor   }
    - { key: Right,    mods: Command, chars: "\x1bOF",   mode: AppCursor   }
    - { key: Back,     mods: Command, chars: "\x15"                        }
    - { key: Back,     mods: Alt,     chars: "\x1b\x7f"                    }
  
colors:
    primary:
        background: '#0d1117'
        foreground: '#ffffff'
    cursor:
        text: '#F81CE5'
        cursor: '#ffffff'
    normal:
        black:   '#000000'
        red:     '#fe0100'
        green:   '#33ff00'
        yellow:  '#feff00'
        blue:    '#0066ff'
        magenta: '#cc00ff'
        cyan:    '#00ffff'
        white:   '#d0d0d0'
    bright:
        black:   '#808080'
        red:     '#fe0100'
        green:   '#33ff00'
        yellow:  '#feff00'
        blue:    '#0066ff'
        magenta: '#cc00ff'
        cyan:    '#00ffff'
        white:   '#FFFFFF'
```

Start new terminal (Alacritty)


## Misc macOS fixes/optimization
Allow apps from anywhere:
```
sudo spctl --master-disable
```

No delay dock:
```
defaults write com.apple.dock autohide-time-modifier -int 0
```

Mouse options:
```
brew install --cask linearmouse
```

## NodeJS LTS & pnpm
```
brew install node@20
brew link node@20 --force
npm install -g pnpm
```

## Global NodeJS packages
```
npm install -g prettier eslint eslint-plugin-prettier

npm install -g typescript

npm install -g ts-node nodemon

npm install -g serve localtunnel vercel
```

## Java
```
brew tap homebrew/cask-versions
brew install --cask temurin17
export JAVA_HOME=$(/usr/libexec/java_home -v '17*')
brew install maven
```

## Python
```
brew install cmake
brew install pkg-config
brew install --cask miniconda
conda create -n py311 python=3.11
conda activate py311
python --version
conda install jupyter
conda install pytorch torchvision -c pytorch
```

## Expo / React Native
```
brew install watchman
brew install cocoapods
brew install ios-deploy

brew cask install android-sdk
brew cask install android-platform-tools

export ANDROID_HOME=~/Library/Android/sdk/
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools

yes | sdkmanager --licenses && sdkmanager --update

adb devices
```

## PHP stuff
```
brew install composer
brew install php
```

## Apps
```
# To mount NTFS drives
brew tap gromgit/homebrew-fuse
brew install --cask macfuse
brew install ntfs-3g-mac
brew install --cask Mounty

# Move and resize windows with keyboard shortcuts
brew install --cask Rectangle

# Privacy friendly web browser based on Chrome
brew install --cask Brave-browser

# File archiver
brew install --cask Keka

# Open source Firefox (web browser) fork
brew install --cask Waterfox-current

# Operating System Utilities
brew install --cask OnyX

# Disk usage utility (visualizer)
brew install --cask Disk-Inventory-X

# Screenshot
brew install --cask Shottr

# Screen recorder
brew install --cask Kap

# IDE
brew install --cask Visual-Studio-Code

# Torrent downloader
brew install --cask qBittorrent

# Format SD cards & USB drives
brew install --cask sdFormatter

# Flash OS images to SD cards & USB drives
brew install --cask balenaEtcher

# Workspace text chat
brew install --cask Slack

# Workspace video chat
brew install --cask Zoom

# Community chat
brew install --cask Discord

# Private chat
brew install --cask Telegram

# Note taking
brew install --cask Notion

# Remote desktop
brew install --cask AnyDesk

# Optimize images
brew install --cask ImageOptim

# Design app
brew install --cask Figma

# Simple video editing app
brew install --cask Shotcut

# Video compression
brew install --cask HandBrake

# Handle .RAR archive files
brew install --cask The-Unarchiver

# FTP / SFTP client
brew install --cask Cyberduck

# Web Debugging Proxy
brew install --cask Charles

# Containerized application development
brew install --cask Docker

# Android simulator
brew install --cask Genymotion
```
