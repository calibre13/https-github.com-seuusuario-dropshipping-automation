# 🚀 Sistema Completo de Automação de Dropshipping

Sistema full-stack de automação para dropshipping com sincronização de estoque, repricing automático, rastreio e notificações.

## ✨ Funcionalidades Implementadas

### 🔄 Sincronização Automática de Estoque
- ✅ **AliExpress**: Integração com API para produtos chineses
- ✅ **Dropi**: Fornecedores brasileiros centralizados
- ✅ **Bling/Tiny**: Integração com ERPs brasileiros
- ✅ Atualização automática a cada 30 minutos (configurável)
- ✅ Pausamento automático de produtos sem estoque
- ✅ Logs detalhados de sincronização

### 💰 Repricing Automático
- ✅ **Câmbio em tempo real**: Atualização automática USD/BRL
- ✅ **Cálculo de impostos**: II, IPI, PIS, COFINS, ICMS
- ✅ **Margem configurável**: Define margem por produto ou global
- ✅ Repricing automático 2x ao dia (00:00 e 12:00)
- ✅ Regras de precificação personalizadas
- ✅ Descontos em massa por categoria

### 📦 Rastreio Automático
- ✅ **Correios**: Integração com API dos Correios
- ✅ **China Post**: Rastreio de encomendas internacionais
- ✅ **Melhor Rastreio**: Suporte a múltiplas transportadoras
- ✅ Atualização automática a cada 60 minutos
- ✅ Detecção automática de tipo de rastreio
- ✅ Histórico completo de eventos

### 📧 Notificações Automáticas
- ✅ **Email (SMTP)**: Templates profissionais em HTML
- ✅ **WhatsApp (Twilio)**: Mensagens automáticas formatadas
- ✅ **Gatilhos automáticos**:
  - Pedido confirmado
  - Código de rastreio disponível
  - Saiu para entrega
  - Pedido entregue
- ✅ Notificações em massa por segmento

### 🎯 Automações em Background
- ✅ **APScheduler**: Tarefas programadas
- ✅ **Sincronização**: A cada 30 min
- ✅ **Repricing**: 2x ao dia
- ✅ **Rastreio**: A cada 60 min
- ✅ **Limpeza de carrinhos**: Diariamente às 03:00
- ✅ **Relatório diário**: Enviado às 08:00 para admins

### 👨‍💼 Painel Administrativo
- ✅ Dashboard com estatísticas em tempo real
- ✅ Gerenciamento completo de produtos
- ✅ Controle de pedidos e status
- ✅ Adição de códigos de rastreio
- ✅ Disparo manual de automações
- ✅ Visualização de logs de automação

### 🛒 E-commerce Completo
- ✅ Catálogo de produtos
- ✅ Carrinho de compras
- ✅ Sistema de pedidos
- ✅ Autenticação JWT
- ✅ Perfil de usuário
- ✅ Histórico de compras

## 🏗️ Arquitetura

### Backend (FastAPI + MongoDB)
```
/backend/
├── server.py                    # API principal com todos os endpoints
├── services/
│   ├── supplier_sync.py        # Sincronização com fornecedores
│   ├── repricing.py            # Repricing automático
│   ├── tracking.py             # Rastreio de pedidos
│   └── notifications.py        # Email e WhatsApp
├── tasks/
│   └── automation_tasks.py     # Tarefas em background
├── requirements.txt
└── .env.example
```

## 🚀 Como Usar

### 1. Pré-requisitos

```bash
# Instalar Python 3.10+
python --version

# Instalar MongoDB
# macOS:
brew tap mongodb/brew
brew install mongodb-community

# Ubuntu:
sudo apt-get install mongodb

# Windows: 
# Baixar de https://www.mongodb.com/try/download/community
```

### 2. Configuração

```bash
# Clone ou extraia o projeto
cd dropshipping-automation

# Crie ambiente virtual
python -m venv venv

# Ative o ambiente
# Linux/Mac:
source venv/bin/activate
# Windows:
venv\Scripts\activate

# Instale dependências
cd backend
pip install -r requirements.txt

# Configure variáveis de ambiente
cp .env.example .env
# Edite o .env com suas credenciais
```

