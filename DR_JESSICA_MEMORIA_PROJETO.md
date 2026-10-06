# MEMÓRIA DE PROJETO - DRA. JÉSSICA CRM

Este repositório contém a aplicação CRM whitelabel configurada exclusivamente para a **Dra. Jéssica**.

---

## 📌 1. Especificações da Instância

- **Nome da Empresa**: Dra. Jéssica
- **Repositório GitHub**: `https://github.com/Webber03/atendi-DrJessica`
- **Domínio Público**: `https://drjessica.vps11814.panel.icontainer.work`
- **Alias WWW**: `www.drjessica.vps11814.panel.icontainer.work`
- **Porta Externa / Servidor**: `3002`
- **Porta Interna da Aplicação (Container / Node)**: `3000`
- **Secret JWT**: `drjessica_crm_secret_key_2026_safe`
- **Assets de Marca**:
  - Logo: `public/assets/logo_drjessica.jpg`
  - Favicon: `public/assets/favicon_drjessica.jpg`

---

## 🗄️ 2. Banco de Dados PostgreSQL Dedicado

- **Host**: `localhost` (ou host do PostgreSQL no container/painel)
- **Porta**: `5432`
- **Usuário**: `drjessica`
- **Senha**: `6BP444fWNie7tm7S`
- **Nome do Banco de Dados**: `crm_drjessica_db` (ou `drjessica`)
- **Permissão**: `Super Usuário`
- **String de Conexão (`DATABASE_URL`)**:
  ```env
  DATABASE_URL="postgres://drjessica:6BP444fWNie7tm7S@localhost:5432/crm_drjessica_db"
  ```

### Script de Criação no PostgreSQL:
```sql
CREATE USER drjessica WITH PASSWORD '6BP444fWNie7tm7S' SUPERUSER;
CREATE DATABASE crm_drjessica_db OWNER drjessica;
GRANT ALL PRIVILEGES ON DATABASE crm_drjessica_db TO drjessica;
```

---

## 🚀 3. Instruções de Deploy

### Opção A: Deploy no Painel iContainer / Docker Standalone
1. **Domínio e SSL**:
   - Domínio principal: `drjessica.vps11814.panel.icontainer.work`
   - Incluir alias: `www.drjessica.vps11814.panel.icontainer.work`
   - Marcar: *Emitir SSL automaticamente e forçar HTTPS*.
2. **Configuração de Portas**:
   - Porta da aplicação: `3000`
   - Porta externa: `3002`
3. **Variáveis de Ambiente (`.env`)**:
   ```env
   PORT=3000
   JWT_SECRET=drjessica_crm_secret_key_2026_safe
   COMPANY_NAME="Dra. Jéssica"
   COMPANY_LOGO_URL="assets/logo_drjessica.jpg"
   COMPANY_FAVICON_URL="assets/favicon_drjessica.jpg"
   DATABASE_URL="postgres://drjessica:6BP444fWNie7tm7S@localhost:5432/crm_drjessica_db"
   APP_URL="https://drjessica.vps11814.panel.icontainer.work"
   GOOGLE_REDIRECT_URI="https://drjessica.vps11814.panel.icontainer.work/api/crm/auth/google/callback"
   ```

---

### Opção B: Deploy Direto na VPS (Node.js + PM2 + Nginx)

1. **Clonar Repositório e Instalar Dependências**:
   ```bash
   cd /var/www
   git clone https://github.com/Webber03/atendi-DrJessica.git painel-crm-drjessica
   cd painel-crm-drjessica
   npm install
   ```

2. **Criar Arquivo `.env`**:
   Salvar as variáveis na raiz da pasta `painel-crm-drjessica`.

3. **Iniciar Processo com PM2**:
   ```bash
   pm2 start server.js --name "crm-drjessica"
   pm2 save
   ```

4. **Configuração do Nginx (Reverse Proxy)**:
   Adicionar no arquivo `/etc/nginx/sites-available/drjessica`:
   ```nginx
   server {
       server_name drjessica.vps11814.panel.icontainer.work www.drjessica.vps11814.panel.icontainer.work;

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
   Recarregar Nginx:
   ```bash
   sudo systemctl reload nginx
   ```
