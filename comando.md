# Passo 1: Atualizar o sistema e instalar dependências
No terminal do seu servidor Ubuntu, execute os seguintes comandos para garantir que o sistema está atualizado e possui o Python, o gerenciador de pacotes e o Git instalados:

# PARA ATUALIZAR A MAQUINA
sudo apt update && sudo apt upgrade -y

# PARA INSTALAR O PROGRAMA
sudo apt install python3-pip python3-venv git -y


# Passo 2: Clonar o repositório do GitHub
Baixe o seu projeto do GitHub para dentro da instância. Substitua a URL pelo link do seu repositório:

# PARA CLONAR = git clone
git clone https://github.com/Esmael-Arcanjo/backend.git

git pull para atualizar


Passo 3: Criar e ativar o ambiente virtual (venv)
É uma boa prática isolar as dependências do projeto em um ambiente virtual:
python3 -m venv venv
source venv/bin/activate


Passo 4: Instalar as dependências do projeto
Instale as bibliotecas necessárias (como fastapi e uvicorn). O comando padrão costuma ser:

pip install --upgrade pip
pip install -r requirements.txt

# para abrir um arqui.nano requirements.txt

Pressione Ctrl + C para parar o servidor atual no terminal.

Crie e configure o serviço:
sudo nano /etc/systemd/system/fastapi.service

Ative e inicie o serviço:
sudo systemctl daemon-reload
sudo systemctl start fastapi
sudo systemctl enable fastapi

Você pode verificar a qualquer momento se ele continua ativo rodando o comando:
sudo systemctl status fastapi

Passo 2: Ativar o HTTPS (SSL) com o Certbot
Se o site abrir mas aparecer como "Não seguro", vamos gerar um certificado gratuito para ele funcionar com https://.
No terminal da sua AWS, execute os comandos:
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d api.leamse.com