### 3. Configurar .env

```bash
# MongoDB
MONGO_URL=mongodb://localhost:27017
DB_NAME=dropshipping_automation

# JWT
JWT_SECRET=sua-chave-secreta-aqui

# APIs de Fornecedores
ALIEXPRESS_API_KEY=sua-chave-aliexpress
DROPI_API_KEY=sua-chave-dropi
BLING_API_KEY=sua-chave-bling

# Rastreio
MELHORRASTREIO_API_KEY=sua-chave-melhorrastreio

# Notificações
TWILIO_ACCOUNT_SID=seu-sid-twilio
TWILIO_AUTH_TOKEN=seu-token-twilio
TWILIO_WHATSAPP_NUMBER=whatsapp:+14155238886

# Email
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=seu-email@gmail.com
SMTP_PASSWORD=sua-senha-de-app

# Automação
AUTO_SYNC_INTERVAL_MINUTES=30
AUTO_REPRICING_ENABLED=true
AUTO_TRACKING_UPDATE_MINUTES=60
```

### 4. Inicie o MongoDB

```bash
# macOS:
brew services start mongodb-community

# Ubuntu:
sudo systemctl start mongodb

# Windows:
# Inicie o serviço MongoDB pelo Services
```

### 5. Inicie o Backend

```bash
cd backend
python server.py

# Ou usando uvicorn:
uvicorn server:app --reload --host 0.0.0.0 --port 8000
```

### 6. Acesse a API

- **API**: http://localhost:8000
- **Documentação**: http://localhost:8000/docs
- **Health Check**: http://localhost:8000/health

## 📊 Endpoints Principais

### Autenticação
```
POST /api/auth/register      # Criar conta
POST /api/auth/login         # Login
GET  /api/auth/me            # Perfil
```

### Produtos
```
GET  /api/products           # Listar produtos
GET  /api/products/{id}      # Detalhes
```

### Pedidos
```
POST /api/orders             # Criar pedido
GET  /api/orders             # Meus pedidos
GET  /api/orders/{id}        # Detalhes
GET  /api/orders/{id}/tracking  # Rastrear
```

### Carrinho
```
GET  /api/cart               # Ver carrinho
POST /api/cart/add           # Adicionar item
```

### Automação (Admin)
```
POST /api/automation/sync        # Disparar sync manual
POST /api/automation/repricing   # Disparar repricing
POST /api/automation/tracking    # Disparar rastreio
GET  /api/automation/stats       # Estatísticas
```

### Admin
```
GET  /api/admin/orders              # Listar pedidos
PUT  /api/admin/orders/{id}/status  # Atualizar status
POST /api/admin/orders/{id}/tracking  # Adicionar rastreio
POST /api/admin/products            # Criar produto
PUT  /api/admin/products/{id}       # Editar produto
GET  /api/admin/dashboard           # Dashboard
```

## 🔧 Configuração das Automações

### Intervalo de Sincronização
```env
# Altere no .env para controlar frequência
AUTO_SYNC_INTERVAL_MINUTES=30  # 30 minutos (padrão)
```

### Habilitar/Desabilitar Repricing
```env
AUTO_REPRICING_ENABLED=true  # true ou false
```

### Intervalo de Rastreio
```env
AUTO_TRACKING_UPDATE_MINUTES=60  # 60 minutos (padrão)
```

## 🎯 Como Integrar Fornecedores

### AliExpress
1. Crie conta em https://portals.aliexpress.com/
2. Obtenha App Key e App Secret
3. Configure no .env:
```env
ALIEXPRESS_API_KEY=sua-app-key
ALIEXPRESS_SECRET=sua-app-secret
```

### Dropi
1. Cadastre-se em https://dropi.com.br
2. Vá em Configurações > API
3. Copie sua API Key:
```env
DROPI_API_KEY=sua-chave-dropi
```

