# Comprehensive AI Providers Reference 🚀

A curated, developer-first index of AI API providers, official base URLs, authentication formats, model tracking, and free-tier availability. This repository serves as a cheat sheet and infrastructure guide for configuring multi-LLM applications, fallback routers, or tools like **LiteLLM**, **OpenWebUI**, and **LangChain**.

**Last updated: November 2026** · 120+ providers · 4 API patterns

---

## 🗺️ Quick Reference Matrix

| Provider | API Format | Base URL Prefix | Auth Method | Free Tier? |
| :--- | :--- | :--- | :--- | :--- |
| **OpenAI** | Pattern A (OpenAI-Compat) | `https://api.openai.com/v1` | `Authorization: Bearer sk-...` | ❌ No |
| **Anthropic** | Pattern B (Messages API) | `https://api.anthropic.com` | `x-api-key` + `anthropic-version` | ❌ No (Web only) |
| **Google Gemini** | Pattern B / A (`/v1beta/openai/`) | `https://generativelanguage.googleapis.com/v1beta` | `x-goog-api-key` OR `?key=` | ✅ Yes (Console tracked) |
| **Mistral AI** | Pattern A (OpenAI-Compat) | `https://api.mistral.ai/v1` | `Authorization: Bearer ...` | ✅ Yes (Free Mode) |
| **DeepSeek** | Pattern A & Pattern B | `https://api.deepseek.com` | `Authorization: Bearer ...` | ❌ No (Low cost) |
| **Groq** | Pattern A (OpenAI-Compat) | `https://api.groq.com/openai/v1` | `Authorization: Bearer ...` | ✅ Yes (Generous RPD) |
| **OpenRouter** | Pattern A (OpenAI-Compat) | `https://openrouter.ai/api/v1` | `Authorization: Bearer ...` | ✅ Yes (`:free` variants) |
| **GitHub Models** | Pattern A (OpenAI-Compat) | `https://models.inference.ai.azure.com` | `Authorization: Bearer $PAT` | ✅ Yes (Tiered limits) |
| **NVIDIA NIM** | Pattern A (OpenAI-Compat) | `https://integrate.api.nvidia.com/v1` | `Authorization: Bearer nvapi-...` | ✅ Yes (~40 RPM) |
| **Cloudflare AI** | Custom / Pattern A | `https://api.cloudflare.com/client/v4/accounts/{id}/ai` | `Authorization: Bearer $CF_TOKEN` | ✅ Yes (10k Neurons/day) |
| **Pollinations** | Pattern C (URL-Based) | `https://text.pollinations.ai` | None required | ✅ Yes (Unlimited) |

> 💡 **Base URLs above are the real API endpoints**, not the homepage — copy-paste ready for `base_url=` in any OpenAI-compatible client.

---

## ⚡ Quick Start (6 lines to any provider)

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://api.groq.com/openai/v1",   # 🔗 change this
    api_key="YOUR_KEY",                          # 🔐 and this
)

