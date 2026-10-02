# 📘 MEMÓRIA DO PROJETO - ITACRED CRM (INSTÂNCIA DEDICADA)

## 📌 Contexto & Histórico de Migração
Esta instância foi gerada a partir da matriz **Painel CRM Whitelabel**. 
A aplicação foi completamente arquitetada e isolada para a empresa **ITACRED**, garantindo total separação de banco de dados, identidade visual, portas de servidor e armazenamento de documentos.

---

## ⚙️ Configurações da Instância ITACRED

### 1. Arquivo de Ambiente (.env)
O arquivo `.env` foi configurado com os seguintes parâmetros:
- **PORT**: `3001` (evitando conflito com a matriz na 3000).
- **JWT_SECRET**: `itacred_crm_secret_key_2026_safe`
- **COMPANY_NAME**: `"ITACRED"`
- **COMPANY_LOGO_URL**: `"assets/logo_itacred.jpg"`
- **COMPANY_FAVICON_URL**: `"assets/favicon_itacred.jpg"`
- **DATABASE_URL**: `"postgres://itacred:yyE8akX7cnsjRYDn@localhost:5432/itacred"`
- **GOOGLE_DRIVE_PARENT_FOLDER_ID**: `"11IlThCLIExkJmGGxuTpXIXqnLbm61TjY"`
- **APP_URL**: `"https://itacred.vps11814.panel.icontainer.work"`
- **GOOGLE_REDIRECT_URI**: `"https://itacred.vps11814.panel.icontainer.work/api/crm/auth/google/callback"`


---

## 🎨 Identidade Visual (Whitelabel Dinâmico)
Toda a interface (título da página, logos do cabeçalho e menu lateral, nome da empresa) é carregada dinamicamente via backend pelo endpoint `GET /api/whitelabel/config` consumido pelo script `public/js/auth.js`.

- Elementos HTML com a classe `.app-company-name` atualizam o nome para **ITACRED**.
- Elementos HTML com a classe `.app-company-logo` atualizam a imagem para a logo da ITACRED.

---

## 🚀 Passo a Passo para Inicialização da ITACRED

### Step 1: Banco de Dados PostgreSQL
Crie o banco de dados dedicado no PostgreSQL:
```sql
CREATE DATABASE crm_itacred_db;
```

### Step 2: Imagens de Identidade Visual
Adicione as imagens da marca ITACRED na pasta de assets:
- `public/assets/logo_itacred.jpg`
- `public/assets/favicon_itacred.jpg`

### Step 3: Instalação e Execução Local
```bash
npm install
node server.js
```
Acesse no navegador: `http://localhost:3001`

### Step 4: Execução em Produção (VPS via PM2)
```bash
pm2 start server.js --name "crm-itacred"
```

---

## 🧩 Módulos e Recursos Prontos
1. **Autenticação & RBAC**: Controle de perfil (Admin, Supervisor, SDR, Closer).
2. **Kanban SDR**: Prospecção, qualificação e agendamento.
3. **Kanban Closer**: Atendimento comercial e fechamento de propostas.
4. **Fila de Closers & Rodízio**: Distribuição automática de leads por regras de SLA.
5. **Relatórios & KPIs**: Dashboard analítico em tempo real.
6. **Integração Google Drive**: Organização de anexos em pasta dedicada.

---
*Documento de Memória gerado automaticamente para continuidade em novos chats e ambientes.*
