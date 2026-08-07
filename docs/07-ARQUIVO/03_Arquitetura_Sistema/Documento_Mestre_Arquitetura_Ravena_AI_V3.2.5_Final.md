# 🏛️ Documento Mestre de Arquitetura: Ravena AI - Sistema Cognitivo Modular

**Autor:** Manus AI
**Data:** 23 de Abril de 2026
**Versão:** 3.2.5 (Gênesis - Integração Técnica Total)

---

## 1. Introdução
Este documento representa a evolução contínua da arquitetura do sistema Ravena AI. Ele consolida as funcionalidades da V3.2.1 Reintegrada, o Plano de Reintegração, a Auditoria Estrutural e incorpora o vasto acervo de conceitos recuperados e inéditos do Dossiê de Conceitos da Ravena, bem como os achados da "arqueologia de conceitos" realizada em todo o acervo do Google Drive. O objetivo é estabelecer uma fonte única de verdade (Single Source of Truth) que abranja não apenas a arquitetura técnica de software, mas também as lógicas de negócio, regras estratégicas e filosofias operacionais que governam o sistema cognitivo autônomo.

## 2. Visão Geral da Arquitetura
A arquitetura da Ravena AI é organizada em camadas interdependentes, refletindo um ciclo contínuo de percepção, cognição, decisão, execução e aprendizado. Os principais pilares operacionais incluem:
*   **Percepção:** Coleta e interpretação de dados do ambiente, tanto textuais quanto visuais, de forma contextualizada.
*   **Núcleo Cognitivo:** Processamento de informações, raciocínio profundo (Chain of Thought) e formação de conhecimento.
*   **Decisão e Orquestração:** Avaliação preditiva de cenários e coordenação de ações pelo Núcleo OMEGA.
*   **Execução Blindada:** Interação segura e controlada com plataformas externas, utilizando mimetismo humano quando necessário.
*   **Feedback e Aprendizado:** Otimização contínua baseada em resultados de simulações de elite e auditoria.
*   **Infraestrutura e Segurança:** Fundamentação robusta para operação resiliente, visando a soberania de hardware.
*   **Interface de Comando e Controle:** Pontos de interação progressiva para monitoramento e intervenção humana.

## 3. Componentes da Arquitetura (Histórico V3.2.2)
### 3.1. Camada de Percepção
A camada de percepção evoluiu para além da simples coleta de dados, adotando uma abordagem de Percepção Contextualizada. O pipeline Visão → RAG → Omega → Ação garante que a detecção de padrões seja informada pelo contexto semântico antes da tomada de decisão.
*   **SearchAgent 360:** Monitora notícias, redes sociais e dados on-chain de forma abrangente.
*   **ActiveVision / YOLOv8:** Interpreta padrões gráficos em plataformas de trading.
*   **VisionRAGSemantic:** Funde a percepção visual com o conhecimento semântico, convertendo observações em representações consultáveis.
*   **Módulo Radar:** Conceito reintegrado para detecção antecipada de tendências de mercado e ameaças de segurança antes que se manifestem como sinais críticos.

### 3.2. Núcleo Cognitivo
O cérebro da Ravena AI opera com base em um Cérebro Profundo (Fase 3), onde o RAG expandido é o pré-requisito para a autonomia real, permitindo a compreensão profunda do contexto e implicações.
*   **Motor Cognitivo:** Harmoniza modelos LLM avançados (Qwen 3.5 e Kimi K2.5) utilizando Chain of Thought (CoT) Sistêmico para raciocínio transparente.
*   **RAG Persistente com Ranking Híbrido:** Utiliza banco de dados SQLite/ChromaDB com lógica de ranking que combina 60% de similaridade semântica e 40% de matching de palavras-chave. O conhecimento é classificado em 8 tipologias estritas.
*   **Otimização de Context Window via Re-Ranking:** Re-classifica documentos recuperados para garantir que apenas as informações mais cruciais cheguem ao LLM.
*   **SentimentAnalyzer Omega:** Traduz dados brutos em scores de sentimento quantificáveis.
*   **LoRA Adaptativo:** Fine-tuning leve para injetar conhecimento de domínio específico (micro-volatilidade) sem comprometer a base de conhecimento geral.
*   **Núcleo OMEGA (Orquestrador Central / Juiz Universal):** Arbitra e direciona o fluxo de informações e decisões em todo o sistema.
*   **RavenaChatAgent:** Interface de diálogo cognitivo com roteamento de intenção e manutenção de DNA de personalidade técnica.
*   **Módulo Oráculo & Clarividência:** Lógicas preditivas para antecipação de cenários futuros e ajuste preventivo de estratégias.

