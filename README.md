# Parrot Sec OS 5.3

## Primer Paso

**Actualizacion**

    sudo apt update && sudo parrot-upgrade -y

**Tilix, Evolution y Nautilus**

    sudo apt install tilix evolution nautilus

**Ir a control center preferred applications (manual)**

> terminal -> tilix

> file manager -> files

## Instalar GNOME

**Eliminar libpipewire**

    sudo apt remove libpipewire-0.3-0 -y

**Eliminar libspa**

    sudo apt remove libspa-0.2-modules -y

**Instalar gnome**

    sudo apt update && sudo apt install parrot-desktop-gnome -y

> Seleccionar gdm3

**Reinicio**

    sudo reboot

> Antes de iniciar sesión cambiar entorno grafico a GNOME

### Extensiones de Gnome

**Activar user themes**

> tweaks tool > extension > user themes

> Abrir firefox ingresar a gnome-extensions, instalar extensión

**Reparar Dash to Dock**

> (no abrir ni habilitar dash to dock) descargar desde repo en el directorio de descarga

    git clone https://github.com/micheleg/dash-to-dock.git

**si no esta instalado ruby (opcional)**

    sudo apt-get install ruby-full 

**SASS**

    sudo gem install sass

>

    export SASS=ruby

>

    cd dash-to-dock/

>

    make

>

    make install

> Hacer Logout

> Desinstalar de Gnome extension desde el navegador logout y volver instalarla desde el buscador y de acuerdo a la version de gnome-shell(3.338)

### Configurar Apariencia

**clonar este repositorio**

    git clone https://github.com/gh0sshx/virtual_machine.git

**Crear carpetas .themes y .icons**

    mkdir {".themes",".icons"}

**copiar contenido desde el repositorio descargado**

    cd virtual_machine/themes

>

    cp -r * ~/.themes

>

    cd ../icons

>

    cp -r * ~/.icons/  

    
#### Configurar Workspace

> En tweaks tools extension cambiar a horizontal

**Para mover applicaciones entre workspaces con atajos de teclado**

    gsettings set org.gnome.desktop.wm.keybindings move-to-workspace-right "['<Super><Alt>Right']"

>

    gsettings set org.gnome.desktop.wm.keybindings move-to-workspace-left "['<Super><Alt>Left']"

**Para moverse dentro de los workspaces**

    gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-left "['<Ctrl><Super>Left']"

>

    gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-right "['<Ctrl><Super>Right']"


#### Configurar oh-my-ash para usuario y root

**instalar zsh**

    sudo apt install zsh

**cambiar a zsh**

    chsh -s /bin/zsh

**instalar oh my zsh**

> https://ohmyz.sh/ via curl

    sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
    
> mantener directorio en terminal, copiar y pegar al final en la .zshrc

    #inherit directory
    if [ $TILIX_ID ] || [ $VTE_VERSION ]; then
        source /etc/profile.d/vte.sh
    fi

> comando para evitar error

    sudo ln -s /etc/profile.d/vte-2.91.sh /etc/profile.d/vte.sh

> Configurar ruta para establecer objetivo (opcional)

    # set target
    function set_target(){
     read target
     echo $target > <path>
    }

### Configurar Fonts

> Desde la web https://www.nerdfonts.com/font-downloads descargar Symbols Nerd Fonts

> Descomprimir el .zip 

    unzip NerdFontsSymbolsOnly.zip -d NerdFonts
    
> crear otra carpeta para almacenar los fonts en el sistema

    mkdir ~/.local/share/fonts

