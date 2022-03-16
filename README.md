# PVE VDI Client

O foco deste projeto é criar um cliente VDI simples destinado à implantação em massa. Este cliente VDI se conecta diretamente ao Proxmox VE e permite que os usuários se conectem (via Spice) a quaisquer VMs que tenham permissão para acessar.

![Login Screen](screenshots/login.png)

![Login Screen with OTP](screenshots/login-totp.png)

![VDI View](screenshots/vdiview.png)

## Instalação do Windows

Você deve instalar o virt-viewer antes de usar o cliente PVE VDI, você pode baixá-lo no site [official Virtual Machine Manager](https://virt-manager.org/download/) site.

Visite a seção [releases](https://github.com/joshpatten/PVE-VDIClient/releases) para baixar um pacote MSI pré-reconstruído

Se você precisar personalizar a instalação, como assinar o executável e o MSI, você pode baixar e instalar o [WIX toolset](https://wixtoolset.org/releases/) e usar o arquivo build_vdiclient.bat para construir um novo MSI.

você precisará baixar a versão python 3.10 mais recente e executar os seguintes comandos para instalar os pacotes necessários:

    requirements.bat

## Instalação linux

Execute os seguintes comandos em um sistema Linux Debian/Ubuntu para instalar os pré-requisitos apropriados

    apt install python3-pip virt-viewer
    chmod +x requirements.sh
    ./requirements.sh
    cp vdiclient.py /usr/local/bin
    chmod +x /usr/local/bin/vdiclient.py

## Arquivo de configuração

O cliente PVE VDI REQUER um arquivo de configuração para funcionar. O cliente procura por este arquivo nos seguintes locais, a menos que --config seja especificado na linha de comando:

* Windows
    * %APPDATA%\VDIClient\vdiclient.ini
    * %PROGRAMFILES%\VDIClient\vdiclient.ini
* Linux
    * ~/.config/VDIClient/vdiclient.ini
    * /etc/vdiclient/vdiclient.ini
    * /usr/local/etc/vdiclient/vdiclient.ini

Consulte **vdiclient.ini.example** para todas as opções de arquivos config disponíveis

Se você encontrar quaisquer problemas, sinta-se livre para enviar um relatório de emissão.

## Requisitos de permissão proxmox

Os usuários que estão acessando as instâncias VDI precisam ter as seguintes permissões atribuídas para cada VM que acessam:

* VM.PowerMgmt
* VM.Console
* VM.Audit
