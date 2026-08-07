# FASE 0 — ESTUDO DE ARQUITETURA + TRIAGEM DE REPOSITÓRIOS (Acervo Ravena)

> **Objetivo:** registrar o estudo da arquitetura atual (RV9 + BIOS/RavenaOS + ravena-aim) e aplicar
> uma triagem efetiva nos **146 repositórios do acervo** (repo.docx, Lotes 60–72, itens 2047–2514)
> para determinar **qual repo é ideal de usar** em cada frente do ecossistema Ravena.
>
> **Observação:** este documento **não vai para o Git** — fica somente neste computador (área de
> trabalho). Por isso, todos os nomes de ferramentas vêm **linkados ao repositório oficial ou
> documentação oficial** (open source) para referência direta.

---

## 1. Estudo de Arquitetura (contexto da triagem)

### 1.1 Ravena RV9 — Arch Linux remaster (PC de trading B3)

| Aspecto | Estado |
| :--- | :--- |
| Base | Arch Linux remasterado (isohybrid/MBR, modo DD), RV9 build #6 |
| Hardware real | i7-8665U, 7.7 GiB RAM, **sem GPU** |
| UI | Terminal-only + eDEX-UI (Electron, `/opt/edex-ui`) com widget IA |
| IA local | llama.cpp (`llm`, porta 8080), `ravena-ia`, Qwen 3.6-27B (IQ2_M ~12GB) via swap/mmap |
| Rede | NetworkManager, VPN (WARP+WireGuard, route-switch), kill-switch nftables |
| Ferramentas | tmux, w3m, links, yt-dlp, mpv, ranger, chrony, intel (geopolítica) |

**Necessidades de triagem (RV9):** tuning de kernel/memória/swap, nftables/firewall, hardening de
sistema, monitoramento leve, otimização de inferência local (GGUF/quantização), nenhuma dependência
de GPU ou nuvem.

### 1.2 Ravena OS / BIOS — base `zluo01/edex-ui` (fork Tauri/Solid.js)

