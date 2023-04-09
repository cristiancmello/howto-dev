# WSL2

## ArchLinux

1. Acesse ambiente Arch

   ```sh
   echo "%wheel ALL=(ALL) ALL" > /etc/sudoers.d/wheel
   useradd -m -G wheel -s /bin/bash {username}
   passwd {username}

   # Atualizando chaves e pacotes
   sudo pacman-key --init
   sudo pacman-key --populate
   sudo pacman -Sy archlinux-keyring
   sudo pacman -Syu
   sudo pacman -S --needed git base-devel
   sudo pacman -S rust

   # Instalando Yay
   git clone https://aur.archlinux.org/yay.git
   cd yay
   makepkg -si

   # Removendo repo clonado
   rm -rf yay

   # Instalando ZSH
   yay -S zsh

   # Instalando Powerlevel10k
   yay -S --noconfirm zsh-theme-powerlevel10k-git

   # Definindo tema do Powerlevel10k
   echo 'source /usr/share/zsh-theme-powerlevel10k/powerlevel10k.zsh-theme' >> ~/.zshrc

   # Mudando Shell para ZSH
   chsh -s /usr/bin/zsh

   # Saia do terminal
   exit
   ```

2. Acesse ambiente Windows

   ```bat
   arch config --default-user {username}
   ```

3. Continuação da configuração do Powerlevel10k e ZSH

   ```sh
   mkdir .zsh

   # Instalando plugins para ZSH
   git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions

   cargo install bat exa

   # exa: alternativa ao `ls`
   # bat: alternativa ao `cat`

   # Abra o arquivo `.zshrc` no vscode
   code .zshrc

   # Adicione as linhas abaixo e salve o arquivo
   source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh
   alias ls="exa --icons"
   alias bat="bat --style-auto"
   ```

4. Edite o arquivo `.zshrc` para inserir detecção de apps instalados com `cargo` e aliases

   ```sh
   # Enable Powerlevel10k instant prompt. Should stay close to the top of ~/.zshrc.
   # Initialization code that may require console input (password prompts, [y/n]
   # confirmations, etc.) must go above this block; everything else may go below.
   if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
   source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
   fi

   source /usr/share/zsh-theme-powerlevel10k/powerlevel10k.zsh-theme

   export PATH=$HOME/.cargo/bin:${PATH}

   # To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
   [[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh

   alias ls="exa --icons -lh"
   alias lt="exa --icons -lh --tree --level=2"
   alias ll="exa --icons -lha"
   ```