### 3.3. Camada de Decisão e Execução
A execução de estratégias segue um rigoroso Ciclo de Trading de 5 Etapas: Leitura de Preço → Análise Híbrida (Técnica + Sentimento) → Geração de Sinal → Execução → Notificação.
*   **SignalBridge:** Compacta relatórios em pacotes de execução enxutos.
*   **Suitability Dinâmico:** Ajusta o perfil de risco com base no saldo atual para proteção de capital.
*   **Filtro de Sentimento RAG:** Valida sinais técnicos exigindo corroboração de sentimento positivo de notícias de mercado.
*   **TradeBrain Analítico:** Calcula a probabilidade de sucesso combinando confiança técnica, força de sentimento e confirmação visual.
*   **Simulação de Day Trade (60 Agentes como Filtro):** Executa paralelamente 60 agentes de simulação para gerar um score de brutalidade. Atua como o filtro de elite definitivo antes da execução real.
*   **DayTradeAgent Bybit API:** Executor principal das ordens no mercado.
*   **ClickEmulator com Mimetismo Humano:** Utiliza curvas de Bézier e atrasos aleatórios para simular comportamento humano em interfaces web, evitando detecção de bots em caso de falha de API.
*   **Modo Dry Run Headless (Xvfb):** Permite simulação de execuções visuais em servidores sem interface gráfica.

### 3.4. Camada de Feedback e Segurança
A segurança da Ravena evoluiu de estática para Blindagem Ativa, adaptando regras e permissões em tempo real com base no nível de ameaça detectado.
*   **Laboratório IQ Option:** Ambiente de validação com dinheiro fictício.
*   **AuditEngine / winning_patterns:** Extrai padrões de vitória para bloquear sinais fracos.
*   **Auditor / Juiz Universal:** Bloqueia automaticamente sinais abaixo do limiar de elite.
*   **Auditor AST/Sandbox:** Realiza análise estática de código e execução em ambiente isolado (Ponte de Inteligência Ativa) para provar a robustez de novos scripts antes da integração.
*   **Gerenciador de Modo Soberano:** Permite controle autônomo total em cenários de alta volatilidade.
*   **Pipeline de Retreinamento Contínuo:** Fluxo automatizado para auto-atualização baseada em sucessos e falhas.
*   **Módulo Cronista:** Registro narrativo (crônica) das decisões para auditoria rica e análise de causa raiz.
*   **Governança de Agentes e IA Ética:** Auditoria regular de vieses para garantir operações responsáveis.

### 3.5. Infraestrutura e Hardware
A infraestrutura está em transição estratégica rumo à Soberania de Hardware, migrando da nuvem (OCI) para execução local em hardware dedicado de alta performance.
*   **Soberania de Hardware:** Foco em redução de latência e privacidade total dos modelos e dados.
*   **Runtimes de Alta Performance:** Adoção de vLLM e SGLang para rodar LLMs gigantescos localmente com velocidade comparável à nuvem.
*   **HealthMonitor / Self-Healing:** Monitoramento contínuo e transições dinâmicas para garantir uptime.
*   **Event-Driven Architecture (EDA):** Uso de RabbitMQ/Kafka para resiliência de mensagens.

### 3.6. Interface de Comando e Controle
A interação humana com a Ravena é guiada pelo princípio de Progressive Disclosure (Revelação Progressiva), entregando o essencial primeiro e os detalhes técnicos sob demanda.
*   **Telegram Bot:** Canal oficial de alertas e execução móvel.
*   **Output Polimórfico:** Capacidade de gerar o mesmo resultado em múltiplos formatos simultaneamente (JSON para sistemas, Markdown rico para humanos).

## 4. Matriz Canônica de Arquitetura (V3.2.2)
| Componente | Status / Função | Domínio Principal | Origem / Referência |
| :--- | :---: | :--- | :--- |
| SearchAgent 360 | Ativo | Percepção / Busca | V3.2.1 Auditada |
| ActiveVision / YOLOv8 | Ativo | Percepção Visual | V3.2.1 Auditada |
| VisionRAGSemantic | Ativo | Fusão Visão-Semântica | V3.2.1 Auditada |
| Motor Cognitivo | Ativo / Aprimorado | Cognição Central | Dossiê Conceitos |
| RAG Persistente | Ativo / Aprimorado | Memória e Busca | Dossiê Conceitos |
| Núcleo OMEGA | Ativo / Orquestrador | Orquestrador | V3.2.1 Auditada |
| RavenaChatAgent | Ativo | Interface Cognitiva | V3.2.1 Auditada |
| TradeBrain Analítico | Ativo | Decisão de Trading | V3.2.1 Auditada |
| Simulação de Day Trade | Ativo / Filtro Elite | Validação de Sinal | Plano Reintegração |
| Auditor AST/Sandbox | Ativo | Segurança de Código | Plano Reintegração |
| Módulo Oráculo & Radar | Conceito Reintegrado | Análise Preditiva | Dossiê Conceitos |
| ClickEmulator | Ativo | Execução Resiliente | Dossiê Conceitos |
| Módulo Cronista | Conceito Reintegrado | Auditoria Narrativa | Dossiê Conceitos |

