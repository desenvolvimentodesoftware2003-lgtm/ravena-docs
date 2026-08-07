# Documento Mestre de Arquitetura Ravena AI Consolidado — V3.2.1

Este documento serve como a fonte canônica de verdade para a arquitetura da Ravena AI, integrando componentes cognitivos, de segurança e de execução de trading de elite.

## 1. Núcleo Cognitivo e Orquestração (Omega Core)
O núcleo da Ravena AI, denominado **Omega Core**, é responsável pela orquestração de todos os subagentes e pela manutenção do estado cognitivo global.

*   **RavenaChatAgent:** Interface de diálogo cognitivo de alto nível, permitindo interações fluidas e profundas (estilo ChatGPT) com roteamento inteligente de intenções para agentes especialistas.
*   **Context Persistence:** Sistema de memória de longo prazo que garante a continuidade das conversas e o aprendizado evolutivo.

## 2. Camada de Trading de Elite (Filtro de Brutalidade)
A funcionalidade de trading da Ravena AI foi elevada ao patamar de elite através da integração de simulações paralelas massivas.

*   **Filtro de 60 Agentes de Simulação:** Cada sinal de trading recebido é submetido a 60 agentes de simulação independentes (`SimulacaoFilter`) que operam em cenários variados (Bullish, Bearish, Black Swan, etc.).
*   **TradeBrain Analítico:** O cérebro de decisão final que consolida os resultados das simulações.
*   **Limiar de Brutalidade (96.99%):** A Ravena AI só autoriza a execução de ordens se a probabilidade final de sucesso, combinada com o score de "brutalidade" das simulações, atingir o limiar crítico de **96.99%**. Sinais abaixo deste valor são sumariamente descartados.

## 3. Percepção e Recuperação de Informação (RAG)
*   **VisionRAGSemantic:** Componente avançado de fusão visual-semântica, permitindo que a Ravena interprete dados visuais (gráficos, prints, diagramas) e os correlacione com sua base de conhecimento semântico.
*   **Mass Ingestion:** Capacidade de processar grandes volumes de documentos técnicos para atualização contínua do conhecimento da Ravena.

## 4. Segurança e Blindagem (Auditor AST)
A integridade da Ravena AI é protegida por uma camada de segurança de "Confiança Zero" (Zero Trust).

*   **Auditor AST & Sandbox:** Realiza a análise estática de código (Abstract Syntax Tree) em tempo real de qualquer script gerado ou recebido, executando-o em um ambiente de sandbox isolado antes da integração final para evitar injeções maliciosas ou falhas lógicas.
*   **Security Core:** Monitoramento contínuo de vulnerabilidades e conformidade com padrões de segurança cibernética.

## 5. Estrutura de Subagentes Especializados
A Ravena delega tarefas complexas para um repositório de subagentes altamente especializados em domínios como:
*   Frontend (React/Vite/Tailwind)
*   Backend (FastAPI/Python)
*   Segurança e DevOps
*   Marketing e Design (Vibecodings Framework)

## 6. Conclusão e Governança
A arquitetura V3.2.1 da Ravena AI é autossustentável e modular, projetada para escalabilidade extrema e precisão brutal em ambientes de alta volatilidade.
