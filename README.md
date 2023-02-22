#!/bin/bash

# Instala dependências
sudo apt update
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev

# Instala Pyenv
curl https://pyenv.run | bash
echo 'export PATH="$HOME/.pyenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc

# Instala Visual Studio Code
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt update
sudo apt install -y code

# Instala Google Chrome
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb

# Instala Spotify
sudo snap install spotify

# Instala Zsh e Oh My Zsh
sudo apt install -y zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Instala Powerlevel10k
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/.oh-my-zsh/custom/themes/powerlevel10k
echo 'ZSH_THEME="powerlevel10k/powerlevel10k"' >> ~/.zshrc

# Configurações do Powerlevel10k
echo 'source ~/.oh-my-zsh/custom/themes/powerlevel10k/powerlevel10k.zsh-theme' >> ~/.zshrc
echo 'POWERLEVEL9K_MODE="nerdfont-complete"' >> ~/.zshrc
echo 'POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(dir vcs)' >> ~/.zshrc
echo 'POWERLEVEL9K_PROMPT_ON_NEWLINE=true' >> ~/.zshrc
echo 'POWERLEVEL9K_PROMPT_ADD_NEWLINE=true' >> ~/.zshrc
echo 'POWERLEVEL9K_VCS_MODIFIED_BACKGROUND="red"' >> ~/.zshrc
echo 'POWERLEVEL9K_VCS_UNTRACKED_BACKGROUND="yellow"' >> ~/.zshrc
echo 'POWERLEVEL9K_SHORTEN_DIR_LENGTH=2' >> ~/.zshrc

# Define o zsh como shell padrão
chsh -s $(which zsh)