resp = client.chat.completions.create(
    model="openai/gpt-oss-120b",
    messages=[{"role": "user", "content": "Hello"}],
)
print(resp.choices[0].message.content)
```

Not OpenAI-compatible? It's almost certainly one of the other two patterns below. 👇

---

## 🧱 Universal API Format Patterns (Cheat Sheet)

~80% of providers follow **Pattern A**. If you are building an ingestion layer, normalize to this pattern first.

### 🔹 Pattern A: OpenAI-Compatible (Most Common)

- **Endpoints:** `POST {base_url}/chat/completions`, `POST {base_url}/embeddings`, `POST {base_url}/images/generations`, `GET {base_url}/models`
- **Headers:**

```http
Authorization: Bearer {api_key}
Content-Type: application/json
```

- **Request body:**

```json
{
  "model": "model-name",
  "messages": [
    {"role": "system", "content": "..."},
    {"role": "user", "content": "..."}
  ],
  "temperature": 0.7,
  "max_tokens": 1024,
  "stream": false
}
```

- **Providers:** OpenAI, Groq, Together, Fireworks, Cerebras, SambaNova, DeepInfra, OpenRouter, DeepSeek, xAI, Novita, Hyperbolic, AIML API, Qwen/DashScope, Zhipu, Moonshot, Yi, MiniMax, iFlow, LongCat, Ollama, LM Studio, vLLM, LocalAI.

### 🔹 Pattern B: Custom REST (Anthropic / Native Style)

- **Endpoints:** `POST {base_url}/messages` (Anthropic) or unique runtime paths (AWS Bedrock, Azure, Vertex).
- **Headers (Anthropic Example):**

```http
x-api-key: {api_key}
anthropic-version: 2023-06-01
Content-Type: application/json
```

- **Providers:** Anthropic, Google Gemini (native), Cohere, AI21, AWS Bedrock.

### 🔹 Pattern C: URL-Based (No Auth)

- **Format:** `GET {base_url}/{prompt}` or inline parameters.
- **Providers:** Pollinations.

### 🔹 Pattern D: WebSocket Streaming (Realtime)

- **Used for:** voice, live transcription, realtime multimodal.
- **Providers:** OpenAI Realtime (`wss://api.openai.com/v1/realtime`), Gemini Live, Deepgram Streaming, LiveKit.

---

## 🏛️ LLM Foundation Labs

| Provider | Base URL | Auth | Format | Free Tier |
| :--- | :--- | :--- | :--- | :--- |
| **OpenAI** | `https://api.openai.com/v1` | `Bearer sk-...` | A | ❌ |
| **Anthropic** | `https://api.anthropic.com` | `x-api-key` + version | B | ❌ |
| **Google Gemini** | `https://generativelanguage.googleapis.com/v1beta` | API key | B / A | ✅ |
| **Mistral** | `https://api.mistral.ai/v1` | Bearer | A | ✅ |
| **DeepSeek** | `https://api.deepseek.com` | Bearer | A + B | ❌ (cheap) |
| **Cohere** | `https://api.cohere.com/v1` | Bearer | B + A | 🎟️ Trial |
| **AI21** | `https://api.ai21.com/studio/v1` | Bearer | B | 🎟️ Trial |
| **xAI (Grok)** | `https://api.x.ai/v1` | Bearer | A | 🎟️ Trial |
| **Reka AI** | `https://api.reka.ai` | Bearer | B | — |

> 🧠 **GPT-5** (400K context, Aug 2025): `$1.25 / $10.00` per 1M tokens (in/out).
> 🧠 **Claude 4 family** — 200K context, strong at coding & agentic tool use.
> 🧠 **Gemini 2.5 Pro** — up to 2M context, best free tier for high-volume work.

---

## 🚀 Open-Source Hosting & Inference

| Provider | Base URL | Auth | Free Tier |
| :--- | :--- | :--- | :--- |
| **Together AI** | `https://api.together.xyz/v1` | Bearer | 💳 $5 credit |
| **Fireworks AI** | `https://api.fireworks.ai/inference/v1` | Bearer | 💳 $1 credit |
| **Groq** | `https://api.groq.com/openai/v1` | Bearer | ✅ Generous |
| **Cerebras** | `https://api.cerebras.ai/v1` | Bearer | ⚠️ 💳 $5 (card req.) |
| **SambaNova** | `https://api.sambanova.ai/v1` | Bearer | ⚠️ Tightened Sep 2026 |
| **Replicate** | `https://api.replicate.com/v1` | Bearer | 💳 $5 credit |
| **DeepInfra** | `https://api.deepinfra.com/v1/openai` | Bearer | 💳 $5 credit |
| **fal.ai** | `https://fal.run` / `https://queue.fal.run` | `Authorization: Key <FAL_KEY>` | ❌ Pay-per-use |
| **Novita** | `https://api.novita.ai/v3/openai` | Bearer | 💳 $0.50 credit |
| **Hyperbolic** | `https://api.hyperbolic.xyz/v1` | Bearer | ✅ Limited |
| **Modal** | Serverless (you deploy) | — | ✅ $30/mo compute |

