================================================================================
                    COMPREHENSIVE AI PROVIDERS REFERENCE
       Base URLs • API Formats • Auth Methods • Models • Free Tiers
================================================================================
Compiled from: awesome-ai, free-ai-apis, AI Providers gist, provider docs
Last updated: November 2026

TABLE OF CONTENTS
  1.  LLM Foundation Labs
  2.  Open-Source Model Hosting & Inference
  3.  LLM Routers, Gateways & Aggregators
  4.  Managed Cloud AI Platforms
  5.  Chinese / Regional LLM Providers
  6.  Free-Tier Focused Providers (Developer-First)
  7.  Image Generation APIs
  8.  Video Generation APIs
  9.  Audio & Speech APIs
  10. Search APIs
  11. Translation APIs
  12. Embedding APIs
  13. Vector Databases
  14. Local / Self-Hosted Inference
  15. GPU Cloud Providers
  16. MCP (Model Context Protocol)
  17. Universal API Format Patterns (Cheat Sheet)
  18. Quick Reference Matrix
  19. Practical Notes & Gotchas

================================================================================
1. LLM FOUNDATION LABS
================================================================================

--------------------------------------------------------------------------------
1.1 OpenAI
--------------------------------------------------------------------------------
Website:        https://platform.openai.com
Docs:           https://platform.openai.com/docs
API Base URL:   https://api.openai.com/v1
Auth:           Bearer token  (Header: Authorization: Bearer sk-...)
API Format:     Custom REST (de-facto industry standard)
Key Models:     GPT-5 (400K context, released Aug 2025) [reference:0],
                GPT-4o, GPT-4o-mini, o1, o3, o4-mini,
                DALL-E 3, Whisper, Embeddings (text-embedding-3)
Free Tier:      No API free tier (usage-based billing)
Notes:          Originator of the OpenAI API spec — most other providers mirror it.
                Realtime API available over WebSocket.
                GPT-5 pricing: $1.25/$10.00 per 1M tokens (in/out) [reference:1].

--------------------------------------------------------------------------------
1.2 Anthropic (Claude)
--------------------------------------------------------------------------------
Website:        https://console.anthropic.com
Docs:           https://docs.anthropic.com
API Base URL:   https://api.anthropic.com
Auth:           x-api-key header + anthropic-version header
API Format:     Custom REST (Messages API: POST /v1/messages)
Key Models:     Claude 4 family (Opus 4, Sonnet 4, Haiku 4),
                Claude 3.5 Sonnet, Claude 3.5 Haiku [reference:2]
Context:        200k tokens
Free Tier:      No API free tier (web app has free tier)
Notes:          Strong at coding, long-form writing, agentic tool use.
                Extended Thinking mode available (native thinking blocks).
                Base URL is https://api.anthropic.com (no /v1 in root for some SDKs;
                endpoint is /v1/messages) [reference:3].

