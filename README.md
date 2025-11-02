ETA ChatBot API

Esta API fornece um sistema de atendimento inteligente utilizando RAG (Retrieval-Augmented Generation), curadoria automática, assistente gerente, roteamento de contexto e memórias persistentes por sessão.
Ela suporta integração com Redis/Mongo ou outros bancos para armazenamento de sessões e memória contextual.

Funcionalidades

Autenticação Bearer Token:	Valida o acesso via header Authorization
Fluxo RAG:	Recupera documentos similares e gera respostas contextuais
Gerente Assistente: Fornece respostas mais formais e estratégicas
Roteador (Router Chain):	Decide automaticamente qual fluxo aplicar
Juiz (Judge Chain):	Avalia se a resposta gerada está coerente
Memória por Sessão:	Recupera histórico de interações do usuário

Requisitos

Python 3.10+
numpy==2.2.2
pymongo==4.11.1
psycopg2-binary==2.9.10
python-dotenv==1.1.0
fastapi==0.116.1
uvicorn==0.35.0
pydantic==2.11.7
google-genai==1.43.0
langchain==0.3.25
langchain-community==0.3.24
langchain-google-genai==2.1.4
redis==6.4.0

Suportar módulos internos:

vector_search.py

chains.py

utils.py

Instalação
git clone https://github.com/seu-repo/eta-chatbot-api.git
cd eta-chatbot-api
pip install -r requirements.txt

Variáveis de Ambiente

Crie um arquivo .env:

api_key= Sua chave de api do gemini
API_TOKEN=Token da API
host_redis=Host do seu banco Redis
password=Senha do seu banco Redis
port_redis=Porta do seu banco Redis
#pg
host =Host do seu banco PGsql
porta =Porta do seu banco PGsql
database =Nome do seu banco PGsql
senha =Senha do seu banco PGsql
user =User do seu banco PGsql

Como Executar
uvicorn main:app --reload


O swagger da API ficará disponível em:

http://127.0.0.1:8000/docs

Formato das Requisições:
POST /chat
Headers
Authorization: Bearer <API_TOKEN>

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

Exemplo de Uso com cURL
curl -X POST http://127.0.0.1:8000/chat?email=usuario@teste.com \
-H "Content-Type: application/json" \
-H "Authorization: Bearer SEU_TOKEN" \
-d '{
  "user_message": "Quero saber como solicitar cartão.",
  "api_key": "SUA_API_KEY"
}'

Endpoint de Health Check para evitar a API de morrer
GET /health


Exemplo de retorno:

{
  "status": "ok",
  "timestamp": "2025-11-02T14:30:00"
}

Estrutura Recomendada do Projeto
/project
|-- main.py
|-- chains.py
|-- vector_search.py
|-- utils.py
|-- .env
|-- requirements.txt
|-- pg_tools.py
|-- redis_tools.py
|-- prompts.py