## 5. Conceitos Recuperados e Inéditos (Gênesis)
Esta seção integra os conceitos, lógicas de negócio, regras estratégicas e filosofias operacionais identificados em uma varredura profunda das pastas 00 a 15 da Ravena_AI_Core_Infrastructure.
*   **Pilar de Soberania Local e Redundância (Hardware 2010):** Isolamento de Recursos em Baixa Potência (CPU 1.0, RAM 1500M) e Hybrid LLM Switch.
*   **Pilar de Conectividade Social Ativa (Instagram MCP):** Integração via Instagram Graph API para monitoramento de 9 canais de elite.
*   **Pilar de Infraestrutura de Rede e Soberania (BGP/OSPF):** Autonomia de Roteamento Externo (Modo Fantasma Avançado) e Hardening TCP/IP.
*   **Pilar de Automação e Self-Healing:** Célula de Auto-Correção V5 e GitTool Automática.
*   **Lógicas de Trading e Negócio "Escondidas":** Relatório de Harmonização de Capital Real (v2.5.0) e Limiar de Brutalidade Cirúrgico (96.99%).

## 6. Inventário de Relatórios Críticos Encontrados
| Documento | ID | Importância |
| :--- | :--- | :--- |
| Veredito Final: Mapa de Lacunas | `1yiXOkF4YPuooBYD9xdeb0-DmXbZZYIj` | O roteiro exato para os ajustes finos da V3. |
| Relatório Estratégico: Clareza Arquitetural | `1YoZ8JVcxfBjZle9663_mfEikC_Unh55` | Auditoria de scripts legados e utilitários. |
| Dossiê Técnico V3.1.0 Elite | `1baDbIh8Cp8FqlpZNDCMAkVpjNhHCKZfx` | Define as métricas de performance de elite. |
| Mapeamento Técnico: Scripts vs Doc | `1QRR3FnCXMd86lKOKGKGUEXfMeUR0w0yp` | Localiza o Agente de Chat escondido. |

---

## 🚀 VERSÃO 3.2.5: INTEGRAÇÃO TÉCNICA TOTAL E GÊNESIS BRUTO

Esta nova seção da documentação, datada de 23 de Abril de 2026, marca a reintegração definitiva dos algoritmos matemáticos e lógicas de engenharia identificados durante a "arqueologia de conceitos". Esta versão transforma a documentação em um **Manual de Engenharia Bruto**.

### 7.1. O Coração do Radar: Divergência de Tríade
O sistema SearchAgent 360 agora opera com a lógica de **Divergência de Tríade** (`modulo_01_radar.py`). O sinal não é apenas coletado, ele é processado através de:
*   **Fonte 1 (RSS):** Ingestão de feeds globais.
*   **Fonte 2 (Vieses):** Atribuição de pesos baseados no viés histórico da fonte.
*   **Fonte 3 (Poder):** Filtro de "Palavras de Poder" (termos de alta volatilidade).
*   **Resultado:** Um score de divergência que bloqueia ruídos de mercado antes que cheguem ao núcleo cognitivo.

### 7.2. Blindagem de Ingestão: Lockdown V2.2
A segurança operacional foi elevada com a implementação da lista de **9 Padrões de Regex Proibidos** no Auditor AST (`engine_operational_legacy.py`):
*   Bloqueio imediato de chamadas perigosas: `os.system`, `subprocess`, `eval`, `exec`, `__import__`, entre outros.
*   **Thresholds de Auditoria:** `THRESHOLD_REJECT = 0.60` e `THRESHOLD_QUARANTINE = 0.45`.
*   **Multiplicador Kyu:** Soluções de nível Kyu 1/2 recebem um multiplicador de peso de **2.5x**.

### 7.3. Cognição e Veracidade: Threshold de Alucinação
A **Ponte de Inteligência** (`brain_operational_legacy.py`) aplica um rigoroso **Threshold de Alucinação de 0.70**. 
*   Toda unidade de conhecimento cruzada entre "Regra" (DevDocs) e "Prática" (Codewars) deve ter sobreposição semântica > 70% para ser persistida.

