# 🚀 Guia de Deploy e Configuração - FastAPI no Ubuntu

Este guia passo a passo ensina como preparar um servidor Ubuntu, clonar o repositório, configurar o ambiente virtual, instalar as dependências, configurar o serviço systemd e habilitar o HTTPS com Certbot.

---

## 📌 Passo 1: Atualizar o sistema e instalar dependências
Garanta que o seu servidor está com os pacotes mais recentes e com as ferramentas essenciais (Python, pip, venv e Git) instaladas.

```bash
# Atualiza a lista de pacotes disponíveis e faz o upgrade de todos os programas desatualizados do sistema
sudo apt update && sudo apt upgrade -y

# Instala o gerenciador de pacotes do Python, o criador de ambientes virtuais e o Git
sudo apt install python3-pip python3-venv git -y
```

---

## 📌 Passo 2: Clonar o repositório do GitHub
Baixe o código-fonte do seu projeto para dentro da instância do servidor.

```bash
# Clona o repositório remoto do GitHub para uma pasta local no servidor
git clone https://github.com/Esmael-Arcanjo/backend.git

# Atualiza o repositório local com as alterações mais recentes vindas do GitHub (execute dentro da pasta do projeto)
git pull
```

---

## 📌 Passo 3: Criar e ativar o ambiente virtual (venv)
Isolar as dependências do projeto evita conflitos com outras aplicações Python do servidor.

```bash
# Cria um ambiente virtual chamado "venv" na pasta atual
python3 -m venv venv

# Ativa o ambiente virtual para que os pacotes instalados fiquem isolados nele
source venv/bin/activate
```

---

## 📌 Passo 4: Instalar as dependências do projeto
Instale as bibliotecas necessárias listadas no arquivo do projeto.

```bash
# Atualiza o pip para a versão mais recente dentro do ambiente virtual
pip install --upgrade pip

# Instala todas as dependências listadas no arquivo requirements.txt (como FastAPI e Uvicorn)
pip install -r requirements.txt

# Abre o editor de texto Nano para criar ou editar o arquivo de dependências requirements.txt
nano requirements.txt
```

---

## 📌 Passo 5: Configurar e iniciar o serviço Systemd (Produção)
Para rodar a aplicação em segundo plano de forma contínua e garantir que reinicie junto com o servidor.

```bash
# Nota: Pressione Ctrl + C para parar o servidor se ele estiver rodando manualmente no terminal

# Cria e abre o arquivo de configuração do serviço systemd para o FastAPI
sudo nano /etc/systemd/system/fastapi.service

# Recarrega o gerenciador do systemd para reconhecer o novo serviço criado
sudo systemctl daemon-reload

# Inicia o serviço do FastAPI imediatamente
sudo systemctl start fastapi

# Configura o serviço para iniciar automaticamente sempre que a máquina for ligada
sudo systemctl enable fastapi

# Verifica o status atual do serviço (se está rodando, erros ou logs recentes)
sudo systemctl status fastapi
```

---

## 📌 Passo 6: Ativar o HTTPS (SSL) com o Certbot
Gera um certificado SSL gratuito para a sua aplicação rodar com segurança via HTTPS.

```bash
# Instala o Certbot e o plugin de integração com o Nginx
sudo apt install certbot python3-certbot-nginx -y

# Solicita e configura automaticamente o certificado SSL para o domínio especificado
sudo certbot --nginx -d api.leamse.com
```

---

## 📌 Comandos Úteis para Desenvolvimento

```bash
# Inicia o servidor Uvicorn escutando em todas as interfaces de rede na porta definida pela variável de ambiente $PORT
uvicorn app.main:app --host 0.0.0.0 --port $PORT

# Inicia o servidor Uvicorn manualmente na porta padrão 8000
uvicorn app.main:app --host 0.0.0.0 --port 8000

# Inicia o Uvicorn com o modo de recarga automática ativado (ótimo para testes e desenvolvimento local)
uvicorn app.main:app --reload
```

---

## 📌 Comandos do Git para Atualizar o Repositório

```bash
# Adiciona todos os arquivos modificados para a área de stage (preparação)
git add .
# Cria um commit salvando as alterações com uma mensagem descritiva
git commit -m "Atualizado"
# Envia as alterações locais para o repositório remoto na branch principal (main)
git push origin main
```