> ⚡ **Groq free tier** (per organization, not per key):
> `gpt-oss-120b` → 30 RPM · 1,000 RPD · 8K TPM · 200K TPD
> `llama-3.1-8b` → 30 RPM · 14,400 RPD · 6K TPM · 500K TPD

---

## 🔀 Routers, Gateways & Aggregators

| Provider | Base URL | Auth | Free Tier |
| :--- | :--- | :--- | :--- |
| **OpenRouter** | `https://openrouter.ai/api/v1` | Bearer | ✅ `:free` models |
| **LiteLLM** | Self-hosted (`:4000`) | Configurable | N/A (OSS) |
| **Portkey** | `https://api.portkey.ai/v1` | `x-portkey-api-key` | 🎟️ Trial |
| **Helicone** | `https://oai.helicone.ai/v1` | `Helicone-Auth` | 🎟️ Trial |
| **AIML API** | `https://api.aimlapi.com/v1` | Bearer | ✅ Limited |
| **Vercel AI Gateway** | `https://api.vercel.ai/v1` | Bearer | 💳 $5 / 30 days |
| **Puter.js** | JS SDK (no backend) | — | ✅ Unlimited (user-pays) |

> 🏆 **OpenRouter**: 20 RPM on all accounts. 50 RPD free, **1,000 RPD after a one-time $10 credit purchase** — permanent. Best free-tier upgrade in this list.
> 🏆 **LiteLLM**: most flexible multi-provider gateway — load balancing, fallbacks, spend tracking.

---

## ☁️ Managed Cloud AI Platforms

| Platform | Base URL | Auth |
| :--- | :--- | :--- |
| **AWS Bedrock** | `https://bedrock-runtime.{region}.amazonaws.com` | AWS SigV4 |
| **Azure OpenAI** | `https://{resource}.openai.azure.com/openai/deployments/{id}` | `api-key` / Entra ID |
| **Google Vertex AI** | `https://{region}-aiplatform.googleapis.com/v1` | OAuth 2.0 / ADC |
| **AWS SageMaker** | Per-endpoint | AWS SigV4 |
| **IBM watsonx** | `https://{region}.ml.cloud.ibm.com/ml/v1` | IBM Cloud IAM |

> 🏢 Enterprise picks: compliance, private networking, VPC isolation, MLOps. No meaningful free tier for most models.

---

## 🌏 Chinese / Regional Providers

| Provider | Base URL | Format | Free Tier |
| :--- | :--- | :--- | :--- |
| **Qwen / DashScope** | `https://dashscope-intl.aliyuncs.com/compatible-mode/v1` | A + B | ✅ 1M tokens / 90 days |
| **Zhipu / GLM** | `https://open.bigmodel.cn/api/paas/v4` | A | 🎟️ Trial |
| **Moonshot (Kimi)** | `https://api.moonshot.cn/v1` | A | 🎟️ Trial |
| **Yi / 01.AI** | `https://api.lingyiwanwu.com/v1` | A | 🎟️ Trial |
| **MiniMax** | `https://api.minimax.chat/v1` | A | 🎟️ Trial |
| **iFlow** | `https://apis.iflow.cn/v1` | A | ✅ Unlimited, 1 concurrent |
| **LongCat** | `https://api.longcat.chat/openai/v1` | A + B | ✅ 500K–50M tok/day |

> 🌍 **Qwen regional endpoints** — pick the closest:
> International: `https://dashscope-intl.aliyuncs.com/compatible-mode/v1`
> China: `https://dashscope.aliyuncs.com/compatible-mode/v1`
> US (Virginia): `https://dashscope-us.aliyuncs.com/compatible-mode/v1`

