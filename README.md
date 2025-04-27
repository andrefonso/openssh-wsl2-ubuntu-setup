# OpenSSH no Ubuntu WSL2: Instalação, Configuração e Ativação Permanente

Este tutorial ensina como instalar, configurar e garantir que o serviço OpenSSH esteja **sempre ativo** no Ubuntu rodando dentro do **WSL2** (Windows Subsystem for Linux 2).

## Sugestão de Nome para o Repositório

**openssh-wsl2-ubuntu-setup**

## Índice

- [Pré-requisitos](#pré-requisitos)
- [Instalação do OpenSSH Server](#instalação-do-openssh-server)
- [Configuração do SSH](#configuração-do-ssh)
- [Ativação do SSH automaticamente no WSL2](#ativação-do-ssh-automaticamente-no-wsl2)
- [Verificando o status do SSH](#verificando-o-status-do-ssh)


## Pré-requisitos

- Windows 10 ou 11 com **WSL2** já instalado.
- Ubuntu (20.04, 22.04, 24.04 ou superior) instalado no WSL2.
- Permissão de administrador no Windows para alterar configurações, se necessário.

## Instalação do OpenSSH Server

1. Abra o Ubuntu no WSL2.

2. Atualize a lista de pacotes e os pacotes instalados:

   ```bash
   sudo apt update
   sudo apt upgrade -y
   ```

3. Instale o OpenSSH Server:

   ```bash
   sudo apt install openssh-server -y
   ```

## Configuração do SSH

1. Edite o arquivo de configuração do SSH (opcional):

   ```bash
   sudo nano /etc/ssh/sshd_config
   ```

2. Verifique e ajuste as seguintes opções ou as incluas no arquivo:

   ```
   Include /etc/ssh/sshd_config.d/*.conf
   Port 22
   PasswordAuthentication yes
   KbdInteractiveAuthentication no
   ```

3. Salve (`CTRL + O`) e saia (`CTRL + X`).

4. Se quiser usar systemd no WSL2 (funciona no Ubuntu 22.04 pra cima, com Windows 11 atualizado), você precisa alterar o arquivo /etc/wsl.conf dentro do WSL:

   - Abra o WSL2 (Ubuntu).

   - Edite ou crie o arquivo /etc/wsl.conf:
  
   ```sh
   sudo nano /etc/wsl.conf
   ```

   - Coloque o seguinte conteúdo:
  
   ```sh
   [boot]
   systemd=true
   ```

   - Salve e feche.

   - Depois, no Windows, reinicie o WSL.

## Ativação do SSH automaticamente no WSL2

1. Crie as chaves de host do SSH digitando o seguinte comando:

   ```sh
   sudo ssh-keygen -A
   ```

2. Depois disso, inicie o SSH:

   ```sh
   sudo service ssh start
   ```


## Verificando o status do SSH

Para verificar se o SSH está rodando:

```sh
sudo service ssh status
```

Se estiver ativo, você verá:

```
Active: active (running)
```

Para iniciar o serviço manualmente (se necessário):

```sh
sudo service ssh start
```

