# curso-postgresql
![download](https://github.com/user-attachments/assets/7dd747a6-cb9e-426a-ba7a-a78850d94239)

# Guia de Instalação e Configuração do PostgreSQL
Este README descreve o passo a passo para instalar, configurar e testar o PostgreSQL, tanto em ambientes Linux (Ubuntu/Debian/Fedora) quanto em Windows. Inclui também exemplos de criação de usuários e bancos de dados, além de referências úteis.

---

## Pré-requisitos

- Acesso com privilégios de **sudo** em Linux ou conta de administrador no Windows.  
- Conexão com a internet para baixar pacotes e dependências.  
- Espaço em disco suficiente (mínimo 200 MB).  

---

## Instalação no Ubuntu / Debian

1. **Adicionar o repositório oficial do PostgreSQL**  
   ```bash
   sudo apt-get update
   sudo apt-get install -y gnupg2 wget lsb-release
   wget -qO - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
   echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main"      | sudo tee /etc/apt/sources.list.d/pgdg.list
   ```  
  

2. **Instalar o servidor PostgreSQL**  
   ```bash
   sudo apt-get update
   sudo apt-get install -y postgresql-16 postgresql-contrib-16
   ```  
  

3. **Iniciar e habilitar o serviço**  
   ```bash
   sudo systemctl start postgresql
   sudo systemctl enable postgresql
   ```  
  

---

## Instalação no Fedora Linux

1. **Instalar o servidor PostgreSQL**  
   ```bash
   sudo dnf install postgresql-server postgresql-contrib
   ```  
 

2. **Inicializar o banco de dados**  
   ```bash
   sudo postgresql-setup --initdb --unit postgresql
   ```  
 

3. **Habilitar e iniciar o serviço**  
   ```bash
   sudo systemctl enable postgresql
   sudo systemctl start postgresql
   ```  
 

---

## Instalação no Windows

1. **Baixar o instalador**  
   Acesse https://www.postgresql.org/download/windows/ e clique em **Download the installer**.

2. **Executar o instalador**  
   - Selecione componentes (Server, pgAdmin 4, Command Line Tools).  
   - Escolha diretórios padrão e defina uma senha para o usuário `postgres`.  
   - Defina a porta (padrão: 5432) e locale.  
   - Conclua a instalação.  
  

---

## Configuração Inicial

1. **Definir senha do usuário `postgres`**  
   ```bash
   sudo -u postgres psql -c "ALTER USER postgres WITH PASSWORD 'SenhaForte123';"
   ```  
  

2. **Permitir conexões remotas**  
   Edite `/etc/postgresql/16/main/postgresql.conf` (Ubuntu/Debian) ou `/var/lib/pgsql/data/postgresql.conf` (Fedora) e ajuste:  
   ```conf
   listen_addresses = '*'
   ```  
  

3. **Configurar autenticação por senha**  
   No arquivo `pg_hba.conf`, substitua métodos `peer` e `ident` por `md5` para conexões desejadas, por exemplo:  
   ```conf
   local   all             postgres                                md5
   host    all             all             0.0.0.0/0               md5
   ```  
  

4. **Reiniciar o serviço**  
   ```bash
   sudo systemctl restart postgresql
   ```  
  

---

## Criação de Usuários e Bancos de Dados

| Comando        | Descrição                            |
| -------------- | ------------------------------------ |
| `createuser`   | Cria um novo role no PostgreSQL      |
| `createdb`     | Cria um novo banco de dados          |
| `psql`         | Cliente interativo de linha de comando |

Exemplo de criação:
```bash
sudo -u postgres createuser --superuser USUÁRIO
sudo -u postgres psql -c "ALTER USER USUÁRIO WITH PASSWORD 'SenhaUSUARIO';"
sudo -u postgres createdb -O USUÁRIO meu_banco
```  


---

## Verificação

Conecte-se ao banco de dados:
```bash
psql -U USUÁRIO -d meu_banco -h localhost -W
```

Onde:
- ``psql`` - comando de terminal do PostgreSQL;
- ``-U`` - Usuário que fará chamada à Base de Dados;
- ``-d`` - Nome da Base de dados (database)

   
E liste tabelas com:
```sql
\dt
```  

---
---
## Referências

- Documentação oficial PostgreSQL: https://www.postgresql.org/docs/  
- Tutorial de instalação (fonte): https://www.postgresql.org/docs/current/tutorial-install.html 
- Gist de configuração avançada: https://gist.github.com/15Dkatz/321e83c4bdd7b78c36884ce92db26d38 
- Política de marcas: https://www.postgresql.org/about/policies/trademarks/ 

---
---



# Links de Apoio
- [PSQL on line](https://pg-sql.com/)
