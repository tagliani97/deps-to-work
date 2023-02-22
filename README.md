#!/bin/bash

sudo apt update

# Instalação do Visual Studio Code
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /usr/share/keyrings/
sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt-get update
sudo apt-get install code

# Instalação do Google Chrome
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
sudo apt-get install -f

# Instalação do Spotify
curl -sS https://download.spotify.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb http://repository.spotify.com stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list
sudo apt-get update && sudo apt-get install spotify-client

sudo apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev

# Instalação do Zsh
sudo apt update
sudo apt install zsh

# Configuração do Zsh como shell padrão
chsh -s $(which zsh)

# Instalação do Oh-My-Zsh com Powerlevel10k theme
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git clone https://github.com/romkatv/powerlevel10k.git ~/.oh-my-zsh/custom/themes/powerlevel10k

# Atualização do arquivo /etc/passwd para tornar o Zsh o shell padrão
sudo sed -i 's/\/bin\/bash/\/usr\/bin\/zsh/g' /etc/passwd

# Altera o shell para Zsh
exec zsh

# Configuração do Powerlevel10k como tema padrão
sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="powerlevel10k\/powerlevel10k"/g' ~/.zshrc

# Instalação do Pyenv
curl https://pyenv.run | bash

# Configuração do Pyenv no Powerlevel10k
echo 'POWERLEVEL9K_LEFT_PROMPT_ELEMENTS+=(virtualenv)' >> ~/.zshrc
echo 'POWERLEVEL9K_PROMPT_ON_NEWLINE=true' >> ~/.zshrc
echo 'POWERLEVEL9K_MULTILINE_FIRST_PROMPT_PREFIX="┌──"' >> ~/.zshrc
echo 'POWERLEVEL9K_MULTILINE_LAST_PROMPT_PREFIX="└──"' >> ~/.zshrc
echo 'POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status root_indicator background_jobs time virtualenv pyenv)' >> ~/.zshrc
echo 'POWERLEVEL9K_PYENV_FOREGROUND="white"' >> ~/.zshrc
echo 'POWERLEVEL9K_PYENV_BACKGROUND="black"' >> ~/.zshrc
echo 'POWERLEVEL9K_PYENV_VISUAL_IDENTIFIER_COLOR="black"' >> ~/.zshrc
echo 'POWERLEVEL9K_PYENV_VISUAL_IDENTIFIER="'"$(echo -e '\uE235')"'"' >> ~/.zshrc
echo 'POWERLEVEL9K_TIME_FORMAT="%D{%H:%M:%S}"' >> ~/.zshrc

echo 'export SHELL=/usr/bin/zsh' >> ~/.bashrc 
echo 'export SHELL=/usr/bin/zsh' >> ~/.zshrc
sudo cp ~/.zshrc /etc/zsh/zshrc
SHELL=/bin/zsh