> ⚠️ Qwen OAuth free tier **discontinued 2026-04-15** — DashScope API key now required.
> ⚠️ LongCat quotas reset at **Beijing midnight**, no rollover.
> ⚠️ iFlow = 1 concurrent request per user; overflow returns `429`.

---

## 🎁 Free-Tier Focused Providers

The best *"no credit card needed"* options, ranked by practical usefulness:

| Provider | Base URL | Free Tier |
| :--- | :--- | :--- |
| **Google Gemini** | `generativelanguage.googleapis.com` | Variable — see AI Studio console |
| **Groq** | `api.groq.com/openai/v1` | 30 RPM · 1K RPD · 200K TPD |
| **OpenRouter** | `openrouter.ai/api/v1` | 20 RPM · 50→1,000 RPD (`:free`) |
| **Mistral** | `api.mistral.ai/v1` | Free mode (see admin panel) |
| **Cloudflare Workers AI** | `api.cloudflare.com/client/v4/...` | 10,000 Neurons/day |
| **NVIDIA NIM** | `integrate.api.nvidia.com/v1` | ~40 RPM · 138 models |
| **Cohere** | `api.cohere.com/v1` | 20 RPM · 1,000 calls/month |
| **GitHub Models** | `models.inference.ai.azure.com` | 15 RPM · 150 RPD |
| **iFlow** | `apis.iflow.cn/v1` | 1 concurrent · unlimited |
| **LongCat** | `api.longcat.chat/openai/v1` | 500K–50M tokens/day |
| **Opencode Zen** | `opencode.ai/zen/v1` | 2+ models at $0 / 1M tokens |
| **Pollinations** | `text.pollinations.ai` | Unlimited · **no auth** |
| **Puter.js** | JS SDK | Unlimited (user-pays) |
| **Ollama / LM Studio** | `localhost` | Unlimited (local) |

> ### ⚠️ Important changes (2026)
> - **Cerebras** — no longer strictly "no credit card"; $5 credit requires a verified payment method.
> - **SambaNova** — free tier tightened in Sep 2026; may require a payment method for first requests.
> - **Mistral** — free-mode limits are unpublished; check your admin panel.
> - **Google Gemini** — per-model limits no longer published publicly; check AI Studio.

---

## 🧪 Media, Infrastructure & Tool APIs

### 🎨 Image & Video Generation

| Provider | Base URL | Auth | Notes |
| :--- | :--- | :--- | :--- |
| **OpenAI DALL·E** | `https://api.openai.com/v1/images/` | Bearer | DALL·E 3 |
| **Stability AI** | `https://api.stability.ai/v2beta` | Bearer | SD 3.5, SDXL, Cascade |
| **Black Forest Labs (FLUX)** | `https://api.bfl.ml/v1` | `x-key` | FLUX.1 Pro / Dev / Schnell |
| **Ideogram** | `https://api.ideogram.ai` | `Api-Key` | 🏆 Best text rendering |
| **Recraft** | `https://external.api.recraft.ai/v1` | Bearer | Vector + raster |
| **Leonardo AI** | `https://cloud.leonardo.ai/api/rest/v1` | Bearer | Game-art presets |
| **Google Imagen** | Vertex AI endpoint | OAuth | Imagen 3 / 4 |
| **Pollinations** | `https://image.pollinations.ai/prompt/{prompt}` | None | Unlimited free |
| **Runway** | `https://api.dev.runwayml.com/v1` | Bearer | Gen-4.5, motion brushes |
| **Luma AI (Dream Machine)** | `https://api.lumalabs.ai/dream-machine/v1` | Bearer | Ray3 engine, 4K HDR |
| **Kling AI** | `https://api.klingai.com` | Bearer | Up to 2 min, 1080p |
| **OpenAI Sora** | `https://api.openai.com/v1/video` | Bearer | Cinematic physics |
| **HeyGen** | `https://api.heygen.com/v2` | `X-Api-Key` | Dubbing, lip-sync |
| **D-ID** | `https://api.d-id.com` | Basic auth | Talking heads |
| **Google Veo** | Vertex AI endpoint | OAuth | Native audio |
| **Twelve Labs** | `https://api.twelvelabs.io/v1.2` | `x-api-key` | 👀 Video *understanding* |

