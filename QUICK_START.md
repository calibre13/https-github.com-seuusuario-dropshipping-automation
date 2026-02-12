# 🚀 GUIA RÁPIDO DE INÍCIO

## Opção 1: Setup Rápido (Recomendado)

```bash
# 1. Torne o script executável
chmod +x setup.sh

# 2. Execute o setup
./setup.sh

# 3. Inicie o MongoDB
# macOS:
brew services start mongodb-community

# Linux:
sudo systemctl start mongodb

# 4. Inicie o servidor
cd backend
source venv/bin/activate
python server.py
```

## Opção 2: Docker (Mais Fácil)

```bash
# 1. Build e inicie os containers
docker-compose up -d

# 2. Popular banco de dados
docker-compose exec backend python seed_database.py

# Pronto! API rodando em http://localhost:8000
```

## Opção 3: Manual

```bash
# 1. Crie ambiente virtual
cd backend
python3 -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 2. Instale dependências
pip install -r requirements.txt

# 3. Configure .env
cp .env.example .env
# Edite o .env com suas credenciais

# 4. Inicie MongoDB
brew services start mongodb-community  # ou: sudo systemctl start mongodb

# 5. Popular banco (opcional)
python seed_database.py

# 6. Inicie servidor
python server.py
```

## 🔐 Credenciais de Teste

Após popular o banco:

**Admin:**
- Email: admin@dropshipping.com
- Senha: admin123

**Cliente:**
- Email: joao@email.com
- Senha: cliente123

## 📍 URLs Importantes

- **API**: http://localhost:8000
- **Documentação**: http://localhost:8000/docs
- **Health Check**: http://localhost:8000/health

## 🎯 Primeiros Testes

### 1. Testar API
```bash
curl http://localhost:8000/health
```

### 2. Fazer Login
```bash
curl -X POST http://localhost:8000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "admin@dropshipping.com",
    "password": "admin123"
  }'
```

### 3. Listar Produtos
```bash
curl http://localhost:8000/api/products
```

### 4. Disparar Sincronização (Admin)
```bash
# Primeiro faça login e pegue o token
# Depois:
curl -X POST http://localhost:8000/api/automation/sync \
  -H "Authorization: Bearer SEU_TOKEN_AQUI"
```

## ⚙️ Configurar Automações

### 1. APIs de Fornecedores

Edite o `.env`:

```bash
# AliExpress
ALIEXPRESS_API_KEY=sua-chave
ALIEXPRESS_SECRET=seu-secret

# Dropi
DROPI_API_KEY=sua-chave

# Bling
BLING_API_KEY=sua-chave
```

### 2. Notificações

```bash
# Email (Gmail)
SMTP_USER=seu-email@gmail.com
SMTP_PASSWORD=sua-senha-de-app

# WhatsApp (Twilio)
TWILIO_ACCOUNT_SID=seu-sid
TWILIO_AUTH_TOKEN=seu-token
TWILIO_WHATSAPP_NUMBER=whatsapp:+14155238886
```

### 3. Ajustar Intervalos

```bash
# Sincronização a cada 15 minutos
AUTO_SYNC_INTERVAL_MINUTES=15

# Rastreio a cada 30 minutos
AUTO_TRACKING_UPDATE_MINUTES=30
```

## 📊 Monitorar Automações

### Via API
```bash
# Estatísticas
curl http://localhost:8000/api/automation/stats \
  -H "Authorization: Bearer SEU_TOKEN"

# Dashboard Admin
curl http://localhost:8000/api/admin/dashboard \
  -H "Authorization: Bearer SEU_TOKEN"
```

### Via MongoDB
```bash
mongosh

use dropshipping_automation

# Ver logs de automação
db.automation_logs.find().sort({timestamp: -1}).limit(10)

# Ver produtos
db.products.find()

# Ver pedidos
db.orders.find()
```

## 🔧 Comandos Úteis

### Docker
```bash
# Ver logs
docker-compose logs -f backend

# Reiniciar
docker-compose restart backend

# Parar tudo
docker-compose down

# Rebuild após mudanças
docker-compose up -d --build
```

### MongoDB
```bash
# Conectar
mongosh

# Backup
mongodump --db dropshipping_automation --out backup/

# Restore
mongorestore backup/dropshipping_automation
```

### Python
```bash
# Ativar ambiente
source venv/bin/activate

# Instalar nova dependência
pip install nome-pacote
pip freeze > requirements.txt

# Desativar ambiente
deactivate
```

## 🆘 Problemas Comuns

### "MongoDB connection failed"
```bash
# Verifique se MongoDB está rodando
mongosh
# Se não conectar, inicie:
brew services start mongodb-community  # macOS
sudo systemctl start mongodb           # Linux
```

### "Port 8000 already in use"
```bash
# Encontre processo usando porta
lsof -i :8000
# Mate o processo
kill -9 PID
```

### "Module not found"
```bash
# Certifique-se de estar no venv
source venv/bin/activate
# Reinstale dependências
pip install -r requirements.txt
```

## 📖 Documentação Completa

Veja o arquivo **README.md** para documentação completa incluindo:
- Todos os endpoints da API
- Exemplos de uso
- Configuração avançada
- Deploy em produção
- E muito mais!

## 🎉 Pronto para Começar!

Seu sistema de automação de dropshipping está configurado.

Próximos passos:
1. Configure suas chaves de API no .env
2. Teste as automações manualmente
3. Configure os intervalos desejados
4. Monitore os logs
5. Escale seu negócio! 🚀
