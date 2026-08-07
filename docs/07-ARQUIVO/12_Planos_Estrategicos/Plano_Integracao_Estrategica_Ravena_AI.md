# Plano de Integração Estratégica: Ravena AI Core Infrastructure

## 1. Visão Geral
Este plano detalha a estratégia de integração e refatoração para a **Ravena AI**, focando na evolução da arquitetura para a pasta `ravana ai core infrastructure`. O objetivo não é uma simples migração de código legado, mas a extração de valor estratégico, refatoração de componentes críticos e a integração de ferramentas auxiliares para maximizar a robustez, observabilidade e segurança do ecossistema.

## 2. Pilares da Integração
A estratégia baseia-se em três pilares fundamentais derivados da análise das versões V2.x e V3.0.0:

| Pilar | Foco | Objetivo |
| :--- | :--- | :--- |
| **Refatoração Cognitiva** | RAG & Busca 360 | Consolidar o "Cérebro Profundo" com persistência em SQLite/ChromaDB. |
| **Observabilidade de Elite** | Dashboard & Métricas | Reintegrar a visualização em tempo real e percepção visual (Vision Module). |
| **Blindagem de Execução** | Risco & Auditoria | Fortalecer o Protocolo Zero Trust e a Blindagem de Capital (2%). |

---

## 3. Plano de Ação por Módulos

### 3.1. Núcleo de Inteligência (IA, RAG e Visão)
*Localização: `04_IA_RAG_e_Visao`*

*   **Refatoração do RAG:** Migrar a lógica de expansão do RAG da V2.0.4 para a estrutura atual, garantindo que o `winning_patterns.json` seja alimentado dinamicamente por buscas semânticas.
*   **Integração do Vision Module:** Reativar o `active_vision.py` com suporte a YOLOv8 para validação visual de sinais, integrando-o ao fluxo de decisão do `signal_bridge.py`.
*   **Mapeamento de Skills via MCP:** Utilizar o `mcp_mapper.py` para catalogar ferramentas externas (APIs de sentimento, calculadoras matemáticas) e disponibilizá-las para os modelos Qwen 3.5 e Kimi K2.5 na OCI.

### 3.2. Módulo de Trading e Execução
*Localização: `07_Trading_Bot_Module`*

*   **Otimização da Ponte de Dados:** Refatorar o `signal_bridge.py` para atuar como um orquestrador de baixa latência, conectando o Agente de Busca 360 ao Day Trade Agent com validação de suitability em tempo real.
*   **Sincronização com Laboratório IQ Option:** Implementar o loop de feedback onde o `audit_engine.py` extrai padrões de sucesso do ambiente de teste para atualizar o "Limiar de Brutalidade" (91.24%) no capital real.
*   **Fallback de Soberania Omega:** Garantir que o `click_emulator.py` esteja pronto para assumir a execução caso a latência da API Bybit exceda 800ms.

### 3.3. Cibersegurança e Blindagem
*Localização: `02_Ciberseguranca_e_Blindagem`*

*   **Juiz Universal (Auditor):** Integrar o `audit_engine.py` como o "Juiz Universal", realizando auditorias de segurança em cada pacote de sinal gerado.
*   **Blindagem de Capital Real:** Aplicar rigorosamente o limite de 2% de alocação e 5% de drawdown através do `risk_manager.py`, bloqueando ordens que não possuam assinatura de conformidade.

### 3.4. Utilitários e Observabilidade
*Localização: `98_Utilitarios_e_Ferramentas`*

*   **Dashboard de Performance:** Refatorar o `dashboard_integration.py` para consumir dados do `metrics_exporter.py` e fornecer uma interface React/Tailwind para monitoramento de saúde do sistema e performance de trades.
*   **Health Monitor:** Centralizar os logs de todos os módulos no `health_monitor.py` para garantir 99.9% de uptime e auto-recuperação (Self-Healing).

---

## 4. Cronograma de Implementação (Fases)

1.  **Fase 1: Harmonização de Dados (Semana 1):** Configuração do RAG persistente e mapeamento de skills MCP.
2.  **Fase 2: Ativação da Percepção (Semana 2):** Integração da Visão Ativa e Dashboard de Monitoramento.
3.  **Fase 3: Blindagem Total (Semana 3):** Implementação final do Protocolo Zero Trust e testes de estresse na Ponte de Sinais.
4.  **Fase 4: Ativação em Produção (Semana 4):** Lançamento da V3.1.0 com feedback loop entre Laboratório e Capital Real.

---

## 5. Conclusão
Este plano transforma a Ravena AI em um ecossistema resiliente e autônomo. A integração estratégica das ferramentas auxiliares e a refatoração dos módulos legados garantem que a versão 3.1.0 seja a mais segura e eficiente até o momento, pronta para operar em infraestrutura de elite na OCI.