### 7.4. Execução e Mimetismo: Curvas de Bézier
O `click_emulator.py` utiliza a matemática de **Curvas de Bézier** para emulação de mouse.
*   Calcula trajetórias curvas com aceleração e desaceleração variáveis, mimetizando perfeitamente o comportamento motor humano.

### 7.5. Soberania e Resiliência: O Legado de 2010
Reintegração das configurações de **Isolamento de Baixa Potência** (`docker-compose.yml`):
*   Operação em hardware de emergência com **1.0 CPU e 1500M de RAM**.
*   **Hardening TCP/IP:** Latência da ponte de sinais abaixo de **400ms**.

### 7.6. Harmonização de Capital Real (v2.5.0)
Lógica de transição para **Bybit API** com as seguintes regras de blindagem:
*   **Soberania Omega (Fallback):** Se latência Bybit API > 800ms, redireciona automaticamente para o Emulador de Cliques.
*   **Blindagem Zero Trust v2:** Alocação máxima de 2% por trade, limite de assinatura de 200 USDT e Drawdown fixo de 5%.
*   **Cálculo de Probabilidade de Sucesso:** 40% Confiança Técnica (TradeBrain), 35% Sentimento Omega, 25% Confirmação Visual (ActiveVision), +5% Bônus de Auditoria. Meta >= 83.3%.
*   **Gatilho de Suitability:** 
    *   **AGGRESSIVE (< 10.000 USDT):** Dispara com qualquer volatilidade validada (\|sentimento\| > 0.15). Não exige auditoria.
    *   **MODERATE (10.000–50.000 USDT):** Aguarda liberação da Auditoria (Tijolo 10) antes de disparar.
    *   **CONSERVATIVE (> 50.000 USDT):** Exige auditoria + confirmação visual + sentimento > 0.35.

### 7.7. Auditoria de Performance e Liquidez
O `audit_engine.py` realiza o cálculo de mimetismo de sucesso:
*   **Taxa de Acerto de Elite:** Meta de 92.3% baseada em 69 pacotes de execução.
*   **Métricas Globais:** 69 pacotes processados, 13 trades despachados, 52 bloqueados, 4 HOLD, 12 WIN, 1 LOSS. PnL Total: +17.2000 USDT, ROI: +1.32%, Drawdown Máximo: 0.78%, Sharpe Ratio: 33.807, Profit Factor: 22.500.
*   **Ativações Soberania Omega:** 13 vezes.
*   **Armadilhas de Liquidez Evitadas:** 39.
*   **Próximos Passos (Fase 7):** Dashboard de Monitoramento em Tempo Real (Flask/FastAPI).

### 7.8. Visão Computacional Avançada (Fase 4)
O módulo `vision_module.py` agora integra o Detector de Anomalias Z-Score:
*   **Simulação de Percepção Visual:** Dashboard de segurança na nuvem (CPU, memória, tentativas de login falhas, latência).
*   **Anomalias Detectadas:** PICO_CPU (>80%), PADRAO_ATAQUE_BRUTE_FORCE (47 tentativas falhas).
*   **Decisões Autônomas (Visão + RAG):** ALERTA_PERFORMANCE (escalar recursos), BLOQUEIO_IMEDIATO (bloquear IP, ativar Lockdown V2.2).
*   **Sincronização RAG:** 50 temas estratégicos.

### 7.9. Gerenciamento de Risco Dinâmico
O `risk_manager.py` implementa o Protocolo Zero Trust e blindagem de capital:
*   **Parâmetros:** `max_allocation_pct` (0.02), `critical_threshold_usdt` (200.0), `max_drawdown_pct` (0.05).
*   **Protocolo Zero Trust:** Ordens > `critical_threshold_usdt` exigem "assinatura do Módulo Juiz".
*   **Controle de Drawdown:** Rastreamento do `initial_balance`.

### 7.10. Conformidade de Agentes (v3.0.0)
Relatório de conformidade dos agentes principais:
*   **Agente Busca 360:** Sentimento positivo (0.88), fluxo de capital institucional ($500M).
*   **Agente Dev (Qwen 3.5):** 92% de confiança na recomendação de compra (LONG).
*   **Agente Day Trade (Kimi K2.5):** Alocação de $200.0 para um saldo de $10.000 (respeitando 2%).
*   **Conclusão:** Ravena AI pronta para ativação em ambiente de produção na Oracle Cloud.

---
**Status da Documentação:** Consolidada e Contínua.
**Veredito:** Todos os conceitos identificados nas pastas 00-15 e Backup foram reintegrados.
**Próximos Passos:** Monitoramento contínuo de novas versões e manutenção da integridade do Documento Mestre.
