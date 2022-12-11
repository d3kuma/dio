# Docker experience

Repositório onde estudei conceitos de Docker. 

Segue instalação para rodar o Docker no ubuntu pelo Windows via WSL.

## Instalando o docker via WSL

### 1. Habilite o WSL 2

Execute no power shell em modo de administrador os comandos:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
#Reinicie o PC
```

Instale esse aplicativo: https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi

Execute este comando no Power Shell:

```powershell
wsl --set-default-version 2
```

### 2. Instalação e configuração

Instale o Ubuntu pela Microsoft Store e rode estes caminhos conforme documentação do docker:https://docs.docker.com/engine/install/ubuntu/

```bash
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

```bash
sudo mkdir -p /etc/apt/keyrings
```

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

```bash
sudo apt-get update
```

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

Para testar o docker hello-world:

## 3. Instalar o Docker for Windows

````bash
sudo docker run hello-world
````

## Executando um container

```dockerfile
#listar containers
docker ps

#listar imagens
docker images

docker -dti ubuntu
#-d rodar em background
#-t 
#-i

#executar
docker exec -it numero_id /bin/bash
#ver os ids em docker ps

#dar nome para a imagem
#docker run -dti --name apelido_imagem imagem_origem
#ex.:
docker run -dti --name ubuntu-principal ubuntu

#rodar imagem (ex.: centos)
docker run -dti centos
#se não estiver no container, vai baixá-la automaticamente

#parar
docker stop numero_id

#excluir container
docker rm numero_id

#excluir imagem
docker rmi nome_imagem

#comandos pelo container

#ex.: criando diretório
docker exec ubuntu_principal mkdir ~/nova_pasta

#copiar entre containers
docker cp arquivo.txt principal:/nova_pasta

```

## Docker MySQL

```bash
docker pull mysql
#-d para executar em background
#-p porta padrao
docker run -e MYSQL_ROOT_PASSWORD=senha --name mysql-A -d -p 3306:3306 mysql
#executando o banco
docker exec -it nome_container bash
#comando para se conectar no banco
mysql -u root -p --protocolo=tcp

```