### Bling/Tiny
1. Acesse https://bling.com.br ou https://tiny.com.br
2. Gere uma API Key
3. Configure:
```env
BLING_API_KEY=sua-chave-bling
TINY_API_TOKEN=seu-token-tiny
```

## 📧 Configurar Email (Gmail)

1. Ative verificação em 2 etapas no Gmail
2. Gere uma "Senha de App":
   - Vá em Conta Google > Segurança
   - Senhas de app
   - Selecione "Email" e seu dispositivo
   - Copie a senha de 16 dígitos
3. Configure no .env:
```env
SMTP_USER=seu-email@gmail.com
SMTP_PASSWORD=xxxx xxxx xxxx xxxx
```

## 📱 Configurar WhatsApp (Twilio)

1. Crie conta em https://www.twilio.com
2. Vá em Messaging > Try it Out > Send a WhatsApp message
3. Configure sandbox do WhatsApp
4. Copie credenciais:
```env
TWILIO_ACCOUNT_SID=ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
TWILIO_AUTH_TOKEN=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
TWILIO_WHATSAPP_NUMBER=whatsapp:+14155238886
```

## 📊 Monitoramento

### Logs de Automação
```bash
# Acesse via API
GET /api/automation/stats

# Visualize no MongoDB
use dropshipping_automation
db.automation_logs.find().sort({timestamp: -1}).limit(10)
```

### Estatísticas
```bash
# Dashboard admin
GET /api/admin/dashboard
```

## 🔒 Segurança

- ✅ Senhas criptografadas com bcrypt
- ✅ Autenticação JWT
- ✅ Proteção de rotas admin
- ✅ CORS configurado
- ✅ Validação de dados com Pydantic

## 📦 Deploy em Produção

### Usando Docker (Recomendado)

```dockerfile
# Dockerfile (criar na raiz)
FROM python:3.10-slim

WORKDIR /app

COPY backend/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY backend/ .

CMD ["uvicorn", "server:app", "--host", "0.0.0.0", "--port", "8000"]
```

```bash
# Build e run
docker build -t dropshipping-automation .
docker run -d -p 8000:8000 --env-file backend/.env dropshipping-automation
```

### Deploy na Nuvem

**Heroku:**
```bash
heroku create seu-app-dropshipping
heroku addons:create mongolab
git push heroku main
```

**AWS/GCP/Azure:**
- Use o Dockerfile acima
- Configure MongoDB Atlas para produção
- Use variáveis de ambiente do provedor

## 🧪 Testes

```bash
# Instalar pytest
pip install pytest pytest-asyncio

# Rodar testes
pytest tests/ -v
```

## 📈 Próximos Passos

- [ ] Dashboard frontend em React
- [ ] Integração com Mercado Livre
- [ ] Multi-loja (venda em várias plataformas)
- [ ] IA para precificação dinâmica
- [ ] App mobile
- [ ] Chatbot de atendimento

## 🆘 Suporte

### Problemas Comuns

**Erro de conexão MongoDB:**
```bash
# Verifique se MongoDB está rodando
mongosh
# Se não conectar, inicie o serviço
brew services start mongodb-community  # macOS
sudo systemctl start mongodb           # Linux
```

**Automações não estão rodando:**
```bash
# Verifique logs
tail -f logs/automation.log

# Ou acesse via API
GET /api/automation/stats
```

**Emails não estão sendo enviados:**
- Verifique se habilitou "Senhas de App" no Gmail
- Confirme as credenciais no .env
- Veja os logs em tempo real

## 📝 Licença

MIT License - Livre para uso comercial

## 👨‍💻 Desenvolvido por

Sistema completo de automação de dropshipping desenvolvido para escalar seu negócio sem trabalho manual.

---

**Total de Funcionalidades: 100% Completas** 🎉

**Automações Ativas:**
- ✅ Sincronização de Estoque
- ✅ Repricing Automático
- ✅ Rastreio Automático
- ✅ Notificações Email/WhatsApp
- ✅ Tarefas em Background
- ✅ Relatórios Automáticos
