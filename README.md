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
- [Notas importantes](#notas-importantes)
- [Licença](#licença)

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

2. Verifique e ajuste as seguintes opções:

   ```
   Port 22
   PermitRootLogin no
   PasswordAuthentication yes
   ```

3. Salve (`CTRL + O`) e saia (`CTRL + X`).

## Ativação do SSH automaticamente no WSL2

No WSL2, os serviços não iniciam automaticamente como em uma instalação tradicional do Linux.  
Para iniciar o SSH sempre que o Ubuntu abrir:

1. Edite o arquivo `.bashrc` do seu usuário:

   ```bash
   nano ~/.bashrc
   ```

2. Adicione o seguinte bloco ao final do arquivo:

   ```bash
   # Iniciar o OpenSSH Server automaticamente no WSL2
   sudo service ssh status > /dev/null || sudo service ssh start
   ```

3. Salve e feche (`CTRL + O`, `ENTER`, `CTRL + X`).

4. Aplique imediatamente:

   ```bash
   source ~/.bashrc
   ```

## Verificando o status do SSH

Para verificar se o SSH está rodando:

```bash
sudo service ssh status
```

Se estiver ativo, você verá:

```
Active: active (running)
```

Para iniciar o serviço manualmente (se necessário):

```bash
sudo service ssh start
```

## Notas importantes

- **Mudança de IP:** O WSL2 atribui um novo IP a cada reinicialização do Windows. Para descobrir o IP atual:

  ```bash
  hostname -I
  ```

- **Permissão sem senha (opcional):** Para evitar a necessidade de senha para iniciar o serviço SSH, você pode configurar o `sudo` para não exigir senha para o comando `service ssh start`. (Atenção: isso pode ter implicações de segurança.)

- **Após atualizações:** Depois de atualizações do sistema (`apt upgrade`), confirme se o OpenSSH Server continua instalado e funcionando.

## Licença

Distribuído livremente para fins educativos.
