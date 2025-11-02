# ETA ChatBot API

Esta API fornece um sistema de atendimento inteligente utilizando **RAG (Retrieval-Augmented Generation)**, **curadoria automática**, **assistente gerente**, **roteamento de contexto** e **memórias persistentes por sessão**.  
Suporta integração com **Redis**, **PostgreSQL** e outros bancos para armazenamento de dados e contexto.

---

## ✨ Funcionalidades

| Componente | Descrição |
|-----------|-----------|
| **Autenticação Bearer Token** | Valida o acesso via header `Authorization` |
| **Fluxo RAG** | Recupera documentos similares e gera respostas contextualizadas |
| **Gerente Assistente** | Fornece respostas formais e estratégicas |
| **Roteador (Router Chain)** | Determina automaticamente o fluxo ideal |
| **Juiz (Judge Chain)** | Avalia a coerência da resposta final |
| **Memória por Sessão** | Recupera histórico customizado de cada usuário |

---

## 📦 Requisitos

| Dependência | Versão |
|------------|--------|
| Python | 3.10+ |
| numpy | 2.2.2 |
| pymongo | 4.11.1 |
| psycopg2-binary | 2.9.10 |
| python-dotenv | 1.1.0 |
| fastapi | 0.116.1 |
| uvicorn | 0.35.0 |
| pydantic | 2.11.7 |
| google-genai | 1.43.0 |
| langchain | 0.3.25 |
| langchain-community | 0.3.24 |
| langchain-google-genai | 2.1.4 |
| redis | 6.4.0 |

**Módulos internos necessários:**

vector_search.py
chains.py
utils.py

---

## 🛠 Instalação

git clone https://github.com/seu-repo/eta-chatbot-api.git
cd eta-chatbot-api
pip install -r requirements.txt
🔐 Variáveis de Ambiente
Crie um arquivo .env na raiz do projeto:


api_key=SUA_CHAVE_DO_GEMINI
API_TOKEN=TOKEN_DA_API

# Redis
host_redis=HOST_REDIS
password=SENHA_REDIS
port_redis=PORTA_REDIS

# PostgreSQL
host=HOST_POSTGRES
porta=PORTA_POSTGRES
database=NOME_BANCO
senha=SENHA_BANCO
user=USUARIO_BANCO

▶️ Como Executar

uvicorn main:app --reload
Acesse documentação Swagger:


http://127.0.0.1:8000/docs
📡 Formato da Requisição
POST /chat
Headers

Authorization: Bearer <API_TOKEN>
Content-Type: application/json
Body

{
  "user_message": "Como posso abrir uma conta?",
  "api_key": "SUA_API_KEY_LLM"
}
Resposta

{
  "resposta": "Aqui está sua resposta processada...",
  "origem": "RAG | CURADORIA | GERENTE | CURADORIA_RAG | CURADORIA_GERENTE"
}
🧪 Exemplo via cURL

curl -X POST http://127.0.0.1:8000/chat?email=usuario@teste.com \
-H "Content-Type: application/json" \
-H "Authorization: Bearer SEU_TOKEN" \
-d '{
  "user_message": "Quero saber como solicitar cartão.",
  "api_key": "SUA_API_KEY"
}'
💓 Health Check
GET /health
Retorno:

{
  "status": "ok",
  "timestamp": "2025-11-02T14:30:00"
}
Use esse endpoint para manter a API ativa através de cronjob / UptimeRobot / Ping externo.

🗂 Estrutura Recomendada

/project
|-- main.py
|-- chains.py
|-- vector_search.py
|-- utils.py
|-- pg_tools.py
|-- redis_tools.py
|-- prompts.py
|-- .env
|-- requirements.txt
