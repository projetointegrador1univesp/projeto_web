Tutorial: Configurando Python 3.9.13 (Recomendado na Univesp)  + Django + MySQL + GitHub no Windows
Instalação do Python 3.9.13, configuração do Django com MySQL, conexão com GitHub e execução local do projeto.
________________________________________
1 - Instalar Python 3.9.13
1.	Baixe a versão 3.9.13 do Python em: 
o	https://www.python.org/downloads/release/python-390/
2.	Durante a instalação, marque a opção "Add Python to PATH".
3.	Após instalar, verifique a versão no terminal: 
4.	python --version
Deve retornar algo como: 
Python 3.9.13
Se outra versão aparecer, siga as instruções abaixo.
Garantir que o Python 3.9 seja Prioritário
No terminal, execute:
where python
Se houver várias versões listadas, ajuste as Variáveis de Ambiente:
1.	Pressione Win + R, digite sysdm.cpl e pressione Enter.
2.	Vá até a aba Avançado → clique em Variáveis de Ambiente.
3.	Na seção Variáveis do Sistema, edite Path.
4.	Remova ou mova para baixo as versões que não sejam 3.9.13
5.	Adicione ou mova para o topo: 
6.	C:\Users\user\AppData\Local\Programs\Python\Python39\
7.	C:\Users\user\AppData\Local\Programs\Python\Python39\Scripts\
8.	Salve e feche. Reabra o terminal e teste novamente python --version.
________________________________________
2️ - Instalar MySQL e MySQL Workbench
1.	Baixe e instale o MySQL Server em: 
o	https://dev.mysql.com/downloads/mysql/
2.	Durante a instalação: 
o	Escolha o modo Developer Default.
o	Defina um usuário: root e senha:root para o MySQL.
3.	Instale também o MySQL Workbench para gerenciar o banco de dados: 
o	https://dev.mysql.com/downloads/workbench/
Para testar a conexão, execute no terminal:
mysql -u root -p
Digite sua senha e, se conectar com sucesso, digite exit; para sair.
________________________________________
3️ - Criar e Configurar o Projeto Django
Clonar o Repositório do GitHub
1.	Instale o Git: https://git-scm.com/downloads
2.	Clone o repositório: 
3.	No terminal digite: git init
4.	Em seguida para clonar o repositório: git clone https://github.com/projetointegrador1univesp/projeto_web.git
5.	Abra o projeto: cd projeto_web
Criar um Ambiente Virtual
1.	No terminal, dentro da pasta do projeto, crie o ambiente virtual: 
2.	python -m venv venv
Ativar o Ambiente Virtual
Se estiver usando Git Bash:
source venv/Scripts/activate
Ou:
. venv/Scripts/activate
Se estiver no cmd:
venv\Scripts\activate
Se estiver no PowerShell:
venv\Scripts\Activate.ps1
Se o ambiente virtual ativou corretamente, você verá (venv) no início do terminal.
Instalar Dependências
pip install -r requirements.txt
Se não houver requirements.txt, instale manualmente:
pip install django mysqlclient
Se houver erro no Windows, instale:
pip install pymysql
E adicione isso no settings.py:
import pymysql
pymysql.install_as_MySQLdb()

Criar o Banco de Dados no MySQL Workbench
1.	Abra o MySQL Workbench.
2.	Conecte-se ao servidor MySQL com usuário root.
3.	Crie um novo schema chamado projeto_web_db com o seguinte comando SQL: 
4.	CREATE DATABASE projeto_web_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
Configurar o Banco de Dados no Django
Edite projeto_web/settings.py e adicione:
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'projeto_web_db',
        'USER': 'root',  # Seu usuário do MySQL
        'PASSWORD': 'root',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}

Criar as Tabelas no Banco, automatizadas
python manage.py migrate
________________________________________
4️ - Rodar o Projeto Localmente
Criar um Superusuário
python manage.py createsuperuser
Preencha usuário, email e senha.
Rodar o Servidor
python manage.py runserver
Acesse http://127.0.0.1:8000/admin e faça login com as credenciais criadas acima.
________________________________________
5️ - Enviar Alterações para o GitHub
git add .
git commit -m "Configuração inicial"
git push origin main
