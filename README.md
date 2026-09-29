# Painel CRM - Instância Whitelabel Padrão

Este repositório contém a versão **Whitelabel Matriz** do Painel CRM, pronta para ser duplicada e implantada na VPS para novos clientes.

## 🚀 Como Implantação para um Novo Cliente na VPS

### 1. Copiar a Pasta do Projeto
Na VPS, copie ou clone este repositório para a pasta do novo cliente:
```bash
cp -r /caminho/painel-crm-whitelabel /var/www/crm-cliente-xyz
cd /var/www/crm-cliente-xyz
```

### 2. Criar o Banco de Dados PostgreSQL
No PostgreSQL da VPS, crie o banco de dados dedicado:
```sql
CREATE DATABASE crm_cliente_xyz;
```

### 3. Configurar o Arquivo `.env`
Copie o exemplo de configuração e preencha com os dados da empresa:
```bash
cp .env.example .env
nano .env
```

Preencha os campos principais:
```env
PORT=3001
JWT_SECRET=chave_secreta_unica_para_este_cliente
COMPANY_NAME="Nome do Cliente"
COMPANY_LOGO_URL="https://link-da-logo.com/logo.png"
DATABASE_URL="postgres://postgres:senha@localhost:5432/crm_cliente_xyz"
GOOGLE_DRIVE_PARENT_FOLDER_ID="id_da_pasta_no_drive"
```

### 4. Instalar Dependências e Iniciar
```bash
npm install --production
pm2 start server.js --name "crm-cliente-xyz"
```

---
*Desenvolvido como modelo padrão Whitelabel.*