### 🔊 Audio & Speech (TTS / STT)

| Provider | Base URL | Auth | Notes |
| :--- | :--- | :--- | :--- |
| **ElevenLabs** | `https://api.elevenlabs.io/v1` | `xi-api-key` | 3,000+ voices, 70+ langs |
| **OpenAI TTS** | `https://api.openai.com/v1/audio/speech` | Bearer | `gpt-4o-mini-tts` |
| **Cartesia (Sonic)** | `https://api.cartesia.ai` | `X-API-Key` | ⚡ **<150 ms** latency |
| **Play.ht** | `https://api.play.ht/api/v2` | `X-User-ID` + Bearer | 900+ voices |
| **Resemble AI** | `https://api.resemble.ai/v2` | Bearer | Cloning + deepfake detection |
| **Deepgram** | `https://api.deepgram.com/v1` | Token | Nova-2, sub-250 ms streaming |
| **AssemblyAI** | `https://api.assemblyai.com/v2` | Authorization | Universal-1, diarization |
| **OpenAI Whisper** | `https://api.openai.com/v1/audio/transcriptions` | Bearer | 50+ languages |
| **Google Cloud STT** | `https://speech.googleapis.com/v1` | OAuth / API key | 60 min/mo free |
| **Local (Piper / Coqui / Bark / Vosk)** | Self-hosted | None | Free, offline |

### 🎵 Music Generation

| Provider | Access | Notes |
| :--- | :--- | :--- |
| **Suno** | Web only | 5 songs/day free |
| **Udio** | Web only | Limited free credits |
| **Mubert** | `https://api.mubert.com/v2` | Real-time generative BG music |
| **MusicGen (Replicate / local)** | `api.replicate.com/v1` | Meta's open model |

### 🔍 Search, Vector Datasets & Extensions

| Provider | Base URL | Auth | Notes |
| :--- | :--- | :--- | :--- |
| **Perplexity Sonar** | `https://api.perplexity.ai` | Bearer | LLM answers + citations |
| **Exa AI** | `https://api.exa.ai` | `x-api-key` | 🧠 Neural agentic search (94.9% SimpleQA) |
| **Tavily** | `https://api.tavily.com` | `api_key` in JSON body | 🏆 RAG-optimized, SOC 2 |
| **Brave Search** | `https://api.search.brave.com/res/v1` | `X-Subscription-Token` | Independent, privacy-first |
| **SerpAPI** | `https://serpapi.com/search` | `api_key` (query) | SERP scraping |
| **You.com** | `https://api.you.com` | Bearer | Deep Search, MCP |
| **Serper** | `https://google.serper.dev` | `X-API-KEY` | Fast/cheap Google SERP |
| **SearXNG** | Self-hosted | None | ♾️ Unlimited, no tracking |

### 🌐 Translation

| Provider | Base URL | Auth | Free Tier |
| :--- | :--- | :--- | :--- |
| **DeepL** | `https://api-free.deepl.com/v2` | `DeepL-Auth-Key` | 500K chars/mo |
| **Google Translate** | `https://translation.googleapis.com/v3` | OAuth | 130+ langs |
| **Microsoft Translator** | `https://api.cognitive.microsofttranslator.com` | `Ocp-Apim-Subscription-Key` | 100+ langs |
| **LibreTranslate** | Self-hosted / `libretranslate.com` | None | ♾️ Open source |
| **MyMemory** | `https://api.mymemory.translated.net` | None | 5,000 words/day |
| **Lingva** | `https://lingva.ml/api/v1` | None | No tracking |