--------------------------------------------------------------------------------
1.3 Google Gemini (AI Studio)
--------------------------------------------------------------------------------
Website:        https://aistudio.google.com
Docs:           https://ai.google.dev/gemini-api/docs
API Base URL:   https://generativelanguage.googleapis.com/v1beta
Auth:           API key (query param ?key=... OR header x-goog-api-key)
API Format:     Custom REST (also OpenAI-compatible endpoint at
                https://generativelanguage.googleapis.com/v1beta/openai/) [reference:4]
Key Models:     Gemini 3.8 Flash (free tier) [reference:5], Gemini 3.6 Flash,
                Gemini 2.5 Pro, Gemini 2.5 Flash, Gemma 4 family,
                Gemini 4 Argon (NOT free tier) [reference:6]
Context:        Up to 2,000,000 tokens (2.5 Pro)
Free Tier:      YES — no credit card needed. Google no longer publishes per-model
                RPM/RPD on the public rate-limits page; exact limits are shown
                inside AI Studio rate-limit console per project [reference:7].
                Reported Flash-class: ~10–15 RPM, a few hundred to 1,500 RPD [reference:8].
Notes:          Best free tier for high-volume work. Multimodal (text/image/video/audio).
                Rate limits applied per project, not per API key [reference:9].
                Grounding with Google Search: 1,500 RPD free per project [reference:10].

--------------------------------------------------------------------------------
1.4 Mistral AI
--------------------------------------------------------------------------------
Website:        https://console.mistral.ai
Docs:           https://docs.mistral.ai
API Base URL:   https://api.mistral.ai/v1
Auth:           Bearer token
API Format:     Custom REST (also OpenAI-compatible)
Key Models:     Mistral Large 3, Small 3.1, Ministral 8B [reference:11],
                Mixtral, Codestral, Pixtral
Free Tier:      YES — "Free mode" (default). Limits intended for evaluation and
                prototyping; exact numbers shown in your admin panel, not published
                publicly [reference:12]. Estimated: ~10–15M tokens/month,
                ~5–10 RPM [reference:13].
Notes:          European lab; open weights under Apache 2.0.
                Codestral is coding-specialized (32k context).

--------------------------------------------------------------------------------
1.5 DeepSeek
--------------------------------------------------------------------------------
Website:        https://platform.deepseek.com
Docs:           https://api-docs.deepseek.com
API Base URL:   https://api.deepseek.com  (OpenAI format)
                https://api.deepseek.com/anthropic  (Anthropic format) [reference:14]
Auth:           Bearer token
API Format:     OpenAI-compatible AND Anthropic-compatible
Key Models:     deepseek-flash (DeepSeek-V4.1-Flash-1017),
                deepseek-v4-pro (DeepSeek-V4-Pro-0813) [reference:15]
Context:        1M tokens [reference:16]
Free Tier:      No permanent free tier (low-cost paid)
Pricing (per 1M tokens, off-peak/peak) [reference:17]:
                Flash:  Input (cache hit) $0.003/$0.006, (miss) $0.15/$0.30
                        Output $0.60/$1.20
                Pro:    Input (cache hit) $0.022/$0.044, (miss) $0.66/$1.32
                        Output $1.98/$3.96
Notes:          Off-peak is half price. Peak hours: 01:00–04:00 and 06:00–10:00 UTC,
                Mon–Fri (excluding Chinese holidays) [reference:18].
                Supports JSON output, tool calls, thinking mode, FIM completion.

--------------------------------------------------------------------------------
1.6 Cohere
--------------------------------------------------------------------------------
Website:        https://dashboard.cohere.com
Docs:           https://docs.cohere.com
API Base URL:   https://api.cohere.com/v1  (also OpenAI-compat at /compatibility/v1) [reference:19]
Auth:           Bearer token
API Format:     Custom REST + OpenAI-compatible layer
Key Models:     Command A+, Command R+, Command R, Embed v3/v4, Rerank
Free Tier:      YES — trial API keys. 1,000 API calls/month total cap,
                20 chat requests/min for most models [reference:20].
                Rerank: 10 req/min trial [reference:21].
Notes:          Enterprise RAG-optimized. Embed + Rerank are best-in-class.
                Trial keys are for non-commercial use only [reference:22].

--------------------------------------------------------------------------------
1.7 AI21 Labs
--------------------------------------------------------------------------------
Website:        https://studio.ai21.com
Docs:           https://docs.ai21.com
API Base URL:   https://api.ai21.com/studio/v1
Auth:           Bearer token
API Format:     Custom REST
Key Models:     Jamba (hybrid SSM-Transformer), Jurassic-2, Maestro
Free Tier:      Trial credits
Notes:          Strong multilingual, enterprise NLP focus.

--------------------------------------------------------------------------------
1.8 xAI (Grok)
--------------------------------------------------------------------------------
Website:        https://console.x.ai
Docs:           https://docs.x.ai
API Base URL:   https://api.x.ai/v1
Auth:           Bearer token
API Format:     OpenAI-compatible
Key Models:     Grok-2, Grok-2 Mini, Grok-3
Free Tier:      Limited trial credits
Notes:          Real-time X platform data indexing. Image + video gen in ecosystem.

--------------------------------------------------------------------------------
1.9 Inflection AI
--------------------------------------------------------------------------------
Website:        https://inflection.ai
API Base URL:   Enterprise API (contact sales)
Key Models:     Pi (empathetic conversational)
Notes:          Focused on helpful, emotionally aware interactions.

--------------------------------------------------------------------------------
1.10 Reka AI
--------------------------------------------------------------------------------
Website:        https://www.reka.ai
Docs:           https://docs.reka.ai
API Base URL:   https://api.reka.ai
Auth:           Bearer token
Key Models:     Reka Core, Reka Flash, Reka Edge (multimodal)
Notes:          Text + image + video understanding.

================================================================================
2. OPEN-SOURCE MODEL HOSTING & INFERENCE
================================================================================

--------------------------------------------------------------------------------
2.1 Together AI
--------------------------------------------------------------------------------
Website:        https://www.together.ai
Docs:           https://docs.together.ai
API Base URL:   https://api.together.xyz/v1
Auth:           Bearer token
API Format:     OpenAI-compatible
Models:         200+ open models (Llama 3/4, Qwen, DeepSeek, Mixtral, FLUX, SD)
Free Tier:      $5 free credits on signup
Notes:          Fast inference, fine-tuning, LoRA adapter support.
                Hosts Llama 4 Maverick and Scout [reference:23].

--------------------------------------------------------------------------------
2.2 Fireworks AI
--------------------------------------------------------------------------------
Website:        https://fireworks.ai
Docs:           https://docs.fireworks.ai
API Base URL:   https://api.fireworks.ai/inference/v1
Auth:           Bearer token
API Format:     OpenAI-compatible
Models:         DeepSeek, Llama (including Llama 4 with full 1M context) [reference:24],
                Qwen, Mixtral, custom fine-tunes
Free Tier:      $1 free credit on signup
Notes:          Low-latency, optimized for open-weight models.

--------------------------------------------------------------------------------
2.3 Groq
--------------------------------------------------------------------------------
Website:        https://console.groq.com
Docs:           https://console.groq.com/docs
API Base URL:   https://api.groq.com/openai/v1
Auth:           Bearer token
API Format:     OpenAI-compatible
Key Models:     openai/gpt-oss-120b, qwen/qwen3.8-27b, llama-3.1-8b,
                llama-3.3-70b, Llama 4 Scout, Kimi K2, Whisper Large v3
Free Tier:      YES — no credit card. Sample limits (per organization) [reference:25]:
                - gpt-oss-120b: 30 RPM, 1,000 RPD, 8K TPM, 200K TPD
                - qwen3.8-27b: 30 RPM, 1,000 RPD, 8K TPM, 200K TPD
                - llama-3.1-8b: 30 RPM, 14.4K RPD, 6K TPM, 500K TPD
Notes:          LPU hardware → extremely low latency.
                Limits apply per organization, not per user/key [reference:26].
                Headers: x-ratelimit-limit-requests (RPD), etc.
                After free tier: GPT OSS 120B $0.15/$0.60 per 1M [reference:27].

--------------------------------------------------------------------------------
2.4 Cerebras
--------------------------------------------------------------------------------
Website:        https://cloud.cerebras.ai
Docs:           https://inference-docs.cerebras.ai
API Base URL:   https://api.cerebras.ai/v1
Auth:           Bearer token
API Format:     OpenAI-compatible
Key Models:     gpt-oss-120b, qwen-3.8-27b, llama3.3-70b, llama3.1-8b
Free Tier:      ⚠️ IMPORTANT UPDATE: The free tier now requires adding a verified
                payment method to receive $5 in credits (expire after 30 days).
                Without a card, API access remains inactive. [reference:28][reference:29]
                Free Trial limits per model: 5 RPM, 30K uncached TPM,
                90K total TPM, 1M TPH, 1M TPD [reference:30].
Notes:          Wafer-scale chip = fastest token throughput available.
                Some community reports cite 30 RPM / 14.4K RPD for legacy free
                tier, but official docs now reflect the $5 credit trial model [reference:31].
                Developer tier (after first purchase): 1,000 RPM on gpt-oss-120b [reference:32].

--------------------------------------------------------------------------------
2.5 SambaNova
--------------------------------------------------------------------------------
Website:        https://cloud.sambanova.ai
Docs:           https://docs.sambanova.ai
API Base URL:   https://api.sambanova.ai/v1
Auth:           Bearer token
API Format:     OpenAI-compatible
Free Tier:      Free Tier (no payment method): ~20 RPM, 20 requests/day,
                200K tokens/day per model [reference:33].
                Developer Tier (card linked): 20M tokens/day across all models [reference:34].
Notes:          ⚠️ Free plan tightened in Sep 2026; some sources say you must add
                a payment method and purchase credits to run first requests [reference:35].
                Verify current terms before building.

--------------------------------------------------------------------------------
2.6 Replicate
--------------------------------------------------------------------------------
Website:        https://replicate.com
Docs:           https://replicate.com/docs
API Base URL:   https://api.replicate.com/v1
Auth:           Bearer token
API Format:     Custom REST (predictions endpoint)
Models:         Any open model (Flux, SD, Llama, Wan, CogVideo, MusicGen, etc.)
Free Tier:      $5 free credits (no credit card)
Notes:          Run + host any model. Pay-per-second. Async predictions.

--------------------------------------------------------------------------------
2.7 Modal
--------------------------------------------------------------------------------
Website:        https://modal.com
API Base URL:   Serverless Python (no fixed base URL — you deploy functions)
Free Tier:      $30/month free compute
Notes:          Serverless GPU, pay-per-use, zero idle cost.

--------------------------------------------------------------------------------
2.8 Baseten
--------------------------------------------------------------------------------
Website:        https://www.baseten.co
API Base URL:   Custom per-deployment
Notes:          Enterprise model serving with infra control.

--------------------------------------------------------------------------------
2.9 DeepInfra
--------------------------------------------------------------------------------
Website:        https://deepinfra.com
API Base URL:   https://api.deepinfra.com/v1/openai
Auth:           Bearer token
API Format:     OpenAI-compatible
Models:         Llama (including Llama 4 Scout/Maverick at low cost) [reference:36],
                Qwen, Mixtral, FLUX, SD
Free Tier:      Free credits on signup
Notes:          Cost-effective serverless inference.
                Llama 4 Scout: $0.08/$0.30 per 1M; Maverick: $0.17/$0.60 [reference:37].

--------------------------------------------------------------------------------
2.10 Lepton AI
--------------------------------------------------------------------------------
Website:        https://www.lepton.ai
API Base URL:   Custom per-deployment
Notes:          Pythonic framework, cloud-native inference.

--------------------------------------------------------------------------------
2.11 fal.ai
--------------------------------------------------------------------------------
Website:        https://fal.ai
Docs:           https://docs.fal.ai
API Base URL:   https://fal.run  (sync) / https://queue.fal.run  (async)
Auth:           Header: Authorization: Key <FAL_KEY>
API Format:     Custom REST (queue-based)
Models:         600+ generative media models (FLUX, SD, video, audio)
Notes:          Optimized for generative media, competitive pricing.

--------------------------------------------------------------------------------
2.12 Novita AI
--------------------------------------------------------------------------------
Website:        https://novita.ai
API Base URL:   https://api.novita.ai/v3/openai
Auth:           Bearer token
API Format:     OpenAI-compatible
Models:         Text, image, audio models; Llama 4 Maverick at $0.27/$0.85 [reference:38]
Free Tier:      $0.50 free credits
Notes:          Affordable all-purpose API.

--------------------------------------------------------------------------------
2.13 Hyperbolic
--------------------------------------------------------------------------------
Website:        https://hyperbolic.xyz
API Base URL:   https://api.hyperbolic.xyz/v1
Auth:           Bearer token
API Format:     OpenAI-compatible
Free Tier:      Yes (limited)
Notes:          Open-source model hosting.

================================================================================
3. LLM ROUTERS, GATEWAYS & AGGREGATORS
================================================================================

--------------------------------------------------------------------------------
3.1 OpenRouter
--------------------------------------------------------------------------------
Website:        https://openrouter.ai
Docs:           https://openrouter.ai/docs
API Base URL:   https://openrouter.ai/api/v1
Auth:           Bearer token
API Format:     OpenAI-compatible
Models:         200+ models from OpenAI, Anthropic, Google, Meta, DeepSeek, etc.
Free Tier:      YES — :free model variants. Current limits (as of Oct 2026) [reference:39]:
                - 20 RPM (all accounts)
                - 50 RPD if lifetime credit purchases < $10
                - 1,000 RPD after purchasing ≥ $10 credits (one-time)
                17+ free models available (varies): Cohere North Mini Code,
                Gemma 4, Nemotron 3 variants, MiniMax M3.1 Flash, etc. [reference:40]
Notes:          Single key for all providers. Automatic fallback + price comparison.
                Negative balance returns 402 even on free models [reference:41].
                Key info: GET https://openrouter.ai/api/v1/key.

--------------------------------------------------------------------------------
3.2 LiteLLM (Open-Source Proxy)
--------------------------------------------------------------------------------
Website:        https://litellm.ai
Docs:           https://docs.litellm.ai
API Base URL:   Self-hosted (default: http://localhost:4000)
Auth:           Configurable (master key)
API Format:     OpenAI-compatible proxy
Models:         100+ providers (Bedrock, Azure, Vertex, Anthropic, Cohere, Groq,
                Mistral, DeepInfra, Perplexity, Ollama, vLLM, etc.)
Notes:          Python SDK + proxy server. Load balancing, fallbacks, spend tracking.
                Most flexible gateway for multi-provider apps.

--------------------------------------------------------------------------------
3.3 Martian
--------------------------------------------------------------------------------
Website:        https://withmartian.com
API Format:     OpenAI-compatible
Notes:          Auto-selects best model per request (Model Mapping).

--------------------------------------------------------------------------------
3.4 Portkey
--------------------------------------------------------------------------------
Website:        https://portkey.ai
API Base URL:   https://api.portkey.ai/v1
Auth:           x-portkey-api-key header
API Format:     OpenAI-compatible
Notes:          Enterprise gateway: load balancing, caching, fallbacks, observability.

--------------------------------------------------------------------------------
3.5 Helicone
--------------------------------------------------------------------------------
Website:        https://helicone.ai
API Base URL:   https://oai.helicone.ai/v1  (proxy)
Auth:           Helicone-Auth header
API Format:     OpenAI-compatible proxy
Notes:          Rust-based gateway, request logging, cost tracking.

--------------------------------------------------------------------------------
3.6 AIML API
--------------------------------------------------------------------------------
Website:        https://aimlapi.com
Docs:           https://docs.aimlapi.com
API Base URL:   https://api.aimlapi.com/v1
Auth:           Bearer token
API Format:     OpenAI-compatible
Models:         200+ models
Free Tier:      Unverified: 10 req/hour (Gemma models only)
                Verified: 10 req/hour FREE models, 10 req/day cheap paid,
                50k credits/day, cost ≤ $0.025/request
Notes:          Unified access to many providers.

--------------------------------------------------------------------------------
3.7 Vercel AI Gateway
--------------------------------------------------------------------------------
Website:        https://vercel.com/ai-gateway
Docs:           https://vercel.com/docs/ai-gateway
API Base URL:   https://api.vercel.ai/v1
Auth:           Bearer token
API Format:     OpenAI-compatible
Free Tier:      $5 credit every 30 days
Notes:          Built into Vercel AI SDK.

--------------------------------------------------------------------------------
3.8 Puter.js (Serverless Frontend)
--------------------------------------------------------------------------------
Website:        https://developer.puter.com
Docs:           https://docs.puter.com
API Format:     JavaScript SDK (no backend, no API key)
Models:         400+ models (text, image, TTS)
Free Tier:      Unlimited via "User-Pays" architecture (users authenticate with own Puter account)
Notes:          Best for web apps wanting zero infra cost. You pay $0 regardless of scale.

================================================================================
4. MANAGED CLOUD AI PLATFORMS
================================================================================

--------------------------------------------------------------------------------
4.1 AWS Bedrock
--------------------------------------------------------------------------------
Website:        https://aws.amazon.com/bedrock
Docs:           https://docs.aws.amazon.com/bedrock
API Base URL:   https://bedrock-runtime.{region}.amazonaws.com
Auth:           AWS SigV4 (IAM credentials)
API Format:     Custom REST (Bedrock Runtime API) + Converse API
Models:         Anthropic Claude, Meta Llama, Cohere, Mistral, Amazon Titan, AI21
Notes:          AgentCore for agents. No free tier for most models.

--------------------------------------------------------------------------------
4.2 Azure AI Foundry / Azure OpenAI
--------------------------------------------------------------------------------
Website:        https://ai.azure.com
Docs:           https://learn.microsoft.com/azure/ai-services/openai
API Base URL:   https://{resource-name}.openai.azure.com/openai/deployments/{deployment-id}
Auth:           api-key header  OR  Azure AD (Entra ID) token
API Format:     OpenAI-compatible (with deployment-based URLs)
Models:         GPT-4o, GPT-4/5, o-series, Llama, Mistral, Cohere (11,000+ models)
Notes:          Enterprise compliance + private networking.

--------------------------------------------------------------------------------
4.3 Google Vertex AI
--------------------------------------------------------------------------------
Website:        https://cloud.google.com/vertex-ai
Docs:           https://cloud.google.com/vertex-ai/docs
API Base URL:   https://{region}-aiplatform.googleapis.com/v1
Auth:           OAuth 2.0 (service account) / ADC
API Format:     Custom REST (also OpenAI-compat endpoint)
Models:         Gemini family, Model Garden (3rd-party + OSS), Imagen, Veo
Notes:          Full MLOps platform. Enterprise-grade.

--------------------------------------------------------------------------------
4.4 AWS SageMaker
--------------------------------------------------------------------------------
Website:        https://aws.amazon.com/sagemaker
API Base URL:   Per-endpoint
Auth:           AWS SigV4
Notes:          Build/train/deploy full ML pipelines.

--------------------------------------------------------------------------------
4.5 Azure Machine Learning
--------------------------------------------------------------------------------
Website:        https://azure.microsoft.com/products/machine-learning
Notes:          AutoML, responsible AI dashboard, managed endpoints.

--------------------------------------------------------------------------------
4.6 Databricks
--------------------------------------------------------------------------------
Website:        https://www.databricks.com
Notes:          Managed MLflow, Unity Catalog, Mosaic AI.

--------------------------------------------------------------------------------
4.7 IBM watsonx
--------------------------------------------------------------------------------
Website:        https://www.ibm.com/watsonx
API Base URL:   https://{region}.ml.cloud.ibm.com/ml/v1
Auth:           IBM Cloud IAM token
Notes:          Foundation models + governance. watsonx.governance for compliance.

================================================================================
5. CHINESE / REGIONAL LLM PROVIDERS
================================================================================

--------------------------------------------------------------------------------
5.1 Qwen / Alibaba (DashScope / Model Studio)
--------------------------------------------------------------------------------
Website:        https://dashscope.console.aliyun.com
Docs:           https://help.aliyun.com/zh/dashscope
API Base URL:   International (default): https://dashscope-intl.aliyuncs.com/compatible-mode/v1
                China: https://dashscope.aliyuncs.com/compatible-mode/v1
                US (Virginia): https://dashscope-us.aliyuncs.com/compatible-mode/v1
                Singapore (workspace-specific): https://{WorkspaceId}.ap-southeast-1.maas.aliyuncs.com/compatible-mode/v1 [reference:42][reference:43]
Auth:           Bearer token (DASHSCOPE_API_KEY)
API Format:     OpenAI-compatible AND Anthropic-compatible [reference:44]
Key Models:     qwen3.8-max ($2/$6 per 1M), qwen3.7-plus ($0.40/$1.60),
                qwen3.8-flash ($0.15/$0.47), Qwen3.8-27B (open weights, Apache 2.0) [reference:45]
Context:        Up to 1M tokens (qwen3.8-max) [reference:46]
Free Tier:      1M free tokens per model for 90 days (proprietary models) [reference:47].
                Qwen OAuth free tier discontinued 2026-04-15; API key via DashScope required [reference:48].
Notes:          Alibaba reprices quarterly — verify console before committing volume [reference:49].
                Qwen3.8-27B fits one 80GB GPU at FP8 (self-host viable) [reference:50].

--------------------------------------------------------------------------------
5.2 Zhipu AI / GLM
--------------------------------------------------------------------------------
Website:        https://open.bigmodel.cn
API Base URL:   https://open.bigmodel.cn/api/paas/v4
Auth:           Bearer token
API Format:     OpenAI-compatible
Models:         GLM-4.5, GLM-4.7, GLM-5.3

--------------------------------------------------------------------------------
5.3 Moonshot AI (Kimi)
--------------------------------------------------------------------------------
Website:        https://platform.moonshot.cn
API Base URL:   https://api.moonshot.cn/v1
Auth:           Bearer token
API Format:     OpenAI-compatible
Models:         Kimi K2, Kimi K2 Thinking, Kimi K3

--------------------------------------------------------------------------------
5.4 Yi / 01.AI
--------------------------------------------------------------------------------
Website:        https://platform.lingyiwanwu.com
API Base URL:   https://api.lingyiwanwu.com/v1
Auth:           Bearer token
API Format:     OpenAI-compatible
Models:         Yi-Large, Yi-Lightning, Yi-Vision (bilingual CN-EN)

--------------------------------------------------------------------------------
5.5 MiniMax
--------------------------------------------------------------------------------
Website:        https://platform.minimaxi.com
API Base URL:   https://api.minimax.chat/v1
Auth:           Bearer token
API Format:     OpenAI-compatible
Models:         MiniMax M2.5/M3.1, Hailuo video
Free Tier:      MiniMax M3.1 Flash appears as a :free model on OpenRouter [reference:51].

--------------------------------------------------------------------------------
5.6 iFlow
--------------------------------------------------------------------------------
Website:        https://iflow.cn
Docs:           https://platform.iflow.cn/docs
API Base URL:   https://apis.iflow.cn/v1
Auth:           Bearer token
API Format:     OpenAI-compatible
Free Tier:      YES — completely free, 1 concurrent request/user (429 on overflow)
Models:         GLM-4.7, DeepSeek-V3.2, Qwen3-Coder-Plus, Kimi-K2, MiniMax-M2.5

--------------------------------------------------------------------------------
5.7 LongCat
--------------------------------------------------------------------------------
Website:        https://longcat.chat
Docs:           https://longcat.chat/platform/docs/APIDocs.html
API Base URL:   https://api.longcat.chat/openai/v1
Auth:           Bearer token
API Format:     OpenAI- AND Anthropic-compatible
Free Tier:      YES — 500k tokens/day (Flash models), 50M tokens/day (Flash-Lite)
                Can request upgrade to 5M tokens/day
Models:         LongCat-Flash-Chat, Flash-Thinking, Flash-Thinking-2601, Flash-Lite
Notes:          Public beta, no paid quotas yet.

--------------------------------------------------------------------------------
5.8 AIWave
--------------------------------------------------------------------------------
Notes:          Hosted OpenAI-compatible gateway for Chinese model routes.
                One USD balance, dated pricing, request-level usage records.

--------------------------------------------------------------------------------
5.9 Heabsy
--------------------------------------------------------------------------------
Notes:          OpenAI- AND Anthropic-compatible inference for open-weight models.
                EEA tier: dedicated GPUs, zero data retention.

--------------------------------------------------------------------------------
5.10 XiuRouter
--------------------------------------------------------------------------------
Notes:          One API for OpenAI, Anthropic, Gemini protocol routes.
                Scoped keys, per-request usage + cost records.

--------------------------------------------------------------------------------
5.11 RunAPI
--------------------------------------------------------------------------------
Notes:          OpenAI-compatible API platform for model APIs, media generation,
                and usage tracking.

================================================================================
6. FREE-TIER FOCUSED PROVIDERS (DEVELOPER-FIRST)
================================================================================

Quick comparison of the best "no credit card needed" options (as of Oct/Nov 2026):

Provider          Base URL                                      Free Tier (official)
----------------- --------------------------------------------- ------------------------------------------
Google Gemini     https://generativelanguage.googleapis.com     Variable, shown in AI Studio
Groq              https://api.groq.com/openai/v1                30 RPM, 1k RPD, 8k TPM, 200k TPD
OpenRouter        https://openrouter.ai/api/v1                  20 RPM, 50–1000 RPD (:free)
Mistral           https://api.mistral.ai/v1                     Free mode (admin panel)
Cloudflare AI     https://api.cloudflare.com/client/v4/...      10,000 Neurons/day
NVIDIA NIM        https://integrate.api.nvidia.com/v1           ~40 RPM, no token billing
Cohere            https://api.cohere.com/v1                     20 RPM, 1k calls/month
SambaNova         https://api.sambanova.ai/v1                   20 RPM, 20 RPD, 200k TPD
GitHub Models     https://models.inference.ai.azure.com         15 RPM, 150 RPD (low tier)
AIML API          https://api.aimlapi.com/v1                    10 req/hour (limited)
iFlow             https://apis.iflow.cn/v1                      1 concurrent, unlimited
LongCat           https://api.longcat.chat/openai/v1            500k–50M tokens/day
Opencode Zen      https://opencode.ai/zen/v1                    2+ free models ($0/1M tokens)
Pollinations      https://text.pollinations.ai                   Unlimited, no auth
Puter             (JS SDK)                                      Unlimited (user-pays)
Ollama            http://localhost:11434/v1                     Unlimited (local)
LM Studio         http://localhost:1234/v1                      Unlimited (local)

⚠️ IMPORTANT CHANGES:
- Cerebras is no longer strictly "no credit card" — requires card for $5 credit trial [reference:52].
- SambaNova free tier tightened in Sep 2026; may require payment method for first requests [reference:53].
- Mistral Free mode limits are not published; check admin panel [reference:54].
- Google Gemini no longer publishes per-model limits publicly; check AI Studio [reference:55].

--------------------------------------------------------------------------------
6.1 GitHub Models
--------------------------------------------------------------------------------
Website:        https://github.com/marketplace/models
Docs:           https://docs.github.com/en/github-models
API Base URL:   https://models.inference.ai.azure.com
                (also https://models.github.ai/inference for some SDKs) [reference:56]
Auth:           GitHub PAT (Bearer)
API Format:     OpenAI-compatible
Models:         GPT-4o, GPT-4.1, GPT-5-mini, o1, Claude Haiku 4.5, DeepSeek, Grok
Free Tier:      Low tier: 15 RPM, 150 RPD, 8k in / 4k out, 5 concurrent
                High tier: 10 RPM, 50 RPD, 8k in / 4k out, 2 concurrent [reference:57]
                Rate limits depend on Copilot subscription tier (Free/Pro/Pro+) [reference:58]

--------------------------------------------------------------------------------
6.2 NVIDIA NIM
--------------------------------------------------------------------------------
Website:        https://build.nvidia.com
Docs:           https://docs.api.nvidia.com/nim
API Base URL:   https://integrate.api.nvidia.com/v1
Auth:           Bearer token (nvapi-...)
API Format:     OpenAI-compatible
Free Tier:      YES — up to 40 RPM for most models, no per-token billing .
                Some sources mention ~1,000 inference credits on signup and
                possible monthly token cap (~1M tokens/month) [reference:60].
Notes:          Rate limit is per API key (sometimes per account) [reference:61].
                138 free models available, up to 1M context, multimodal
                (audio, embedding, image, PDF, reasoning, rerank, text, video, vision) [reference:62].

--------------------------------------------------------------------------------
6.3 Cloudflare Workers AI
--------------------------------------------------------------------------------
Website:        https://developers.cloudflare.com/workers-ai
API Base URL:   https://api.cloudflare.com/client/v4/accounts/{account_id}/ai/run/{model}
                (OpenAI-compat: https://api.cloudflare.com/client/v4/accounts/{account_id}/ai/v1) [reference:63]
Auth:           Bearer token (CF API token)
API Format:     Custom REST (Cloudflare envelope) + OpenAI-compatible layer
Models:         Llama 4 Scout, Mistral, Qwen, FLUX, Whisper, embeddings [reference:64]
Free Tier:      YES — 10,000 Neurons/day (resets 00:00 UTC), no card stated [reference:65].
                Workers Free also includes 100k requests/day for Worker invocations [reference:66].
Notes:          Neuron costs vary by model: ~50–200 small text (7B),
                ~500–2,000 large text (70B), ~10,000+ image gen [reference:67].
                Errors: 3021 (per-minute rate limit, retryable),
                3036 (daily Neurons exhausted, not retryable today),
                3040 (capacity, retryable) .

--------------------------------------------------------------------------------
6.4 Perplexity (Pro)
--------------------------------------------------------------------------------
Website:        https://www.perplexity.ai
Docs:           https://docs.perplexity.ai
API Base URL:   https://api.perplexity.ai
Auth:           Bearer token
API Format:     OpenAI-compatible
Models:         Sonar, Sonar Pro, Sonar Reasoning
Free Tier:      Pro subscribers get $0 API credit/month (auto-applied on 1st).
                This affects billing/credits, not rate limits directly.
Notes:          Search-augmented answers with cited sources.

--------------------------------------------------------------------------------
6.5 Opencode Zen
--------------------------------------------------------------------------------
Website:        https://opencode.ai/zen
Docs:           https://opencode.ai/docs/zen
API Base URL:   https://opencode.ai/zen/v1
Free Models:    Big Pickle (free during beta), GPT 5 Nano (always free),
                MiMo V2 Flash, Nemotron 3 Super, MiniMax M2.5, Trinity Large
Free Tier:      $0 per 1M tokens on free models; pay-as-you-go for rest.
                Monthly spend caps available.

--------------------------------------------------------------------------------
6.6 Pollinations
--------------------------------------------------------------------------------
Website:        https://pollinations.ai
API Base URL:   https://text.pollinations.ai/{prompt}   (text)
                https://image.pollinations.ai/prompt/{prompt}   (image)
                Append ?model=openai-audio&voice=nova for audio
Auth:           None
API Format:     URL-based (no headers needed)
Free Tier:      Unlimited, no signup, no API key.
Notes:          Open source, privacy-first (zero data storage).
                Supports models like GPT-5, Claude, Gemini for text; Flux, GPT Image
                for images; OpenAI-audio for speech. 500+ community projects.

================================================================================
7. IMAGE GENERATION APIs
================================================================================

Provider              Base URL                              Auth            Notes
--------------------- ------------------------------------- --------------- ---------------------------
OpenAI DALL-E        https://api.openai.com/v1/images/     Bearer          DALL-E 3
Stability AI         https://api.stability.ai/v2beta       Bearer          SD 3.5, SDXL, Cascade
Black Forest Labs    https://api.bfl.ml/v1                 x-key header    FLUX.1 Pro/Dev/Schnell
Ideogram             https://api.ideogram.ai               Api-Key header  Best text rendering
Recraft              https://external.api.recraft.ai/v1    Bearer          Vector + raster
Leonardo AI          https://cloud.leonardo.ai/api/rest/v1 Bearer          Game art presets
Google Imagen        Vertex AI endpoint                    OAuth           Imagen 3/4
Midjourney           Discord bot (no official API)         N/A             Artistic outputs
Pollinations         https://image.pollinations.ai/prompt/  None            Unlimited free
Clipdrop             https://clipdrop-api.co               x-api-key       BG removal, cleanup
Photoroom            https://image-api.photoroom.com/v2    x-api-key       Product photography

================================================================================
8. VIDEO GENERATION APIs
================================================================================

Provider              Base URL                              Auth            Notes
--------------------- ------------------------------------- --------------- ---------------------------
Runway               https://api.dev.runwayml.com/v1       Bearer          Gen-4.5, motion brushes
Pika                 https://api.pika.art                  API key         PikaSwaps, Pikaffects
Luma AI              https://api.lumalabs.ai/dream-machine/v1  Bearer      Ray3 engine, 4K HDR
Kling AI             https://api.klingai.com               Bearer          Up to 2min, 1080p
OpenAI Sora          https://api.openai.com/v1/video       Bearer          Cinematic physics
Synthesia            https://api.synthesia.io/v2           Authorization   230+ avatars, 140+ langs
HeyGen               https://api.heygen.com/v2             X-Api-Key       Dubbing, lip-sync
D-ID                 https://api.d-id.com                  Basic auth      Talking heads, 120+ langs
Google Veo           Vertex AI endpoint                    OAuth           Native audio
Twelve Labs          https://api.twelvelabs.io/v1.2        x-api-key       Video understanding
Decart (Lucy 2)      https://api.decart.ai                 Bearer          Real-time video gen

================================================================================
9. AUDIO & SPEECH APIs
================================================================================

--- Text-to-Speech (TTS) & Voice Cloning ---

Provider              Base URL                              Auth            Notes
--------------------- ------------------------------------- --------------- ---------------------------
ElevenLabs           https://api.elevenlabs.io/v1          xi-api-key      3,000+ voices, 70+ langs
OpenAI TTS           https://api.openai.com/v1/audio/speech Bearer         gpt-4o-mini-tts
Play.ht              https://api.play.ht/api/v2            X-User-ID + Bearer  900+ voices
Resemble AI          https://api.resemble.ai/v2            Bearer          Voice cloning + deepfake detection
Cartesia             https://api.cartesia.ai               X-API-Key       <150ms latency (Sonic)
Speechify            https://api.speechify.ai/v1           Bearer          1,000+ voices
Murf.ai              https://api.murf.ai/v1                api-key         Studio voiceovers
Coqui TTS (local)    Self-hosted                           None            Open source
Piper (local)        Self-hosted                           None            Fast local TTS
Bark (local)         Self-hosted                           None            Multilingual, expressive

--- Speech-to-Text (STT) ---

Provider              Base URL                              Auth            Notes
--------------------- ------------------------------------- --------------- ---------------------------
Deepgram             https://api.deepgram.com/v1           Token           Nova-2, sub-250ms, streaming
AssemblyAI           https://api.assemblyai.com/v2         Authorization   Universal-1, diarization
OpenAI Whisper       https://api.openai.com/v1/audio/transcriptions Bearer  50+ languages
Google Cloud STT     https://speech.googleapis.com/v1      OAuth/API key   60 min/month free
Vosk (local)         Self-hosted                           None            Offline STT
SpeechBrain (local)  Self-hosted                           None            Open-source toolkit

--- Music / Audio Generation ---

Provider              Base URL                              Auth            Notes
--------------------- ------------------------------------- --------------- ---------------------------
Suno                 Web only (no official API)            OAuth (web)     5 songs/day free
Udio                 Web only                              OAuth (web)     Limited free credits
Mubert               https://api.mubert.com/v2             api_key         Real-time generative BG music
Replicate (MusicGen) https://api.replicate.com/v1          Bearer          AudioCraft models
AudioCraft (local)   Self-hosted                           None            Meta's open model

================================================================================
10. SEARCH APIs
================================================================================

Provider              Base URL                              Auth            Notes
--------------------- ------------------------------------- --------------- ---------------------------
Perplexity Sonar     https://api.perplexity.ai             Bearer          LLM answers + citations
Tavily               https://api.tavily.com                api_key (body)  Agent/RAG search, SOC 2
Exa                  https://api.exa.ai                    x-api-key       Neural search (94.9% SimpleQA)
Brave Search         https://api.search.brave.com/res/v1   X-Subscription-Token  Independent, privacy
SerpAPI              https://serpapi.com/search            api_key (query) SERP scraping
You.com              https://api.you.com                   Bearer          Deep Search, MCP
Serper               https://google.serper.dev             X-API-KEY       Fast/cheap Google SERP
SearXNG (local)      Self-hosted                           None            Metasearch, no tracking

================================================================================
11. TRANSLATION APIs
================================================================================

Provider              Base URL                              Auth            Notes
--------------------- ------------------------------------- --------------- ---------------------------
DeepL                https://api-free.deepl.com/v2  (free) Authorization: DeepL-Auth-Key  Best for European langs
                     https://api.deepl.com/v2        (pro)
Google Cloud Trans.  https://translation.googleapis.com/v3 OAuth          130+ langs, AutoML
Microsoft Translator https://api.cognitive.microsofttranslator.com  Ocp-Apim-Subscription-Key  100+ langs
Amazon Translate     AWS endpoint (Translate)              SigV4           AWS-integrated
ModernMT             https://api.modernmt.com/translate    api_key         Learns from corrections
Unbabel              Enterprise API                        Bearer          AI + human editors
LILT                 https://api.lilt.com/v2               Bearer          Enterprise localization
Phrase               https://api.phrase.com/v2             Bearer          Dev-friendly, CLI
Lokalise             https://api.lokalise.com/api2          X-Api-Token     400+ langs
Tolgee               Self-hosted/cloud                     Bearer          In-context translation
LibreTranslate       Self-hosted or https://libretranslate.com  None       Open source
MyMemory             https://api.mymemory.translated.net   None            5,000 words/day
Lingva               https://lingva.ml/api/v1              None            Google alt, no tracking

================================================================================
12. EMBEDDING APIs
================================================================================

Provider              Base URL                              Auth            Notes
--------------------- ------------------------------------- --------------- ---------------------------
OpenAI Embeddings    https://api.openai.com/v1/embeddings  Bearer          text-embedding-3-small/large
Voyage AI            https://api.voyageai.com/v1           Bearer          Voyage 4, 50M tokens free
Cohere Embed         https://api.cohere.com/v1/embed       Bearer          Embed v3/v4 multilingual
Google Embedding     Vertex AI endpoint                    OAuth           Gecko, multimodal
Jina AI              https://api.jina.ai/v1                Bearer          1M tokens free, reranking
Nomic                https://api-atlas.nomic.ai/v1         Bearer          Open-source, free tier
Ollama (local)       http://localhost:11434/v1             None            Unlimited local embeddings

================================================================================
13. VECTOR DATABASES
================================================================================

Provider         Type                Website                           Notes
---------------- --------------- ------------------------------------- ------------------------------------
Pinecone         Managed cloud       https://www.pinecone.io            Serverless, billions of vectors
Weaviate         Cloud / self-host   https://weaviate.io                Hybrid search (vector + keyword)
Qdrant           Cloud / self-host   https://qdrant.tech                High QPS at 99% recall
Chroma           Local / cloud       https://www.trychroma.com          Dev-friendly, great for RAG prototypes
Milvus           Self-host / cloud   https://milvus.io                  Billion-scale, low latency
Zilliz Cloud     Managed Milvus      https://zilliz.com                 Enterprise SLAs
pgvector         Postgres extension  https://github.com/pgvector/pgvector  Vectors + relational data
LanceDB          Serverless          https://lancedb.com                Lance columnar format, zero-copy

================================================================================
14. LOCAL / SELF-HOSTED INFERENCE
================================================================================

Tool            Base URL (local)              Notes
--------------- ----------------------------- ----------------------------------------------------
Ollama          http://localhost:11434/v1     One command to run any model. OpenAI-compatible.
LM Studio       http://localhost:1234/v1      GUI + local server, GGUF support
llama.cpp       http://localhost:8080/v1      C/C++ engine, CPU-optimized, quantization
vLLM            http://localhost:8000/v1      High-throughput, PagedAttention
LocalAI         http://localhost:8080/v1      OpenAI-compatible self-hosted
Jan             (app)                         Offline-first desktop assistant
MLX             (Apple Silicon)               Apple's array/ML framework
ExecuTorch      (mobile)                      Meta's on-device framework (50KB footprint)
LlamaEdge       (WASM)                        Edge runtime via WebAssembly
NVIDIA TensorRT-LLM (local)                   GPU inference optimization for NVIDIA
Ollama Cloud    https://ollama.com            Free tier: 5h session / 5d weekly limits

================================================================================
15. GPU CLOUD PROVIDERS
================================================================================

Provider         Website                           Notes
---------------- --------------------------------- ------------------------------------------
RunPod           https://www.runpod.io             On-demand + serverless A100/H100
Lambda Cloud     https://lambdalabs.com            H100/A100, zero egress, InfiniBand
CoreWeave        https://www.coreweave.com         Kubernetes-native hyperscale
Vast.ai          https://vast.ai                   Marketplace, bidding, cheapest
Nebius           https://nebius.com                Blackwell Ultra, EU data centers
TensorDock       https://tensordock.com            100+ global locations
Paperspace       https://www.paperspace.com        DigitalOcean-owned, notebooks
Crusoe Cloud     https://crusoecloud.com           Clean-energy powered
Fluidstack       https://fluidstack.io             Distributed idle compute
Modal            https://modal.com                 Serverless GPU, $30/month free
Anyscale         https://www.anyscale.com          Ray-based distributed compute
Predibase        https://predibase.com             LoRAX multi-adapter serving

================================================================================
16. MCP (MODEL CONTEXT PROTOCOL)
================================================================================

Website:        https://modelcontextprotocol.io
Spec:           https://spec.modelcontextprotocol.io
Governance:     Donated to Linux Foundation AAIF (originally Anthropic)

Core Protocol
-------------
MCP Specification         https://modelcontextprotocol.io/specification
MCP TypeScript SDK        npm install @modelcontextprotocol/sdk
MCP Python SDK            pip install mcp
MCP Registry              ~2,000 entries (407% growth since launch)

Notable MCP Servers
-------------------
Official Servers Repo     https://github.com/modelcontextprotocol/servers
Awesome MCP Servers       https://github.com/punkpeye/awesome-mcp-servers (97k stars)
Playwright MCP            Microsoft's browser automation (39k stars)
ActionKit by Paragon      130+ SaaS integrations

MCP makes any LLM able to:
  - Call external tools
  - Read from data sources
  - Execute actions in software

================================================================================
17. UNIVERSAL API FORMAT PATTERNS (CHEAT SHEET)
================================================================================

Most providers follow one of these three patterns. If you're building an AI model
that ingests provider data, normalize to Pattern A first — ~80% of providers use it.

--------------------------------------------------------------------------------
PATTERN A: OpenAI-Compatible (most common)
--------------------------------------------------------------------------------
Endpoint format:
  POST {base_url}/chat/completions
  POST {base_url}/embeddings
  POST {base_url}/images/generations
  GET  {base_url}/models

Headers:
  Authorization: Bearer {api_key}
  Content-Type: application/json

Request body (chat):
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

Response:
  {
    "id": "chatcmpl-...",
    "object": "chat.completion",
    "created": 1234567890,
    "model": "model-name",
    "choices": [{
      "index": 0,
      "message": {"role": "assistant", "content": "..."},
      "finish_reason": "stop"
    }],
    "usage": {"prompt_tokens": 10, "completion_tokens": 20, "total_tokens": 30}
  }

Providers using Pattern A:
  OpenAI, Groq, Together, Fireworks, Cerebras, SambaNova, DeepInfra,
  OpenRouter, DeepSeek, xAI, Novita, Hyperbolic, AIML API, Vercel AI GW,
  GitHub Models, NVIDIA NIM, Qwen/DashScope, Zhipu, Moonshot, Yi,
  MiniMax, iFlow, LongCat, Ollama, LM Studio, vLLM, LocalAI

--------------------------------------------------------------------------------
PATTERN B: Custom REST (Anthropic-style)
--------------------------------------------------------------------------------
Endpoint format:
  POST {base_url}/messages

Headers:
  x-api-key: {api_key}
  anthropic-version: 2023-06-01
  Content-Type: application/json

Request body:
  {
    "model": "claude-sonnet-4-20250514",
    "max_tokens": 1024,
    "system": "...",
    "messages": [
      {"role": "user", "content": "..."}
    ]
  }

Response:
  {
    "id": "msg_...",
    "type": "message",
    "role": "assistant",
    "content": [{"type": "text", "text": "..."}],
    "model": "...",
    "stop_reason": "end_turn",
    "usage": {"input_tokens": 10, "output_tokens": 20}
  }

Providers using Pattern B:
  Anthropic, Google Gemini (native), Cohere, AI21, AWS Bedrock

--------------------------------------------------------------------------------
PATTERN C: URL-Based (no auth, no headers)
--------------------------------------------------------------------------------
Endpoint format:
  GET {base_url}/{prompt}

Example (Pollinations):
  https://text.pollinations.ai/What is AI?
  https://image.pollinations.ai/prompt/a%20cat%20wearing%20a%20hat
  https://text.pollinations.ai/Hello?model=openai-audio&voice=nova

Providers using Pattern C:
  Pollinations

--------------------------------------------------------------------------------
PATTERN D: WebSocket Streaming (realtime)
--------------------------------------------------------------------------------
Used for voice, live transcription, and realtime multimodal:

  OpenAI Realtime API      wss://api.openai.com/v1/realtime
  Google Gemini Live       wss://generativelanguage.googleapis.com/ws/...
  Deepgram Streaming       wss://api.deepgram.com/v1/listen
  LiveKit                  wss://... (WebRTC)

================================================================================
18. QUICK REFERENCE MATRIX (UPDATED)
================================================================================

Provider          Auth            Base URL Prefix                                Free Tier?
----------------- --------------- ---------------------------------------------- -----------
OpenAI            Bearer          https://api.openai.com/v1                      No
Anthropic         x-api-key       https://api.anthropic.com/v1                   No
Google Gemini     API key         https://generativelanguage.googleapis.com      YES (variable)
Mistral           Bearer          https://api.mistral.ai/v1                      YES (Free mode)
DeepSeek          Bearer          https://api.deepseek.com/v1                    No (cheap)
Cohere            Bearer          https://api.cohere.com/v1                      YES (trial)
AI21              Bearer          https://api.ai21.com/studio/v1                 Trial
xAI               Bearer          https://api.x.ai/v1                            Trial
Groq              Bearer          https://api.groq.com/openai/v1                 YES (generous)
Cerebras          Bearer          https://api.cerebras.ai/v1                     $5 credit (card req.)
Together          Bearer          https://api.together.xyz/v1                    $5 credit
Fireworks         Bearer          https://api.fireworks.ai/inference/v1          $1 credit
SambaNova         Bearer          https://api.sambanova.ai/v1                    YES (tightened)
Replicate         Bearer          https://api.replicate.com/v1                   $5 credit
DeepInfra         Bearer          https://api.deepinfra.com/v1/openai            Credits
fal.ai            Key header      https://fal.run                                Pay-per-use
Novita            Bearer          https://api.novita.ai/v3/openai                $0.50 credit
Hyperbolic        Bearer          https://api.hyperbolic.xyz/v1                  Trial
OpenRouter        Bearer          https://openrouter.ai/api/v1                   YES (:free)
LiteLLM           Configurable    Self-hosted (localhost:4000)                   N/A
Portkey           x-portkey-key   https://api.portkey.ai/v1                      Trial
Helicone          Helicone-Auth   https://oai.helicone.ai/v1                     Trial
AIML API          Bearer          https://api.aimlapi.com/v1                     YES (limited)
Vercel AI GW      Bearer          https://api.vercel.ai/v1                       $5/mo
Hugging Face      Bearer          https://router.huggingface.co/v1               $0.10/mo
GitHub Models     GitHub PAT      https://models.inference.ai.azure.com          YES
NVIDIA NIM        Bearer          https://integrate.api.nvidia.com/v1            YES (40 RPM)
Cloudflare AI     Bearer          https://api.cloudflare.com/client/v4/...       YES (10k Neurons/day)
Perplexity        Bearer          https://api.perplexity.ai                      Pro credit
Opencode Zen      Bearer          https://opencode.ai/zen/v1                     YES (free models)
Pollinations      None            https://text.pollinations.ai                   Unlimited
iFlow             Bearer          https://apis.iflow.cn/v1                       YES (1 concurrent)
LongCat           Bearer          https://api.longcat.chat/openai/v1             YES (500k/day)
Qwen/DashScope    Bearer          https://dashscope-intl.aliyuncs.com/...        YES (1M tokens/90d)
Zhipu/GLM         Bearer          https://open.bigmodel.cn/api/paas/v4           Trial
Moonshot          Bearer          https://api.moonshot.cn/v1                     Trial
Yi/01.AI          Bearer          https://api.lingyiwanwu.com/v1                 Trial
MiniMax           Bearer          https://api.minimax.chat/v1                    Trial
Anyscale          Bearer          https://api.endpoints.anyscale.com/v1          Trial
AWS Bedrock       SigV4           https://bedrock-runtime.{region}.amazonaws.com No
Azure OpenAI      api-key/OAuth   https://{res}.openai.azure.com                 No
Google Vertex     OAuth           https://{region}-aiplatform.googleapis.com     No
Ollama            None            http://localhost:11434/v1                      Unlimited local
LM Studio         None            http://localhost:1234/v1                       Unlimited local
vLLM              None            http://localhost:8000/v1                       Unlimited local
LocalAI           None            http://localhost:8080/v1                       Unlimited local
Stability AI      Bearer          https://api.stability.ai/v2beta                Credits
BFL FLUX          x-key           https://api.bfl.ml/v1                          Pay-per-use
Ideogram          Api-Key         https://api.ideogram.ai                        Credits
ElevenLabs        xi-api-key      https://api.elevenlabs.io/v1                   Trial
Deepgram          Token           https://api.deepgram.com/v1                    $200 credit
AssemblyAI        Authorization   https://api.assemblyai.com/v2                  Free hours
Cartesia          X-API-Key       https://api.cartesia.ai                        Trial
Tavily            api_key body    https://api.tavily.com                         1k/mo free
Exa               x-api-key       https://api.exa.ai                             1k/mo free
Brave Search      X-Sub-Token     https://api.search.brave.com/res/v1            2k/mo free
SerpAPI           api_key query   https://serpapi.com/search                     100/mo free
Serper            X-API-KEY       https://google.serper.dev                      Trial
DeepL             DeepL-Auth-Key  https://api-free.deepl.com/v2                  500k chars/mo
Runway            Bearer          https://api.dev.runwayml.com/v1                Trial
HeyGen            X-Api-Key       https://api.heygen.com/v2                      Trial
D-ID              Basic auth      https://api.d-id.com                           Trial
Twelve Labs       x-api-key       https://api.twelvelabs.io/v1.2                 Trial
Pinecone          Api-Key         Per-index host                                 Free tier
Weaviate          Bearer/OAuth    Per-instance                                   Free sandbox
Qdrant            api-key         Per-cluster                                    Free tier
Chroma            None/Bearer     Local or https://api.trychroma.com             Free local
Milvus            None/Bearer     Self-host or Zilliz                            Free
Voyage AI         Bearer          https://api.voyageai.com/v1                    50M tokens
Jina AI           Bearer          https://api.jina.ai/v1                         1M tokens
Nomic             Bearer          https://api-atlas.nomic.ai/v1                  Free tier

================================================================================
19. PRACTICAL NOTES & GOTCHAS
================================================================================

1. FREE TIER VOLATILITY
   Free tiers changed significantly in 2026. Cerebras and SambaNova now require
   payment methods or purchase credits for usable free access [reference:69][reference:70].
   Google and Mistral no longer publish per-model limits publicly — check their
   consoles. Always verify at the provider's docs before building.

2. RATE LIMIT HEADERS
   Most OpenAI-compatible providers return rate-limit headers:
   - x-ratelimit-limit-requests / x-ratelimit-remaining-requests
   - x-ratelimit-limit-tokens / x-ratelimit-remaining-tokens
   - retry-after (seconds to wait after 429)
   Groq's headers refer to RPD for "requests" and TPM for "tokens" [reference:71].

3. 402 VS 429
   - 429 = rate limit exceeded (wait and retry).
   - 402 = payment required (OpenRouter returns this even on free models if
     balance is negative) [reference:72].

4. AUTH QUIRKS
   - Anthropic: x-api-key + anthropic-version (NOT Bearer).
   - Azure OpenAI: api-key header (NOT Bearer) or Azure AD token.
   - Stability AI: Bearer (standard).
   - fal.ai: Authorization: Key <FAL_KEY> (not Bearer).
   - AWS Bedrock: SigV4 signing (not a simple header).
   - Google: API key as query param or x-goog-api-key header.

5. CONTEXT WINDOW CHANGES
   - DeepSeek now offers 1M context (V4.1 Flash / V4 Pro) [reference:73].
   - Gemini 2.5 Pro: 2M tokens.
   - GPT-5: 400K (1M select variants) [reference:74].
   - Llama 4: full 1M context on Fireworks, narrower on Groq/Oracle [reference:75].
   - Qwen3.8-max: 1M context [reference:76].

6. MODEL NAMING CHANGES
   - Claude: claude-opus-4, claude-sonnet-4, claude-haiku-4 (2026 naming) [reference:77].
   - OpenAI: gpt-5, gpt-5-mini (GPT-5 released Aug 2025) [reference:78].
   - DeepSeek: deepseek-flash and deepseek-v4-pro (legacy names retired) [reference:79].
   - Qwen: qwen3.8-max, qwen3.7-plus, qwen3.8-flash [reference:80].
   - Llama: Llama 4 Scout (17B active) and Maverick (17B active/128 experts) [reference:81].

7. PROVIDER-SPECIFIC GOTCHAS
   - Groq rate limits are per organization, not per key. Extra keys don't help [reference:82].
   - NVIDIA NIM rate limit is per API key (or per account, varies) [reference:83].
   - Cloudflare Neurons reset daily at 00:00 UTC. Large models consume
     disproportionately more neurons (image gen ~10k/request) [reference:84].
   - OpenRouter: buying $10 credits ONCE permanently raises daily free limit
     from 50 to 1,000 [reference:85].
   - LongCat: quotas reset at Beijing midnight, do not roll over.
   - iFlow: only 1 concurrent request per user; additional requests get 429.

8. BUILDING FOR MULTI-PROVIDER
   - Use an OpenAI-compatible client (openai-python, openai-node, LiteLLM) and
     swap base_url + api_key. Covers ~80% of providers.
   - For Anthropic, use the anthropic SDK or route through LiteLLM/OpenRouter.
   - For Gemini, use google-genai SDK or the OpenAI-compat endpoint.
   - For Bedrock/Vertex, use their native SDKs (boto3, google-cloud-aiplatform)
     or LiteLLM's abstraction.

9. FREE-TIER STRATEGY FOR PRODUCTION
   - Don't rely on free tiers for production traffic — limits can change without
     notice. Use them for prototyping, fallbacks, or low-priority batch jobs.
   - For zero-cost production, self-host open-weight models (Ollama, vLLM) or
     use Puter.js (user-pays) for web apps.
   - Combine providers: Groq for speed, Gemini for long context, Groq/Cerebras
     for high-volume simple tasks.

================================================================================
                            END OF REFERENCE
================================================================================
