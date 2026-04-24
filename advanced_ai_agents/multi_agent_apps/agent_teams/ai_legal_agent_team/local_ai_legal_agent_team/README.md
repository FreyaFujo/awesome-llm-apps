# 👨‍⚖️ Local AI Legal Agent Team

A fully local variant of the [AI Legal Agent Team](../README.md). Instead of calling OpenAI and Qdrant Cloud, this version runs the language model locally with [Ollama](https://ollama.com) and stores embeddings in a self-hosted [Qdrant](https://qdrant.tech) instance — no API keys, no outbound requests for inference, and your documents stay on your machine.

## Features

- **Specialized Legal AI Agent Team** (same roles as the cloud version, all powered by a local Llama 3.1 8B model via Ollama)
  - **Legal Researcher** — finds and cites relevant precedents from the uploaded document.
  - **Contract Analyst** — reviews clauses, obligations, and potential issues.
  - **Legal Strategist** — synthesizes risks, opportunities, and recommendations.
  - **Team Lead** — coordinates the three agents into a single response.

- **Document Analysis Types**
  - Contract Review
  - Legal Research
  - Risk Assessment
  - Compliance Check
  - Custom Query

- **Fully Local Stack**
  - LLM: Ollama running `llama3.1:8b`
  - Embeddings: Ollama running `openhermes`
  - Vector store: Qdrant at `http://localhost:6333`

## Prerequisites

1. **Install Ollama** — follow the instructions at [ollama.com](https://ollama.com), then pull the models:
   ```bash
   ollama pull llama3.1:8b
   ollama pull openhermes
   ```

2. **Run Qdrant locally** (Docker is the easiest option):
   ```bash
   docker run -p 6333:6333 -p 6334:6334 qdrant/qdrant
   ```

## How to Run

1. **Setup Environment**
   ```bash
   git clone https://github.com/Shubhamsaboo/awesome-llm-apps.git
   cd awesome-llm-apps/advanced_ai_agents/multi_agent_apps/agent_teams/ai_legal_agent_team/local_ai_legal_agent_team

   pip install -r requirements.txt
   ```

2. **Make sure Ollama and Qdrant are running** (see Prerequisites).

3. **Run the Application**
   ```bash
   streamlit run local_legal_agent.py
   ```

4. **Use the Interface**
   - Upload a legal document (PDF)
   - Select an analysis type
   - Add a custom query if needed
   - View analysis, key points, and recommendations

## Notes

- Supports PDF documents only.
- First run will be slower while Ollama loads the models into memory.
- Quality of analysis depends on the local model; expect the cloud variant (GPT-4o) to produce stronger results for complex documents.
- No data leaves your machine — suitable for sensitive or privileged material.