### 🧲 Embeddings

| Provider | Base URL | Auth | Free Tier |
| :--- | :--- | :--- | :--- |
| **OpenAI** | `https://api.openai.com/v1/embeddings` | Bearer | ❌ |
| **Voyage AI** | `https://api.voyageai.com/v1` | Bearer | **50M tokens** |
| **Jina AI** | `https://api.jina.ai/v1` | Bearer | **1M tokens** + reranking |
| **Cohere Embed** | `https://api.cohere.com/v1/embed` | Bearer | Trial |
| **Nomic** | `https://api-atlas.nomic.ai/v1` | Bearer | Free tier |
| **Ollama** | `http://localhost:11434/v1` | None | ♾️ Unlimited local |

### 🗄️ Vector Databases

| Provider | Type | Notes |
| :--- | :--- | :--- |
| **Pinecone** | Managed cloud | Serverless, billions of vectors |
| **Weaviate** | Cloud / self-host | Hybrid search (vector + keyword) |
| **Qdrant** | Cloud / self-host | High QPS at 99% recall |
| **Chroma** | Local / cloud | Best for RAG prototypes |
| **Milvus / Zilliz** | Self-host / cloud | Billion-scale, enterprise SLAs |
| **pgvector** | Postgres extension | Vectors + relational data together |
| **LanceDB** | Serverless | Lance columnar format, zero-copy |

### 💻 Local / Self-Hosted Inference

| Tool | Local URL | Notes |
| :--- | :--- | :--- |
| **Ollama** | `http://localhost:11434/v1` | One command per model |
| **LM Studio** | `http://localhost:1234/v1` | GUI + server, GGUF support |
| **llama.cpp** | `http://localhost:8080/v1` | C/C++, CPU-optimized |
| **vLLM** | `http://localhost:8000/v1` | High throughput, PagedAttention |
| **LocalAI** | `http://localhost:8080/v1` | OpenAI-compatible, self-hosted |
| **MLX** | Apple Silicon | Apple array/ML framework |
| **ExecuTorch** | Mobile | Meta's on-device framework (50 KB) |

> ♾️ All local tools are **unlimited, no auth, no cost**.

### 🖥️ GPU Cloud Providers

| Provider | Notes |
| :--- | :--- |
| **RunPod** | On-demand + serverless A100/H100 |
| **Lambda Cloud** | H100/A100, zero egress, InfiniBand |
| **CoreWeave** | Kubernetes-native hyperscale |
| **Vast.ai** | 🏆 Marketplace bidding — cheapest |
| **Nebius** | Blackwell Ultra, EU data centers |
| **Modal** | Serverless GPU, **$30/mo free** |
| **Crusoe Cloud** | Clean-energy powered |
| **Predibase** | LoRAX multi-adapter serving |

### 🔌 MCP (Model Context Protocol)

