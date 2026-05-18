# 📧 Autonomous Email Assistant with LangGraph & Long-Term Memory

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/downloads/)
[![LangGraph](https://img.shields.io/badge/LangGraph-State_of_the_Art-orange.svg)](https://python.langchain.com/docs/langgraph)
[![LLM](https://img.shields.io/badge/LLM-Gemini_1.5_Flash-green.svg)](https://ai.google.dev/)
[![Status](https://img.shields.io/badge/Status-Completed-success.svg)]()

> **O fim da amnésia artificial.** Um assistente de e-mail 100% autônomo capaz de ler caixas de entrada, rotear ações de forma determinística, acionar ferramentas reais (como checagem de calendário) e manter memória de longo prazo vetorial.

Este projeto é a consolidação de uma jornada profunda na orquestração de Agentes de Inteligência Artificial (LLMs), saindo dos tradicionais *chatbots* para construir um ecossistema com capacidade de decisão, execução e retenção de contexto contínuo.

---

## Arquitetura do Projeto

A aplicação foi desenvolvida focando em três pilares fundamentais da engenharia de IA moderna: Roteamento Estruturado, Ação Autônoma e Memória Semântica.

### 1. Roteamento Inteligente e Determinístico (Triage Router)
LLMs puros podem ser imprevisíveis. Para garantir confiabilidade corporativa, implementei um sistema de triagem (`triage_router`) utilizando **Pydantic**.
* O agente lê o e-mail e é forçado a devolver a classificação no formato estruturado (JSON).
* **Decisões:** O e-mail é classificado rigorosamente entre `Responder`, `Ignorar` (como spams/newsletters) ou `Notificar` (alertas críticos).
* Esta trava garante que o fluxo no `StateGraph` siga a rota correta sem alucinações.

### 2. Ação e Execução via Ferramentas (Tools)
O assistente não é apenas um gerador de texto; ele toma atitudes no mundo real.
* Utilizando a abstração `create_react_agent` e o decorador `@tool` do Python, o agente acessa funções customizadas.
* **Ferramentas Ativas:** Ele é capaz de rodar `check_calendar_availability` (verificar horários), `schedule_meeting` (agendar reuniões) e enviar e-mails de resposta proativamente, dependendo do roteamento decidido no passo 1.

### 3. Memória de Longo Prazo e Embeddings (O Pulo do Gato)
Para resolver a "amnésia" comum aos LLMs entre execuções, integrei o framework **Langmem**.
* O agente possui ferramentas próprias (`manage_memory_tool` e `search_memory_tool`) para ler e salvar o próprio contexto.
* Utilizando **Google Embeddings**, as informações relevantes são transformadas em vetores e salvas em um banco de dados (`InMemoryStore`).
* Antes de formular qualquer resposta ou ação, a IA realiza uma busca semântica em milissegundos, permitindo aprendizado contínuo sobre o usuário (neste projeto simulado pela persona de *Sarah Chen, Engenheira de Software Sênior*).

---

## Como Executar Localmente

### Pré-requisitos
* Python 3.10+
* Chaves de API do [Google Gemini](https://aistudio.google.com/) e do [Tavily](https://tavily.com/) (caso ative buscas web adicionais).

### Passos de Instalação

1. **Clone o repositório:**
   ```bash
   git clone [https://github.com/SEU_USUARIO/autonomous-email-assistant.git](https://github.com/SEU_USUARIO/autonomous-email-assistant.git)
   cd autonomous-email-assistant
2. **Crie e ative um ambiente virtual:**
   python -m venv venv
  # No Windows:
  venv\Scripts\activate
  # No Linux/Mac:
  source venv/bin/activate
# Estrutura de Arquivos de Destaque
MultiAg.ipynb: Introdução ao Roteamento Determinístico (Pydantic), configuração da classe Router e criação das Ferramentas básicas (@tool). A orquestração final (Capstone). Implementação do StateGraph completo, união do roteador com as ferramentas de ação e a introdução decisiva da Memória Vetorial (Langmem + Embeddings).
