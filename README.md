# Best AI Gateways

An AI gateway is a control point between applications and the model providers, MCP servers, and agents they call. It gives callers one API and applies routing, access control, spend limits, and logging to that traffic. Products using the label differ in what they govern, where they run, and which features require a paid tier.

This list selects 14 AI gateways that meet the criteria below. Each entry gives the license and deployment model, what the gateway does well, a real limitation, and who it suits. The full catalog is [Awesome AI Gateways](https://github.com/ai-gateways/awesome-ai-gateways#ai-gateways), and the [AI gateway guide](https://github.com/ai-gateways/ai-gateway#what-is-an-ai-gateway) explains how the technology works.

## Contents

- [How these AI gateways were selected](#how-these-ai-gateways-were-selected)
- [AI gateway comparison](#ai-gateway-comparison)
- [Best open-source AI gateways](#best-open-source-ai-gateways)
  - [Bifrost](#bifrost)
  - [LiteLLM](#litellm)
  - [Portkey AI Gateway](#portkey-ai-gateway)
  - [Kong AI Gateway](#kong-ai-gateway)
  - [agentgateway](#agentgateway)
  - [Agent Router](#agent-router)
  - [New API](#new-api)
  - [Higress](#higress)
  - [Apache APISIX](#apache-apisix)
- [Best managed AI gateways](#best-managed-ai-gateways)
  - [Cloudflare AI Gateway](#cloudflare-ai-gateway)
  - [Vercel AI Gateway](#vercel-ai-gateway)
  - [OpenRouter](#openrouter)
  - [Azure API Management](#azure-api-management)
  - [Google Cloud Apigee](#google-cloud-apigee)
- [How to choose an AI gateway](#how-to-choose-an-ai-gateway)
- [What this list leaves out](#what-this-list-leaves-out)
- [Related guides](#related-guides)

## How these AI gateways were selected

A platform is on this list only when its own repository or documentation shows that it meets every test below. Features in a paid edition count toward the tests, and each entry says which ones are paid.

- **One API across providers.** Callers reach models from at least three independent providers through a single API.
- **Failover or load balancing.** The gateway routes around failures or spreads traffic across providers, models, or deployments.
- **Per-consumer controls.** Gateway-issued keys, budgets, or token limits apply per team, application, or key.
- **Usage visibility.** Request logs, metrics, or traces record usage such as token counts or cost.
- **Usable from any stack.** Applications can call the gateway without being hosted on the vendor's platform.
- **Gateway-first and built for shared use.** The gateway is the product's main job, and it serves teams running shared traffic rather than individuals pooling free tiers or personal subscriptions.
- **Adoption and upkeep.** Open-source projects need at least 2,000 GitHub stars and a commit in the last six months. Closed products need self-serve access, public documentation, and a large existing user base through the vendor's cloud, network, or developer platform. OpenRouter qualifies through its model marketplace.

## AI gateway comparison

The table compares the 14 gateways on license, deployment, other traffic they govern, failover, and spend controls. A dash means the sources reviewed for this list do not document that traffic type, not that the feature is absent. Each entry below links the source for its row.

| Gateway | License | Deployment | Also governs | Failover or load balancing | Spend or token controls |
|---|---|---|---|---|---|
| [Bifrost](https://github.com/maximhq/bifrost#key-features) | Apache 2.0 | Self-hosted | MCP, A2A | Fallbacks and load balancing; adaptive routing is Enterprise | Virtual keys, budgets, rate limits |
| [LiteLLM](https://github.com/BerriAI/litellm#why-litellm) | MIT, except `enterprise/` | Self-hosted | MCP, A2A | Load balancing | Virtual keys, spend tracking |
| [Portkey AI Gateway](https://github.com/Portkey-AI/gateway#reliable-routing) | MIT | Self-hosted, or hosted by the vendor | MCP (Portkey platform) | Fallbacks, retries, weighted load balancing | Virtual keys, usage analytics |
| [Kong AI Gateway](https://developer.konghq.com/ai-gateway/#three-traffic-types-unified-control) | Apache 2.0 core, Enterprise plugins | Self-hosted or Konnect | MCP, A2A | Load balancing is Enterprise | Token quotas and cost budgets |
| [agentgateway](https://github.com/agentgateway/agentgateway#key-features) | Apache 2.0 | Self-hosted binary or Kubernetes | MCP, A2A | Load balancing, failover | Per-key dollar or token budgets |
| [Agent Router](https://github.com/theagentrouter/agent-router#formerly-envoy-ai-gateway) | Apache 2.0 | Kubernetes with Envoy Gateway, or `aigw` CLI | MCP | Failover | Quotas, usage attribution |
| [New API](https://github.com/QuantumNous/new-api#capabilities) | AGPL-3.0 with added terms | Self-hosted | - | Channel priorities, weights, retries | Quotas, API key restrictions |
| [Higress](https://github.com/higress-group/higress#use-cases) | Apache 2.0 | Docker or Kubernetes | MCP server hosting | Multi-model load balancing | Token rate limiting |
| [Apache APISIX](https://apisix.apache.org/docs/apisix/plugins/ai-proxy-multi/#description) | Apache 2.0 | Self-hosted | - | Load balancing, retries, fallbacks | Token quotas per consumer |
| [Cloudflare AI Gateway](https://developers.cloudflare.com/ai-gateway/#features) | Proprietary | Managed | MCP through separate portals | Fallback, dynamic routing | Budget and rate limits in dynamic routes |
| [Vercel AI Gateway](https://vercel.com/docs/ai-gateway#centralize-multi-provider-ai-operations) | Proprietary | Managed | - | Provider and model failover | Budgets per team, project, key, or member |
| [OpenRouter](https://openrouter.ai/docs/quickstart#using-the-openrouter-api) | Proprietary | Managed | - | Automatic model fallbacks | Credit limits per key |
| [Azure API Management](https://learn.microsoft.com/en-us/azure/api-management/genai-gateway-capabilities#traffic-mediation-and-control) | Proprietary | Azure service | MCP, A2A | Load balancer, circuit breaker | Token limits per consumer |
| [Google Cloud Apigee](https://cloud.google.com/solutions/apigee-ai#:~:text=Multicloud%20model%20routing) | Proprietary | Google Cloud service | - | Circuit breaker pattern | Token limit enforcement |

Details reflect each project's repository or documentation in November 2026; confirm current capabilities before choosing.

## Best open-source AI gateways

Nine open-source gateways meet the criteria. All can be self-hosted, which keeps prompts, responses, and logs inside your own network. They differ in implementation language, license terms, and how much of the feature set sits in a paid edition.

### Bifrost

[Bifrost](https://github.com/maximhq/bifrost#the-fastest-way-to-build-ai-applications-that-never-go-down), built by Maxim AI, is a Go gateway that puts model calls behind one OpenAI-compatible API and also governs [MCP tool calls](https://github.com/maximhq/bifrost/blob/dev/docs/mcp/overview.mdx#L134) and [agent-to-agent traffic](https://github.com/maximhq/bifrost/blob/dev/docs/features/agent-gateway/overview.mdx#L10).

- **License and deployment:** [Apache 2.0](https://github.com/maximhq/bifrost#license). Self-hosted through [npx, Docker, or the Go SDK](https://github.com/maximhq/bifrost#getting-started-options), or on [Kubernetes and other container platforms](https://github.com/maximhq/bifrost/blob/dev/docs/deployment-guides/overview.mdx#L11).
- **Does well:** Covers 25+ model providers in its [provider support matrix](https://github.com/maximhq/bifrost/blob/dev/docs/providers/supported-providers/overview.mdx#L13), with [automatic fallbacks and load balancing](https://github.com/maximhq/bifrost#core-infrastructure), [budgets and rate limits](https://github.com/maximhq/bifrost/blob/dev/docs/features/governance/budget-and-limits.mdx#L7) on virtual keys, and [semantic caching](https://github.com/maximhq/bifrost/blob/dev/docs/features/semantic-caching.mdx#L16). The project's [published benchmark](https://github.com/maximhq/bifrost#performance) reports 11 µs of added overhead per request at a sustained 5,000 RPS on a t3.xlarge.
- **Limitation:** [Clustering](https://github.com/maximhq/bifrost/blob/dev/docs/enterprise/clustering.mdx#L7), [adaptive load balancing](https://github.com/maximhq/bifrost/blob/dev/docs/enterprise/adaptive-routing/overview.mdx#L65), [guardrails](https://github.com/maximhq/bifrost/blob/dev/docs/enterprise/guardrails.mdx#L7), [role-based access control](https://github.com/maximhq/bifrost/blob/dev/docs/enterprise/rbac.mdx#L7), [audit logs](https://github.com/maximhq/bifrost/blob/dev/docs/enterprise/audit-logs.mdx#L7), and [in-VPC deployment](https://github.com/maximhq/bifrost/blob/dev/docs/enterprise/invpc-deployments.mdx#L9) are Enterprise features. The deployment guides cover self-hosting, so your team operates the gateway. Its provider count is lower than the 100+ LiteLLM lists.
- **Suits:** Platform teams that want one self-hosted gateway for model, tool, and agent traffic, especially when agent loops make many calls and added latency compounds.

### LiteLLM

[LiteLLM](https://github.com/BerriAI/litellm#what-is-litellm) is a Python SDK and proxy server that calls 100+ LLM providers in the OpenAI format.

- **License and deployment:** [MIT, except the `enterprise/` directory](https://github.com/BerriAI/litellm/blob/main/LICENSE#L3). Self-hosted with [Docker or Terraform](https://github.com/BerriAI/litellm#get-started).
- **Does well:** Provider breadth, plus [virtual keys, spend tracking, guardrails, load balancing, and an admin dashboard](https://github.com/BerriAI/litellm#why-litellm). The proxy also serves as an [MCP gateway](https://docs.litellm.ai/docs/mcp#:~:text=control%20MCP%20access%20by%20Key) and an [A2A gateway](https://github.com/BerriAI/litellm#features). The README reports 8 ms P95 latency at 1,000 RPS.
- **Limitation:** [Single sign-on and audit logs](https://docs.litellm.ai/docs/enterprise#:~:text=single%20sign-on%2C%20audit%20logs) require the Enterprise license.
- **Suits:** Python teams that need the widest provider coverage from a self-hosted proxy.

### Portkey AI Gateway

[Portkey AI Gateway](https://github.com/Portkey-AI/gateway#ai-gateway) is a TypeScript gateway that routes to 1,600+ language, vision, audio, and image models.

- **License and deployment:** [MIT](https://github.com/Portkey-AI/gateway/blob/main/LICENSE#L1). Self-hosted on [Docker, Node.js, or Cloudflare Workers](https://github.com/Portkey-AI/gateway/blob/main/docs/installation-deployments.md#local-deployment), or through Portkey's hosted and enterprise versions.
- **Does well:** Config-driven [fallbacks, retries with exponential backoff, and weighted load balancing](https://github.com/Portkey-AI/gateway#reliable-routing), plus [guardrails](https://github.com/Portkey-AI/gateway#security--accuracy). The README claims under 1 ms of latency and a 122 KB footprint.
- **Limitation:** [Palo Alto Networks closed its acquisition of Portkey](https://www.paloaltonetworks.com/company/press/2026/palo-alto-networks-completes-acquisition-of-portkey-to-secure-ai-agents#:~:text=as%20the%20core%20AI%20Gateway%20for%20Prisma%20AIRS) on May 29, 2026, and plans to make it the core gateway for Prisma AIRS. The newest tagged release of the open-source repository is [v1.15.2 from January 2026](https://github.com/Portkey-AI/gateway/releases/tag/v1.15.2). Semantic caching and provider optimization are [limited to the hosted and enterprise versions](https://github.com/Portkey-AI/gateway#cost-management).
- **Suits:** JavaScript and edge teams that want a small, config-driven router and have confirmed the open-source project's direction after the acquisition.

### Kong AI Gateway

[Kong AI Gateway](https://developer.konghq.com/ai-gateway/#three-traffic-types-unified-control) adds AI plugins to Kong Gateway, so one gateway handles API, LLM, MCP, and A2A traffic.

- **License and deployment:** [Apache 2.0](https://github.com/Kong/kong#license) for Kong Gateway, with some AI plugins limited to the AI Gateway Enterprise offering. [Self-hosted](https://github.com/Kong/kong#getting-started) or on Kong Konnect.
- **Does well:** A [universal LLM API](https://github.com/Kong/kong#features) across providers such as OpenAI, Anthropic, Gemini, Bedrock, and Azure AI, with plugins for AI observability, semantic caching, and semantic routing, plus [token quotas and cost budgets](https://developer.konghq.com/ai-gateway/#:~:text=token%20quotas%20and%20cost%20budgets).
- **Limitation:** [AI Proxy Advanced](https://developer.konghq.com/plugins/ai-proxy-advanced/#load-balancing), the plugin that load balances across models, is [only available in AI Gateway Enterprise](https://developer.konghq.com/plugins/ai-proxy-advanced/#:~:text=only%20available%20as%20part%20of%20our%20AI%20Gateway%20Enterprise).
- **Suits:** Teams that already run Kong for API traffic and want LLM controls in the same plugin model.

### agentgateway

[agentgateway](https://github.com/agentgateway/agentgateway#key-features) is a Rust proxy and [Linux Foundation](https://github.com/agentgateway/agentgateway#:~:text=Linux%20Foundation) project built on MCP and A2A, with LLM, MCP, and A2A gateway functions.

- **License and deployment:** Apache 2.0. Self-hosted as a [standalone binary driven by YAML, or on Kubernetes](https://github.com/agentgateway/agentgateway#documentation) with a built-in controller and Gateway API support.
- **Does well:** A [unified OpenAI-compatible API](https://github.com/agentgateway/agentgateway#key-features) with load balancing, failover, and [per-key dollar or token budgets](https://agentgateway.dev/docs/standalone/latest/documentation/llm/cost-controls/budget-limits/per-key/), plus routing to self-hosted models through Kubernetes Inference Gateway extensions.
- **Limitation:** [Per-key budgets depend on a configured database and model catalog](https://agentgateway.dev/docs/standalone/latest/documentation/llm/cost-controls/budget-limits/per-key/#:~:text=Start%20agentgateway%20with%20a%20database), so budgets add a stateful dependency to an otherwise config-driven proxy.
- **Suits:** Kubernetes platform teams that want one open-source data plane for model, tool, and agent traffic, including self-hosted inference.

### Agent Router

[Agent Router](https://github.com/theagentrouter/agent-router#formerly-envoy-ai-gateway), formerly Envoy AI Gateway, is an Agentic AI Foundation project that gives applications one OpenAI-compatible API for hosted models, self-hosted inference, and MCP servers.

- **License and deployment:** Apache 2.0. Runs through the [`aigw` CLI, or on Kubernetes with Envoy Gateway](https://github.com/theagentrouter/agent-router#quick-start).
- **Does well:** Keeps [credentials, routing, quotas, failover, and usage attribution](https://github.com/theagentrouter/agent-router#agent-router) in one place, enforced by Envoy, with a broad [provider list](https://github.com/theagentrouter/agent-router#supported-ai-providers).
- **Limitation:** The README presents the standalone CLI for [running on a laptop](https://github.com/theagentrouter/agent-router#quick-start), so production deployments assume Kubernetes and Envoy Gateway.
- **Suits:** Platform teams already invested in Envoy and Kubernetes.

### New API

[New API](https://github.com/QuantumNous/new-api#capabilities) is a self-hosted gateway and web console that exposes OpenAI, Anthropic, and Gemini API formats over many upstream providers.

- **License and deployment:** [AGPL-3.0 with additional terms](https://github.com/QuantumNous/new-api#-license). Self-hosted with [Docker Compose](https://github.com/QuantumNous/new-api#deployment), by default with PostgreSQL and Redis.
- **Does well:** [Channel priorities, weights, retries, quotas, usage logs, audit logs, and per-user access control](https://github.com/QuantumNous/new-api#capabilities), all managed from a console available in seven languages.
- **Limitation:** The added license terms require modified versions to [keep the attribution notice and a visible link to the project](https://github.com/QuantumNous/new-api#-license), which matters for teams that rebrand internal tools.
- **Suits:** Teams that want a self-hosted console with per-user quotas and pricing, and are comfortable with AGPL terms.

### Higress

[Higress](https://github.com/higress-group/higress#what-is-higress) is a CNCF sandbox API gateway based on Istio and Envoy, extended with Wasm plugins.

- **License and deployment:** Apache 2.0. Runs [with Docker or on Kubernetes](https://github.com/higress-group/higress#quick-start).
- **Does well:** [A unified protocol across LLM providers, AI observability, multi-model load balancing, token rate limiting, and caching](https://github.com/higress-group/higress#use-cases), plus hosting for MCP servers. Its provider support spans both Chinese and international model providers.
- **Limitation:** The README describes the [Docker path](https://github.com/higress-group/higress#:~:text=for%20learning%20or%20for%20building%20simple%20sites) as suited to learning or simple sites, so production use means operating it on Kubernetes.
- **Suits:** Kubernetes teams that use both Chinese and international model providers, or that already run Istio or Envoy.

### Apache APISIX

[Apache APISIX](https://github.com/apache/apisix#ai-gateway) is an Apache Software Foundation API gateway that serves as an AI gateway through plugins.

- **License and deployment:** Apache 2.0. Self-hosted.
- **Does well:** The [`ai-proxy-multi` plugin](https://apisix.apache.org/docs/apisix/plugins/ai-proxy-multi/#description) adds load balancing, retries, fallbacks, and health checks across providers, with [rate limits per consumer](https://apisix.apache.org/docs/apisix/plugins/ai-proxy-multi/#load-balance-and-rate-limit-by-consumers) and token usage in access logs.
- **Limitation:** [Token quotas count provider-reported usage](https://apisix.apache.org/ai-gateway/#:~:text=Count%20provider-reported%20token%20usage) rather than dollars, and [retry and health-check behavior depends on the selected algorithm](https://apisix.apache.org/ai-gateway/#:~:text=retry%20and%20health-check%20behavior%20depends%20on%20the%20selected%20algorithm).
- **Suits:** Teams already running APISIX that want to add LLM routing through plugins.

## Best managed AI gateways

The managed services below meet the same criteria. They remove the work of operating a gateway. The trade-off is that AI traffic passes through the vendor's service and the configuration is tied to that vendor.

### Cloudflare AI Gateway

[Cloudflare AI Gateway](https://developers.cloudflare.com/ai-gateway/#features) is a managed gateway on Cloudflare's network with analytics, logging, caching, rate limiting, and model fallback.

- **License and deployment:** Proprietary. Managed by Cloudflare and available on all plans.
- **Does well:** [Dynamic routes](https://developers.cloudflare.com/ai-gateway/features/dynamic-routing/#:~:text=Budget%20Limit) apply rate and budget limits and switch to a fallback when a limit is exceeded.
- **Limitation:** Hosted only, and [plan limits apply](https://developers.cloudflare.com/ai-gateway/reference/limits/#gateway-limits): 10 gateways per account on the free plan, 20 on paid plans, and 200 requests per 60 seconds per gateway through Unified Billing.
- **Suits:** Teams already on Cloudflare that want logging and caching without running infrastructure.

### Vercel AI Gateway

[Vercel AI Gateway](https://vercel.com/docs/ai-gateway#centralize-multi-provider-ai-operations) is a managed gateway for calling models across providers from any server, cloud, or local environment.

- **License and deployment:** Proprietary. Managed by Vercel and available on all plans. Applications [do not need to run on Vercel](https://vercel.com/docs/ai-gateway#:~:text=Your%20application%20does%20not%20need%20to%20run%20on%20Vercel).
- **Does well:** Centralized credentials, request logs, provider and model failover, and budgets per team, project, API key, or member. Vercel [charges no markup or platform fee on tokens](https://vercel.com/docs/ai-gateway/pricing#:~:text=charges%20no%20markup).
- **Limitation:** Hosted only, and [budgets cover only spend billed through system credentials](https://vercel.com/docs/ai-gateway#:~:text=BYOK%20spend%20is%20metered%20separately), so bring-your-own-key usage does not count toward those limits.
- **Suits:** Product teams that want multi-provider access and spend limits with no gateway to operate.

### OpenRouter

[OpenRouter](https://openrouter.ai/docs/quickstart#using-the-openrouter-api) is a hosted API for hundreds of models behind one endpoint.

- **License and deployment:** Proprietary. Managed by OpenRouter.
- **Does well:** [Automatic model fallbacks](https://openrouter.ai/docs/guides/routing/model-fallbacks#how-it-works), [credit limits per API key](https://openrouter.ai/docs/guides/overview/auth/provisioning-api-keys#use-cases), and one bill across providers. Prompts and completions are [not logged by default](https://openrouter.ai/docs/faq#privacy-and-data-logging).
- **Limitation:** Hosted only. OpenRouter [charges a fee when credits are purchased, and a 5% fee on bring-your-own-key usage above the plan allowance](https://openrouter.ai/docs/faq#pricing-and-fees).
- **Suits:** Small teams that want access to many models quickly through one account.

### Azure API Management

[Azure API Management](https://learn.microsoft.com/en-us/azure/api-management/genai-gateway-capabilities#traffic-mediation-and-control) extends an existing API gateway with AI gateway policies for LLM APIs, MCP servers, and A2A agent APIs.

- **License and deployment:** Proprietary. An Azure service.
- **Does well:** [Token limits per API consumer](https://learn.microsoft.com/en-us/azure/api-management/genai-gateway-capabilities#token-rate-limiting-and-quotas), a [load balancer](https://learn.microsoft.com/en-us/azure/api-management/genai-gateway-capabilities#load-balancer), a [circuit breaker](https://learn.microsoft.com/en-us/azure/api-management/genai-gateway-capabilities#circuit-breaker), and [logging and monitoring](https://learn.microsoft.com/en-us/azure/api-management/genai-gateway-capabilities#observability-and-governance), with backends that include models in Microsoft Foundry and providers such as Amazon Bedrock.
- **Limitation:** [Semantic caching requires Azure Managed Redis or another compatible external cache](https://learn.microsoft.com/en-us/azure/api-management/genai-gateway-capabilities#semantic-caching), and the control plane is tied to Azure.
- **Suits:** Organizations that already standardize on Azure API Management.

### Google Cloud Apigee

[Google Cloud Apigee](https://cloud.google.com/solutions/apigee-ai#:~:text=Multicloud%20model%20routing) is an API management platform that Google Cloud positions as an AI gateway, configured through policies on API proxies.

- **License and deployment:** Proprietary. A Google Cloud service.
- **Does well:** Model abstraction and multicloud model routing, [token limit enforcement](https://cloud.google.com/solutions/apigee-ai#:~:text=Token%20limit%20enforcement), [Model Armor integration](https://cloud.google.com/solutions/apigee-ai#:~:text=Model%20Armor%20integration) for prompt and response sanitization, and token-based usage dashboards.
- **Limitation:** Google publishes the [circuit breaker](https://github.com/GoogleCloudPlatform/apigee-samples/tree/main/llm-circuit-breaking) and [semantic cache](https://github.com/GoogleCloudPlatform/apigee-samples/tree/main/llm-semantic-cache) as samples, so teams build and maintain that proxy logic themselves.
- **Suits:** Google Cloud teams that already use Apigee and want LLM traffic under the same API program.

## How to choose an AI gateway

Choose an AI gateway by where prompts and logs must stay, which traffic it needs to govern, and what you already operate. Start from the situation closest to yours, then test the candidates with your own traffic.

| Situation | Candidates |
|---|---|
| Prompts and logs must stay inside your network | Bifrost, LiteLLM, agentgateway, Agent Router, New API |
| One gateway for model, MCP, and A2A traffic | Bifrost, LiteLLM, agentgateway, Kong AI Gateway, Azure API Management |
| Widest provider list from a Python stack | LiteLLM |
| Extending an API gateway you already run | Kong AI Gateway, Apache APISIX, Higress, Azure API Management, Google Cloud Apigee |
| Kubernetes, Envoy, and self-hosted inference | Agent Router, agentgateway |
| No gateway infrastructure to operate | Cloudflare AI Gateway, Vercel AI Gateway, OpenRouter |

Published latency figures come from each project's own tests, use different setups, and are not comparable. Load test with your own prompts and providers at the request rate you expect, and force an upstream failure to confirm that failover works. The [AI gateway evaluation checklist](https://github.com/ai-gateways/ai-gateway#how-to-evaluate-an-ai-gateway) lists what else to check.

## What this list leaves out

This list covers gateways that meet every test above, so several useful categories are out of scope. Each has a better home elsewhere in this organization.

- **Free-tier aggregators.** Tools for pooling personal free tiers and subscriptions serve individual developers. [Awesome Free AI Providers](https://github.com/ai-gateways/awesome-free-ai-providers#free-tiers) lists the free tiers themselves.
- **Platform-bound gateways.** Gateways usable only from one vendor's data or hosting platform are in [Cloud and Platform AI Gateways](https://github.com/ai-gateways/awesome-ai-gateways#cloud-and-platform-ai-gateways).
- **Model routers and inference gateways.** Tools that pick a model per request or balance self-hosted model servers are in [Model Routers and Aggregators](https://github.com/ai-gateways/awesome-ai-gateways#model-routers-and-aggregators) and [Inference Gateways](https://github.com/ai-gateways/awesome-ai-gateways#inference-gateways).
- **Smaller or sales-led products.** Open-source projects below the adoption bar and closed products without self-serve access are in [AI Gateways](https://github.com/ai-gateways/awesome-ai-gateways#ai-gateways) and [API Gateways with AI Features](https://github.com/ai-gateways/awesome-ai-gateways#api-gateways-with-ai-features).

## Related guides

- [The three kinds of AI traffic](https://github.com/ai-gateways/ai-gateway#the-three-kinds-of-ai-traffic): how LLM, MCP, and agent gateways fit under one AI gateway
- [How to evaluate an LLM gateway](https://github.com/ai-gateways/llm-gateway#how-to-evaluate-an-llm-gateway): routing, budgets, and failover checks for model traffic
- [Best MCP Gateways](https://github.com/ai-gateways/best-mcp-gateways#best-open-source-mcp-gateways): the same selective treatment for MCP gateways
- [Best Agent Gateways](https://github.com/ai-gateways/best-agent-gateways#best-open-source-agent-gateways): the same selective treatment for agent gateways
- [Cost governance](https://github.com/ai-gateways/ai-governance#cost-governance): budgets and attribution for AI spend
- [Where to enforce guardrails](https://github.com/ai-gateways/ai-guardrails#where-to-enforce-guardrails): checks at the gateway and elsewhere
- [OpenTelemetry for LLM applications](https://github.com/ai-gateways/llm-observability#opentelemetry-for-llm-applications): tracing model calls through a gateway
- [Awesome AI Gateways](https://github.com/ai-gateways/awesome-ai-gateways#contents): the full catalog of LLM, MCP, and agent gateways