- **Spec:** `https://modelcontextprotocol.io` · Governance: Linux Foundation AAIF (originally Anthropic)
- **Install:** `npm install @modelcontextprotocol/sdk` (TS) · `pip install mcp` (Python)
- **Notable servers:** [Official servers](https://github.com/modelcontextprotocol/servers) · [Awesome MCP Servers](https://github.com/punkpeye/awesome-mcp-servers) (97k ★) · Playwright MCP (39k ★) · ActionKit by Paragon (130+ SaaS)
- **What it does:** MCP lets any LLM call external tools, read from data sources, and execute actions in software.

---

## 💡 Practical Notes & Gotchas

- **Free Tier Volatilities:** Providers update tiers frequently. Infrastructure like Cerebras and SambaNova require adding a verified card to initialize free/trial credits. Google and Mistral manage exact current free quotas strictly inside their UI project consoles rather than public static docs. **Always verify against the provider's console before building.**

- **Rate Limit Enforcement:**
  - Groq limits apply per *Organization*, not per individual API key. Generating extra keys will not bypass limits.
  - Cloudflare Worker AI Neurons reset daily at 00:00 UTC. Heavy visual tasks consume drastically higher neuron weights (~10,000 neurons per request).
  - NVIDIA NIM limits are per API key (sometimes per account, varies).
  - LongCat quotas reset at Beijing midnight and do not roll over.
  - iFlow allows only 1 concurrent request per user; overflow returns `429`.

- **HTTP 402 vs 429:** A `429` indicates rate limit saturation (safe to retry with backoff). A `402` implies Payment Required (OpenRouter passes a 402 if your total credit balance hits zero, even on completely free variants).

- **Rate-Limit Headers:** Most OpenAI-compatible providers return:
  ```
  x-ratelimit-limit-requests      x-ratelimit-remaining-requests
  x-ratelimit-limit-tokens        x-ratelimit-remaining-tokens
  retry-after                     (seconds, after a 429)
  ```
  Groq's "requests" header means **RPD**; "tokens" means **TPM**.

- **Auth Quirks:**
  - **Anthropic** — `x-api-key` + `anthropic-version` (not Bearer)
  - **Azure OpenAI** — `api-key` header or Entra ID token (not Bearer)
  - **fal.ai** — `Authorization: Key <FAL_KEY>` (not Bearer)
  - **AWS Bedrock** — SigV4 signing, not a simple header
  - **Google** — API key as query param OR `x-goog-api-key` header

- **Context Window Changes (2026):**
  - DeepSeek V4.1 Flash / V4 Pro → **1M tokens**
  - Gemini 2.5 Pro → **2M tokens**
  - GPT-5 → **400K** (1M on select variants)
  - Llama 4 → **1M** on Fireworks, narrower elsewhere
  - Qwen3.8-max → **1M tokens**
  - Claude → **200K tokens**

- **Building for Multi-Provider:**
  - Use an OpenAI-compatible client (`openai-python`, `openai-node`, LiteLLM) and swap `base_url` + `api_key`. Covers ~80% of providers.
  - Anthropic → native SDK, or route through LiteLLM / OpenRouter.
  - Gemini → `google-genai` SDK, or the `/v1beta/openai/` compatibility endpoint.
  - Bedrock / Vertex → native SDKs (`boto3`, `google-cloud-aiplatform`) or LiteLLM's abstraction.

- **Free-Tier Strategy for Production:** 🚫 Don't run production traffic on free tiers — limits change without notice. Use them for prototyping, fallbacks, and low-priority batch jobs. For genuinely zero-cost production: self-host open-weight models (Ollama, vLLM) or use Puter.js (user-pays) for web apps. **Combine providers:** Groq for speed, Gemini for long context, Groq/Cerebras for high-volume simple tasks.

- **Universal Self-Hosting:** For local sandbox tasks or air-gapped workloads, deploy local engines running OpenAI-compatible proxies:
  - **Ollama:** `http://localhost:11434/v1`
  - **LM Studio:** `http://localhost:1234/v1`
  - **vLLM:** `http://localhost:8000/v1`
  - **LocalAI:** `http://localhost:8080/v1`

---

## 🤝 Contributing

Found an updated base URL, altered header rule, or missing provider? Contributions are welcome! Please open an Issue or submit a Pull Request.

**When contributing:**
1. Add or edit the entry in the relevant section **and** the [Quick Reference Matrix](#️-quick-reference-matrix)
2. Include a link to the official docs as your source
3. Describe what changed and when you verified it

**Please don't add providers without a public, documented API.**

---

## 📄 License

MIT

> **Disclaimer:** This is a community reference, not legal or financial advice. Provider terms, pricing, and rate limits change frequently. Verify everything against official documentation before shipping to production.