| Aspecto | Estado (notebook Colab "bios") |
| :--- | :--- |
| Base | [`zluo01/edex-ui`](https://github.com/zluo01/edex-ui) — eDEX-UI reescrito em **Solid.js + Tauri (Rust)** (original: [GitSquared/edex-ui](https://github.com/GitSquared/edex-ui)) |
| Alvo | Chrome OS (Crostini) / Linux, **x86_64, baseline 2GB RAM** |
| Boot | BIOS simulado 4 fases (POST → Discovery → Security → Transition), ~3.2s, sem interrupção |
| Identidade | Paleta **Celeste Blue #B2FFFF**, fundo Deep Slate #0B0E14, Fira Code, estética "Cyberpunk Sóbrio" |
| Segurança | CSP desativado, filesystem recursivo via `opener`, PTY em Rust com threads dedicadas |
| IA | **Ravena Shield** (NVML `check_ravena_shield_vram`, margem 10% contra OOM) + widget AI Telemetry Bridge |
| Stack frontend | Solid.js, TanStack Query, Xterm.js, Tailwind, Vite |
| Build | `pnpm run build:chromeos` (`--target x86_64-unknown-linux-gnu`, `WEBKIT_DISABLE_DMABUF_RENDERER=1`) |

**Necessidades de triagem (BIOS):** qualquer coisa Solid.js/TanStack/Tailwind (já em uso no fork),
telemetria de GPU/memória, segurança leve de Tauri/Rust, processos de sistema; **descartar** tudo que
seja pesado, Python, ou dependa de Kubernetes/GPU real.

### 1.3 ravena-aim — Sistema Cognitivo Modular de Trading (Python 3.11+)

| Aspecto | Estado |
| :--- | :--- |
| Base | [`ravena-aim`](https://github.com/desenvolvimentodesoftware2003-lgtm/ravena-aim), v3.2.6, 54+ módulos em 8 domínios |
| Camadas | Percepção (signal_bridge, bybit_connector, active_vision) · Cognição (omega_core, rag, trade_brain) · Execução (click_emulator, risk_manager, social_connector) · Governança (security_core, hacker_agent, auditor, zero_trust) |
| Módulos | rag (RAG + visão semântica), vector_store, memory, learning (DNA), orchestration (chat/search/dev agents), security (red team), trading, vision, api server, telegram bot |
| Filosofia | Soberania híbrida: opera local (offline) com LLMs em nuvem quando disponível; deploy OCI via Docker |
| Tooling | pyproject (ruff, pytest), pre-commit, docker-compose |

**Necessidades de triagem (AIM):** agentes/memória/RAG vetorial (FAISS/LanceDB/Mem0/MemGPT/LlamaIndex),
segurança de app (SAST/SCA/secrets), observabilidade, rate limiting de API, otimização de modelos
(vLLM/TensorRT p/ OCI futuro), qualidade de código (Semgrep/Dependabot). Python-first.

---

## 2. Critérios de Triagem

Para cada repo do acervo, classifiquei por **alvo de aplicação** e **prioridade**:

| Sinal | Alvo | Significado |
| :---: | :--- | :--- |
| 🖥 **RV9** | Arch trading PC | Kernel, rede, IA local CPU, terminal |
| 💠 **BIOS** | Ravena OS Alpha (Solid/Tauri, Chrome OS) | Frontend, telemetria, segurança leve |
| 🧠 **AIM** | ravena-aim (Python/OCI) | Agentes, RAG, trading, devsecops |
| ☁ **OCI** | Futuro em nuvem (somente referência) | K8s, data lake, API gateway pesados |

Prioridade: **P0** usar agora · **P1** alta · **P2** média/após base · **P3** referência · **X** duplicado/descartar.

> Os links abaixo apontam para o **repositório oficial** de cada ferramenta (não para as URLs do
> acervo, que eram formatos `github.com/<org>/<repo>-setup` e precisavam de validação). As entradas
> do acervo servem como **índice de tema**; o link oficial é a fonte real de integração.

---

## 3. Matriz de Triagem (146 repos, com links oficiais)

### 3.1 IA — Agentes & RAG (destino: 🧠 AIM, alguns 🖥 RV9)

| Ferramenta (link oficial) | Alvo | Prioridade | Justificativa |
| :--- | :---: | :---: | :--- |
| [FAISS](https://github.com/facebookresearch/faiss) | 🧠 | **P0** | Indexação vetorial leve, ideal p/ vector_store do aim |
| [LanceDB](https://github.com/lancedb/lancedb) | 🧠 | **P0** | Vector store leve/embedded, sem servidor — melhor custo p/ aim |
| [Mem0](https://github.com/mem0ai/mem0) | 🧠 | **P0** | Camada de memória persistente p/ agentes (o aim tem módulo memory) |
| [LlamaIndex](https://github.com/run-llama/llama_index) | 🧠 | **P0** | Busca híbrida p/ o RAG do aim (rag_advanced) |
| [Letta (MemGPT)](https://github.com/letta-ai/letta) | 🧠 | **P1** | Memória hierárquica/paginação de contexto |
| [RedisVL](https://github.com/RedisVentures/redisvl) | 🧠 | **P1** | Busca vetorial em Redis (já tem Redis no sandbox-ravena) |
| [LangGraph](https://github.com/langchain-ai/langgraph) | 🧠 | **P1** | Fluxos em grafo p/ orquestração (omega_core) |
| [CrewAI](https://github.com/crewAIInc/crewAI) | 🧠 | **P1** | Times hierárquicos p/ specialized_agents |
| [AutoGen](https://github.com/microsoft/autogen) | 🧠 | **P2** | Colaboração multi-agente (2 variantes no acervo: usar 1) |
| [DSPy](https://github.com/stanfordnlp/dspy) | 🧠 | **P2** | Otimização programática de prompts |
| [TruLens](https://github.com/truera/trulens) | 🧠 | **P2** | Avaliação de alucinação/RAG |

### 3.2 IA — Modelos & Inferência (destino: 🖥 RV9 CPU + 🧠 AIM/OCI GPU)

| Ferramenta (link oficial) | Alvo | Prioridade | Justificativa |
| :--- | :---: | :---: | :--- |
| [llama.cpp (GGUF)](https://github.com/ggml-org/llama.cpp) | 🖥 | **P0** | JÁ É a stack do RV9 (llm/llama.cpp). Validar versão/quantização |
| [bitsandbytes](https://github.com/bitsandbytes-foundation/bitsandbytes) | 🖥/🧠 | **P0** | 4/8-bit p/ CPU e GPU — casa com a stack atual |
| [AutoAWQ](https://github.com/casper-hansen/AutoAWQ) | 🧠/☁ | **P2** | Compressão p/ GPU — futuro OCI |
| [vLLM](https://github.com/vllm-project/vllm) | 🧠/☁ | **P2** | Servidor de inferência OpenAI-compat p/ OCI futuro |
| [TensorRT-LLM](https://github.com/NVIDIA/TensorRT-LLM) | ☁ | **P3** | Requer GPU NVIDIA — sem aplicação imediata |
| [Unsloth](https://github.com/unslothai/unsloth) | 🧠 | **P2** | Ajuste fino eficiente (treinador do aim) |
| [HuggingFace Optimum](https://github.com/huggingface/optimum) | 🧠 | **P2** | Exportação/otimização p/ hardware |
| [PEFT / LoRA](https://github.com/huggingface/peft) | 🧠 | **P2** | LoRA (2 variantes no acervo: usar 1) |
| [DistilBERT (Transformers)](https://github.com/huggingface/transformers) | 🧠 | **P3** | Destilação clássica, menos prioritária |
| [Triton Inference Server](https://github.com/triton-inference-server/server) | ☁ | **P3** | Servidor multi-framework — só OCI |

### 3.3 Segurança de Aplicação & Containers (destino: 🧠 AIM + 💠 BIOS)

| Ferramenta (link oficial) | Alvo | Prioridade | Justificativa |
| :--- | :---: | :---: | :--- |
| [Semgrep](https://github.com/semgrep/semgrep) | 🧠 | **P0** | Regras custom p/ o código Python do aim (já tem pre-commit) |
| [Dependabot](https://github.com/dependabot) | 🧠 | **P1** | SCA no GitHub do aim (2 variantes no acervo: usar 1) |
| [HashiCorp Vault](https://github.com/hashicorp/vault) | 🧠 | **P1** | O aim tem secrets_manager — padrão Vault p/ produção |
| [Trivy](https://github.com/aquasecurity/trivy) | 🧠/☁ | **P1** | Varredura de imagens Docker (aim vai p/ OCI) |
| [Kubescape](https://github.com/kubescape/kubescape) | ☁ | **P2** | Requer K8s — OCI futuro |
| [Falco](https://github.com/falcosecurity/falco) | ☁ | **P2** | Runtime security em containers |
| [Prowler](https://github.com/prowler-cloud/prowler) | ☁ | **P2** | Auditoria de nuvem — quando subir OCI |
| [ScoutSuite](https://github.com/nccgroup/ScoutSuite) | ☁ | **P2** | Auditoria multicloud OCI |
| [PCI-DSS hardening](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Infrastructure_as_Code_Security_Cheat_Sheet.md) | ☁ | P3 | Sem PCI no escopo atual (referência OWASP) |

### 3.4 Ciberdefesa (destino: 🖥 RV9, seletivo)

| Ferramenta (link oficial) | Alvo | Prioridade | Justificativa |
| :--- | :---: | :---: | :--- |
| [nftables (Netfilter)](https://git.netfilter.org/nftables/) | 🖥 | **P0** | JÁ é o kill-switch do RV9 — validar regras avançadas |
| [Suricata](https://github.com/OISF/suricata) | 🖥 | **P2** | IDS pesado p/ 7.7GB — avaliar recurso |
| [Snort 3](https://github.com/snort3/snort3) | 🖥 | **P2** | Alternativa ao Suricata (2 variantes no acervo: usar 1) |
| [Zeek](https://github.com/zeek/zeek) | 🖥 | **P3** | Telemetria de rede — pesado p/ o PC atual |
| [YARA](https://github.com/VirusTotal/yara) | 🖥/🧠 | **P1** | Varredura de padrões — leve, útil p/ hardening |
| [MISP](https://github.com/MISP/MISP) | 🖥 | P2 | Compartilhamento de IoC (2 variantes no acervo: usar 1) |
| [Volatility3](https://github.com/volatilityfoundation/volatility3) | 🖥 | **P1** | Forense de memória — resposta a incidente |
| [Velociraptor](https://github.com/Velocidex/velociraptor) | 🖥 | P3 | Pesado p/ endpoint |
| [Shuffle (SOAR)](https://github.com/shuffle/shuffle) | 🖥/☁ | **P1** | Playbooks de resposta — leve, útil |
| [Elastic Detection Rules](https://github.com/elastic/detection-rules) | ☁ | P3 | Requer cluster Elastic |
| [ElastAlert](https://github.com/Yelp/elastalert) | ☁ | P3 | Variante Elastic |

### 3.5 Kernel & Sistema Linux (destino: 🖥 RV9 — a frente mais direta)

| Ferramenta (link oficial) | Alvo | Prioridade | Justificativa |
| :--- | :---: | :---: | :--- |
| [Kernel VM tuning (docs vm)](https://docs.kernel.org/admin-guide/sysctl/vm.html) | 🖥 | **P0** | Page cache/swap = base da inferência do Qwen 27B em 7.7GB |
| [Sysctl TCP/IP (docs kernel)](https://docs.kernel.org/networking/ip-sysctl.html) | 🖥 | **P0** | Tuning TCP p/ latência de trading |
| [cgroups v2 (docs kernel)](https://docs.kernel.org/admin-guide/cgroup-v2.html) | 🖥 | **P0** | Isolar CPU/RAM do llama.cpp vs trading |
| [perf (tools/kernel)](https://github.com/torvalds/linux/tree/master/tools/perf) | 🖥 | **P1** | Diagnóstico de gargalos |
| [bpftrace](https://github.com/bpftrace/bpftrace) | 🖥 | **P1** | Profiling leve no kernel |
| [libbpf (eBPF)](https://github.com/libbpf/libbpf) | 🖥 | **P2** | Desenvolvimento eBPF |
| [liburing (io_uring)](https://github.com/axboe/liburing) | 🖥 | **P2** | E/S assíncrona — avançado |
| [audit-userspace (auditd)](https://github.com/linux-audit/audit-userspace) | 🖥 | **P1** | Auditoria de eventos sensíveis |
| [AppArmor](https://gitlab.com/apparmor/apparmor) | 🖥 | **P1** | Blindagem de binários (chrome/electron, llama) |

### 3.6 Frontend (destino: 💠 BIOS/RavenaOS — Solid.js)

| Ferramenta (link oficial) | Alvo | Prioridade | Justificativa |
| :--- | :---: | :---: | :--- |
| [TanStack Query](https://github.com/TanStack/query) | 💠 | **P0** | JÁ é dependência do fork (5.101.2) — usar doc oficial |
| [Tailwind CSS](https://github.com/tailwindlabs/tailwindcss) | 💠 | **P0** | Tailwind já usado no fork (2 variantes no acervo: usar 1) |
| [tailwind-merge](https://github.com/dcastil/tailwind-merge) | 💠 | **P1** | Resolução de conflitos de classes |
| [Lighthouse CI](https://github.com/GoogleChrome/lighthouse-ci) | 💠 | **P1** | CI de performance do dashboard |
| [Zustand](https://github.com/pmndrs/zustand) | 💠 | **P2** | Estado global leve (se adotado) |
| [Valtio](https://github.com/pmndrs/valtio) | 💠 | **P2** | Proxies (alternativa ao Zustand — escolher 1) |
| [Effector](https://github.com/effector/effector) | 💠 | **P3** | Overkill p/ Solid |
| [Redux Toolkit](https://github.com/reduxjs/redux-toolkit) | 💠 | **P3** | React-only — NÃO aplica (fork é Solid.js) |
| [Remix](https://github.com/remix-run/remix) | 💠 | **P3** | React/SSR — NÃO aplica |
| [Next.js](https://github.com/vercel/next.js) | 💠 | **P3** | React/Next — NÃO aplica |
| [Module Federation](https://github.com/module-federation/module-federation-examples) | 💠 | P3 | Sem micro-frontends no escopo |

### 3.7 Backend & APIs (destino: 🧠 AIM, seletivo)

| Ferramenta (link oficial) | Alvo | Prioridade | Justificativa |
| :--- | :---: | :---: | :--- |
| [grpc-gateway](https://github.com/grpc-ecosystem/grpc-gateway) | 🧠 | **P1** | Se o aim expuser gRPC no API server |
| [gRPC (grpc-go)](https://github.com/grpc/grpc-go) | 🧠/☁ | **P1** | mTLS entre microsserviços |
| [Resilience4j](https://github.com/resilience4j/resilience4j) | 🧠 | P3 | Java — NÃO aplica (aim é Python) |
| [Spring Framework (WebFlux)](https://github.com/spring-projects/spring-framework) | 🧠 | P3 | Java/Spring — NÃO aplica |
| [Axon Framework](https://github.com/AxonFramework/AxonFramework) | 🧠 | P3 | Java — NÃO aplica |
| [NestJS CQRS](https://github.com/nestjs/cqrs) | 🧠 | P3 | NestJS — NÃO aplica |
| [Akka](https://github.com/akka/akka) | 🧠 | P3 | Scala — NÃO aplica |
| [Dapr](https://github.com/dapr/dapr) | ☁ | **P2** | Abstraction de pub/sub — OCI futuro |
| [Go Clean Architecture](https://github.com/bxcodec/go-clean-arch) | 🧠 | P2 | Referência de arquitetura (não importa código) |
| [Apache Kafka](https://github.com/apache/kafka) | ☁ | **P3** | Cluster Kafka — sem uso local |
| [Apache Pulsar](https://github.com/apache/pulsar) | ☁ | P3 | Sem uso local |

### 3.8 Banco de Dados (destino: 🧠 AIM/OCI, baixa prioridade local)

| Ferramenta (link oficial) | Alvo | Prioridade | Justificativa |
| :--- | :---: | :---: | :--- |
| [Redis](https://github.com/redis/redis) | 🧠 | **P2** | Redis já usado no sandbox — modo cluster p/ produção |
| [Patroni (PostgreSQL HA)](https://github.com/patroni/patroni) | ☁ | **P2** | HA PostgreSQL no OCI |
| [Apache Cassandra](https://github.com/apache/cassandra) | ☁ | P3 | Sem uso local |
| [ScyllaDB](https://github.com/scylladb/scylladb) | ☁ | P3 | Sem uso local |
| [Couchbase](https://github.com/couchbase/couchbase-lite-core) | ☁ | P3 | Sem uso local (server proprietário) |
| [MongoDB](https://github.com/mongodb/mongo) | ☁ | P3 | Sem uso local |
| [Terraform MongoDB Atlas](https://github.com/mongodb/terraform-provider-mongodbatlas) | ☁ | P3 | Atlas é serviço gerenciado |
| [TiDB](https://github.com/pingcap/tidb) | ☁ | P3 | Sem uso local |
| [Citus](https://github.com/citusdata/citus) | ☁ | P3 | Sem uso local |
| [CockroachDB](https://github.com/cockroachdb/cockroach) | ☁ | P3 | Sem uso local |
| [MySQL Server](https://github.com/mysql/mysql-server) | 🧠 | **P2** | Tuning MySQL (se o aim usar MySQL) |

### 3.9 Dados / Data Lakehouse (destino: ☁ OCI — somente referência)

| Ferramenta (link oficial) | Alvo | Prioridade | Justificativa |
| :--- | :---: | :---: | :--- |
| [MinIO](https://github.com/minio/minio) | ☁ | **P2** | S3 local/híbrido — candidato p/ armazenar modelos |
| [Trino](https://github.com/trinodb/trino) | ☁ | P3 | Motor de consulta federada |
| [Presto](https://github.com/prestodb/presto) | ☁ | P3 | Sem uso |
| [Apache Flink](https://github.com/apache/flink) | ☁ | P3 | Sem uso |
| [dbt Core](https://github.com/dbt-labs/dbt-core) | ☁ | P3 | Lakehouse — fora do escopo atual |
| [Apache Iceberg](https://github.com/apache/iceberg) | ☁ | P3 | Lakehouse — fora do escopo atual |
| [Nessie](https://github.com/projectnessie/nessie) | ☁ | P3 | Lakehouse — fora do escopo atual |
| [Unity Catalog](https://github.com/unitycatalog/unitycatalog) | ☁ | P3 | Lakehouse — fora do escopo atual |
| [Astronomer Cosmos](https://github.com/astronomer/astronomer-cosmos) | ☁ | P3 | Lakehouse — fora do escopo atual |
| Delta Live Tables | ☁ | P3 | Proprietário Databricks — não aplica |

### 3.10 Cloud Native & GitOps (destino: ☁ OCI futuro)

| Ferramenta (link oficial) | Alvo | Prioridade | Justificativa |
| :--- | :---: | :---: | :--- |
| [Traefik](https://github.com/traefik/traefik) | ☁ | **P2** | Ingress leve p/ OCI (2 variantes no acervo: usar 1) |
| [Apache APISIX](https://github.com/apache/apisix) | ☁ | P3 | Alternativa ao Traefik |
| [AWS Load Balancer Controller](https://github.com/kubernetes-sigs/aws-load-balancer-controller) | ☁ | P3 | AWS-only |
| [Argo CD](https://github.com/argoproj/argo-cd) | ☁ | **P2** | GitOps p/ OCI (ApplicationSets) |
| [Argo Rollouts](https://github.com/argoproj/argo-rollouts) | ☁ | **P2** | Canários p/ OCI |
| [Flux2](https://github.com/fluxcd/flux2) | ☁ | P3 | Alternativa ao Argo |
| [Fleet (Rancher)](https://github.com/rancher/fleet) | ☁ | P3 | Multi-cluster |
| [Istio](https://github.com/istio/istio) | ☁ | P3 | Service mesh — overkill |
| [Linkerd](https://github.com/linkerd/linkerd2) | ☁ | P3 | Service mesh — overkill |
| [Rook](https://github.com/rook/rook) | ☁ | P3 | Storage K8s |
| [Cluster API Azure](https://github.com/kubernetes-sigs/cluster-api-provider-azure) | ☁ | P3 | Azure-only |
| [Crossplane](https://github.com/crossplane/crossplane) | ☁ | P3 | IaC — só quando houver OCI |
| [Terramate](https://github.com/terramate-io/terramate) | ☁ | P3 | IaC — só quando houver OCI |
| [Terragrunt](https://github.com/gruntwork-io/terragrunt) | ☁ | P3 | IaC — só quando houver OCI |
| [KCL](https://github.com/kcl-lang/kcl) | ☁ | P3 | IaC — só quando houver OCI |
| [driftctl](https://github.com/snyk/driftctl) | ☁ | P3 | IaC — só quando houver OCI |
| [Terraform](https://github.com/hashicorp/terraform) | ☁ | P3 | IaC — só quando houver OCI |
| [Pulumi](https://github.com/pulumi/pulumi) | ☁ | P3 | IaC alternativo |
| [GitHub Actions Runner](https://github.com/actions/runner) | 🧠 | **P2** | Runners p/ CI do aim (2 variantes no acervo: usar 1) |
| [HashiCorp Nomad](https://github.com/hashicorp/nomad) | 🖥/☁ | **P2** | Orquestração leve já mapeada no acervo (seção 3 do repo.docx) |

### 3.11 API Gateway & Edge (destino: ☁ OCI / 🧠 AIM)

| Ferramenta (link oficial) | Alvo | Prioridade | Justificativa |
| :--- | :---: | :---: | :--- |
| [ModSecurity](https://github.com/owasp-modsecurity/ModSecurity) | 🧠/☁ | **P1** | WAF no Nginx — protege o API server do aim |
| [Kong Gateway](https://github.com/Kong/kong) | 🧠/☁ | **P1** | JWT/rate-limit/bot no gateway (plugins oficiais do Kong) |
| [kong-oidc](https://github.com/Kong/kong-oidc) | 🧠/☁ | **P1** | OIDC centralizado p/ produção (plugin comunidade) |
| [Kong bot-detection](https://github.com/Kong/kong-plugin-bot-detection) | 🧠/☁ | **P2** | Bloqueio de tráfego automatizado |
| [Envoy](https://github.com/envoyproxy/envoy) | ☁ | P3 | Envoy — OCI |
| [Apollo Federation](https://github.com/apollographql/federation) | ☁ | P3 | GraphQL — sem escopo atual |
| [GraphQL Mesh](https://github.com/graphql-hive/graphql-mesh) | ☁ | P3 | GraphQL — sem escopo atual |
| [graphql-depth-limit](https://github.com/stems/graphql-depth-limit) | ☁ | P3 | GraphQL — sem escopo atual |

---

## 4. RESULTADO DA TRIAGEM — Top Picks por Frente

### 🖥 RV9 (Arch trading PC) — P0 para aplicar
1. [Kernel VM tuning](https://docs.kernel.org/admin-guide/sysctl/vm.html) (swap/page cache — roda o Qwen 27B)
2. [Sysctl TCP/IP](https://docs.kernel.org/networking/ip-sysctl.html) + [cgroups v2](https://docs.kernel.org/admin-guide/cgroup-v2.html) (latência de trading + isolar llama.cpp)
3. [nftables](https://git.netfilter.org/nftables/) (evoluir o kill-switch)
4. [llama.cpp/GGUF](https://github.com/ggml-org/llama.cpp) + [bitsandbytes](https://github.com/bitsandbytes-foundation/bitsandbytes) (inferência local)
5. [AppArmor](https://gitlab.com/apparmor/apparmor) / [auditd](https://github.com/linux-audit/audit-userspace) / [perf](https://github.com/torvalds/linux/tree/master/tools/perf)

### 💠 BIOS / Ravena OS Alpha — P0 para aplicar
1. [TanStack Query](https://github.com/TanStack/query) (já no fork — doc oficial)
2. [Tailwind CSS](https://github.com/tailwindlabs/tailwindcss) + [tailwind-merge](https://github.com/dcastil/tailwind-merge) (design system Celeste)
3. [Lighthouse CI](https://github.com/GoogleChrome/lighthouse-ci) (CI do dashboard)
4. [cgroups v2](https://docs.kernel.org/admin-guide/cgroup-v2.html) (baseline 2GB — limitação de recursos)
5. Referência de **Ravena Shield** já implementada (NVML) — não precisa de repo externo

### 🧠 ravena-aim — P0 para aplicar
1. [FAISS](https://github.com/facebookresearch/faiss) / [LanceDB](https://github.com/lancedb/lancedb) / [Mem0](https://github.com/mem0ai/mem0) (vector store + memória)
2. [LlamaIndex](https://github.com/run-llama/llama_index) (RAG híbrido)
3. [Semgrep](https://github.com/semgrep/semgrep) + [Dependabot](https://github.com/dependabot) (devsecops)
4. [Kong Gateway](https://github.com/Kong/kong) (JWT/rate-limit) + [ModSecurity](https://github.com/owasp-modsecurity/ModSecurity) (API server)
5. [GitHub Actions Runner](https://github.com/actions/runner) (CI do aim)

---

## 5. Próximos Passos (após triagem)

1. **Validar URLs do acervo** (formato `github.com/<org>/<repo>-setup`): podem ser fictícios — usar os
   links oficiais desta triagem como fonte real de integração.
2. **Montar o acervo consolidado** (Lote 4+ dos reels) já com as colunas de triagem: `Alvo` e `Prioridade`,
   e a coluna `Link oficial` preenchida.
3. **Aplicar em frentes separadas:** primeiro os P0 do RV9 (kernel/memória), depois BIOS (frontend) e AIM (agentes/RAG).
4. Revisar com o usuário os "X" (variantes duplicadas advanced/expert/setup — manter apenas 1 link por ferramenta).
