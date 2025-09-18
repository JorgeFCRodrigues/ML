# Visualizador STRIDE – Modelo de Ameaças

Aplicação web que gera **modelos de ameaças STRIDE** a partir de um **desenho de arquitetura (imagem)** e informações fornecidas pelo usuário.  
A análise é feita usando a **API do Azure OpenAI**, e os resultados são exibidos em texto e em um **grafo interativo** com Cytoscape.

## 🏗️ Estrutura do Projeto

```
.
├─ main.py        # API FastAPI que recebe dados, envia para o Azure OpenAI e retorna o modelo de ameaças
├─ index.html     # Interface web (formulário + visualização de grafo)
└─ .env           # Variáveis de ambiente com credenciais do Azure OpenAI
```

## ✨ Funcionalidades

- Upload de **imagem da arquitetura** (ex.: diagrama do sistema).  
- Formulário para informar:
  - Tipo de aplicação
  - Métodos de autenticação
  - Exposição na internet
  - Dados sensíveis
  - Descrição detalhada da aplicação
- Geração de **modelo de ameaças STRIDE** (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege).
- Exibição do resultado em:
  - **Texto** (JSON formatado vindo do modelo).
  - **Grafo interativo** com Cytoscape e opção de impressão.

## 🚀 Tecnologias

- **Backend:** [FastAPI](https://fastapi.tiangolo.com/)  
- **Frontend:** HTML5, Bootstrap 5, Cytoscape.js  
- **IA:** [Azure OpenAI](https://learn.microsoft.com/azure/ai-services/openai/overview)  
- **Outros:** Python 3.10+, dotenv, base64

## ⚙️ Pré-requisitos

- Python 3.10 ou superior
- Conta e deployment no **Azure OpenAI**
- Node/servidor estático (opcional, apenas se quiser servir o `index.html` fora do FastAPI)

## 🔑 Variáveis de Ambiente

Crie um arquivo `.env` na raiz (já existe um modelo) com:

```env
AZURE_OPENAI_API_KEY=your_api_key_here
AZURE_OPENAI_ENDPOINT=https://your-resource-name.openai.azure.com/
AZURE_OPENAI_API_VERSION=2025-01-01-preview
AZURE_OPENAI_DEPLOYMENT_NAME=your_deployment_name_here
```

⚠️ **Nunca** faça commit do `.env` com credenciais reais.

## 🖥️ Como Executar

1. **Instalar dependências**:

   ```bash
   pip install fastapi uvicorn python-dotenv openai
   ```

2. **Rodar o backend**:

   ```bash
   uvicorn main:app --host 0.0.0.0 --port 8001 --reload
   ```

3. **Abrir o frontend**:

   - Basta abrir o arquivo `index.html` no navegador  
     *(ou servir com um servidor estático, se preferir)*.

4. **Testar**:

   - Acesse o formulário, envie os dados e aguarde a geração do modelo de ameaças.

## 📂 Endpoints Principais

- `POST /analisar_ameacas`  
  Recebe:
  - `imagem` (arquivo)
  - `tipo_aplicacao`, `autenticacao`, `acesso_internet`, `dados_sensiveis`, `descricao_aplicacao`  
  Retorna: JSON com `threat_model` e `improvement_suggestions`.

## 🛡️ Licença

Defina a licença desejada (ex.: MIT, Apache-2.0).  