> Copiar los archivos descomprimidos a la carpeta creada en .local/share , después limpiar cache

    cp NerdFonts/* ~/.local/share/fonts

>

    fc-cache -f -v

### Desactivar autoasignación de nombres de interfaz de red

> Editar el  archivo grub

    nano /etc/default/grub

> buscar la línea que comienza con ‘GRUB_CMDLINE_LINUX_DEFAULT’

> agregar al final antes de cerrar las comillas

     net.ifnames=0

**Guarda y cierra el archivo, actualiza el archivo grub**

    sudo update-grub

**Enmascara el archivo.link de udev para la política predeterminada**

    sudo ln -s /dev/null /etc/systemd/network/99-default.link1

**Reiniciar Sistema**

    sudo reboot

### Configurar executor con fonts symbol

> ir a extensions

**Target**

    if [[ $(cat /home/ghost/VPN/.target) == "" ]]; then echo "󰓾 ---.---.---.---"; else echo "󰓾 " && cat /home/ghost/VPN/.target; fi && echo "   "

**VPN**

    if [[ $(ip -4 addr show tun0 2>&1) == *"does not exist." ]]; then echo "󱘖 VPN Not Online"; else echo "tun0  " && ip -4 addr show tun0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}'; fi && echo "   "

**LAN**

    if [[ $(ip addr show dev eth0 | grep 'inet ' | awk '{print $2}' | cut -f1 -d'/') == "" ]]; then echo "eth0󰈂"; else echo "eth0 󰈀 " && ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}'; fi && echo "   "

**Wifi (opcional)**

    if [[ $(ip addr show dev wlan0 | grep 'inet ' | awk '{print $2}' | cut -f1 -d'/') == "" ]]; then echo "wlan0󰖪"; else echo "wlan0 󱚻 " && ip -4 addr show wlan0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}';fi && echo "   "

### Agregar color en terminal

**Instalar zsh plugin

> https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md

    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/plugins/zsh-syntax-highlighting

**Editar archivo**
    
    nano ~/.oh-my-zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

**Copiar y pegar**

    ZSH_HIGHLIGHT_HIGHLIGHTERS=(main brackets pattern)
    ZSH_HIGHLIGHT_STYLES[default]=none
    ZSH_HIGHLIGHT_STYLES[unknown-token]=fg=white,underline
    ZSH_HIGHLIGHT_STYLES[reserved-word]=fg=cyan,bold
    ZSH_HIGHLIGHT_STYLES[suffix-alias]=fg=green,underline
    ZSH_HIGHLIGHT_STYLES[global-alias]=fg=green,bold
    ZSH_HIGHLIGHT_STYLES[precommand]=fg=green,underline
    ZSH_HIGHLIGHT_STYLES[commandseparator]=fg=blue,bold
    ZSH_HIGHLIGHT_STYLES[autodirectory]=fg=green,underline
    ZSH_HIGHLIGHT_STYLES[path]=bold
    ZSH_HIGHLIGHT_STYLES[path_pathseparator]=
    ZSH_HIGHLIGHT_STYLES[path_prefix_pathseparator]=
    ZSH_HIGHLIGHT_STYLES[globbing]=fg=blue,bold
    ZSH_HIGHLIGHT_STYLES[history-expansion]=fg=blue,bold
    ZSH_HIGHLIGHT_STYLES[command-substitution]=none
    ZSH_HIGHLIGHT_STYLES[command-substitution-delimiter]=fg=magenta,bold
    ZSH_HIGHLIGHT_STYLES[process-substitution]=none
    ZSH_HIGHLIGHT_STYLES[process-substitution-delimiter]=fg=magenta,bold
    ZSH_HIGHLIGHT_STYLES[single-hyphen-option]=fg=green
    ZSH_HIGHLIGHT_STYLES[double-hyphen-option]=fg=green
    ZSH_HIGHLIGHT_STYLES[back-quoted-argument]=none
    ZSH_HIGHLIGHT_STYLES[back-quoted-argument-delimiter]=fg=blue,bold
    ZSH_HIGHLIGHT_STYLES[single-quoted-argument]=fg=yellow
    ZSH_HIGHLIGHT_STYLES[double-quoted-argument]=fg=yellow
    ZSH_HIGHLIGHT_STYLES[dollar-quoted-argument]=fg=yellow
    ZSH_HIGHLIGHT_STYLES[rc-quote]=fg=magenta
    ZSH_HIGHLIGHT_STYLES[dollar-double-quoted-argument]=fg=magenta,bold
    ZSH_HIGHLIGHT_STYLES[back-double-quoted-argument]=fg=magenta,bold
    ZSH_HIGHLIGHT_STYLES[back-dollar-quoted-argument]=fg=magenta,bold
    ZSH_HIGHLIGHT_STYLES[assign]=none
    ZSH_HIGHLIGHT_STYLES[redirection]=fg=blue,bold
    ZSH_HIGHLIGHT_STYLES[comment]=fg=black,bold
    ZSH_HIGHLIGHT_STYLES[named-fd]=none
    ZSH_HIGHLIGHT_STYLES[numeric-fd]=none
    ZSH_HIGHLIGHT_STYLES[arg0]=fg=cyan
    ZSH_HIGHLIGHT_STYLES[bracket-error]=fg=red,bold
    ZSH_HIGHLIGHT_STYLES[bracket-level-1]=fg=blue,bold
    ZSH_HIGHLIGHT_STYLES[bracket-level-2]=fg=green,bold
    ZSH_HIGHLIGHT_STYLES[bracket-level-3]=fg=magenta,bold
    ZSH_HIGHLIGHT_STYLES[bracket-level-4]=fg=yellow,bold
    ZSH_HIGHLIGHT_STYLES[bracket-level-5]=fg=cyan,bold
    ZSH_HIGHLIGHT_STYLES[cursor-matchingbracket]=standout

**Habilitar plugins**

    plugins=(git sudo zsh-syntax-highlighting)

**Instalar extensiones**

    Clock Left
>

    Improved Workspace Indicator

## Instalar Dropbox

> https://www.dropbox.com/es/install-linux
  
    sudo dpkg -i 

>

    sudo apt install -f

>

    sudo dpkg -i 

>

    Dropbox start -i



