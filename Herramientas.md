# INSTALAR HERRAMIENTAS

### BATCAT

    sudo apt install bat

**Configurar alias**

    alias bcat="bat"
    

### SECLIST

    wget -c https://github.com/danielmiessler/SecLists/archive/master.zip -O SecList.zip \
    && unzip SecList.zip \
    && rm -f SecList.zip

>

    mv SecLists-master SecLists

>
    
    sudo mv SecLists /usr/share/

### CRACKMAPEXEC

> https://github.com/byt3bl33d3r/CrackMapExec/wiki/Installation

    sudo python3 -m pip install pipx

>

    pipx ensurepath

>

    pipx install crackmapexec

### PROXYCHAINS

**Eliminar proxychains**

    sudo apt remove proxychains 

**Instalar proxychains4**

    sudo apt install proxychains4 proxychains

### SEARCHSPLOIT

    sudo apt -y install exploitdb












