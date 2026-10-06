# MEMÓRIA DE PROJETO - DRA. JÉSSICA CRM

Este repositório contém a aplicação CRM whitelabel configurada exclusivamente para a **Dra. Jéssica**.

---

## 📌 1. Especificações da Instância

- **Nome do Cliente**: Dra. Jéssica
- **Repositório GitHub**: `https://github.com/Webber03/atendi-DrJessica`
- **Porta do Servidor (Node.js)**: `3002`
- **URL Pública**: `https://drjessica.vps11814.panel.icontainer.work`
- **Banco de Dados PostgreSQL**:
  - **Host**: `localhost`
  - **Porta**: `5432`
  - **Database**: `drjessica`
  - **Usuário**: `drjessica`
  - **Senha**: `6BP444fWNie7tm7S`
  - **URL de Conexão**: `postgres://drjessica:6BP444fWNie7tm7S@localhost:5432/drjessica`

---

## 🚀 2. Comandos de Deploy no Servidor (VPS)

### A. Clonar Repositório & Instalar Dependências
```bash
cd /var/www
git clone https://github.com/Webber03/atendi-DrJessica.git painel-crm-drjessica
cd painel-crm-drjessica
npm install
```

### B. Configurar o arquivo `.env`
Criar o arquivo `.env` na raiz do projeto com o seguinte conteúdo:
```env
PORT=3002
JWT_SECRET=drjessica_crm_secret_key_2026_safe
COMPANY_NAME="Dra. Jéssica"
COMPANY_LOGO_URL="assets/logo_drjessica.jpg"
COMPANY_FAVICON_URL="assets/favicon_drjessica.jpg"
DATABASE_URL="postgres://drjessica:6BP444fWNie7tm7S@localhost:5432/drjessica"
APP_URL="https://drjessica.vps11814.panel.icontainer.work"
GOOGLE_REDIRECT_URI="https://drjessica.vps11814.panel.icontainer.work/api/crm/auth/google/callback"
```

### C. Configurar o Banco de Dados no PostgreSQL (Painel / Terminal)
```sql
CREATE USER drjessica WITH PASSWORD '6BP444fWNie7tm7S' SUPERUSER;
CREATE DATABASE drjessica OWNER drjessica;
GRANT ALL PRIVILEGES ON DATABASE drjessica TO drjessica;
```

### D. Executar com PM2
```bash
pm2 start server.js --name "crm-drjessica"
pm2 save
```

### E. Configurar Proxy Nginx
Adicionar o bloco do servidor no Nginx (`/etc/nginx/sites-available/drjessica`):
```nginx
server {
    server_name drjessica.vps11814.panel.icontainer.work;

    location / {
        proxy_pass http://localhost:3002;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```
E recarregar o Nginx:
```bash
sudo systemctl reload nginx
```
