# INSTALAR HERRAMIENTAS

### SECLIST

    wget -c https://github.com/danielmiessler/SecLists/archive/master.zip -O SecList.zip \
    && unzip SecList.zip \
    && rm -f SecList.zip

>

    mv SecLists-master SecLists

>
    
    sudo mv SecLists /usr/share/

### CRACKMAPEXEC

> ...

### PROXYCHAINS

**Eliminar proxychains**

    sudo apt remove proxychains 

>

    sudo apt autoremove

> https://github.com/haad/proxychains

**Clonar repositorio**    

    git clone https://github.com/haad/proxychains.git

> necesita un compilador de C que funcione, preferiblemente gcc

    ./configure

>

    make

>

    sudo make install

**Crear alias en la bashrc o zshrc**

    alias proxychains="proxychains4"















