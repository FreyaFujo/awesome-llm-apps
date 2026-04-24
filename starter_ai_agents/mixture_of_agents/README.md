## 🔄 Mixture of Agents LLM App

This Streamlit application demonstrates a Mixture-of-Agents approach: it sends the same question to multiple open-source LLMs in parallel, then asks an aggregator model to synthesize their answers into a single, higher-quality response.

### Features

- Fans a single prompt out to four reference models running on [Together AI](https://www.together.ai/):
  - `Qwen/Qwen2-72B-Instruct`
  - `Qwen/Qwen1.5-72B-Chat`
  - `mistralai/Mixtral-8x22B-Instruct-v0.1`
  - `databricks/dbrx-instruct`
- Aggregates the four responses with `mistralai/Mixtral-8x22B-Instruct-v0.1` using a critical-synthesis system prompt.
- Shows each individual model's answer in an expandable section plus a streaming aggregated answer.
- API key is entered directly in the UI — no `.env` needed.

### How to get Started?

1. Clone the GitHub repository
```bash
git clone https://github.com/Shubhamsaboo/awesome-llm-apps.git
cd awesome-llm-apps/starter_ai_agents/mixture_of_agents
```

2. Install the required dependencies
```bash
pip install -r requirements.txt
```

3. Get your Together AI API Key

- Sign up at [together.ai](https://www.together.ai/) and create an API key in the console.

4. Run the app
```bash
streamlit run mixture-of-agents.py
```

5. Open the URL shown in the console (typically `http://localhost:8501`), paste your Together API key into the password field, enter a question, and click **Get Answer**.

### How it works

1. Your question is sent concurrently (via `asyncio.gather`) to the four reference models.
2. Each model's response is displayed individually.
3. All four responses are concatenated and passed to the aggregator model along with a system prompt instructing it to critically evaluate and synthesize them.
4. The aggregated response is streamed back to the UI token-by-token.

### Notes

- Requires a Together AI account with credits; each question triggers five model calls (four reference + one aggregator).
- Model availability on Together changes over time. If a call fails, swap the deprecated model IDs at the top of `mixture-of-agents.py`.
