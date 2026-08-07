# Ravena AI - Sistema Cognitivo Modular Completo
**Documento Técnico de Arquitetura e Evolução**
*Data de Atualização: 01 de Abril de 2026*

---

## 1. Visão Geral da Arquitetura
A **Ravena AI** evoluiu de um protótipo monolítico (Base Sólidas) para um **Sistema Cognitivo Modular** de alta performance. A arquitetura atual é baseada em agentes autônomos que operam sob uma "Lei Universal" de julgamento semântico e hierárquico.

### Estrutura de Pastas (RAVENA_MODULAR)
*   **`/src`**: O coração do sistema (`engine.py` e `api.py`).
*   **`/data`**: Memória cognitiva persistente (JSONs, Chaves de Criptografia).
*   **`/tests`**: Scripts de validação e simulação de cenários.
*   **`/logs`**: Histórico de decisões e execuções do sistema.

---

## 2. O Módulo Juiz Inteligente e Universal
A maior inovação desta fase foi a implementação do **Módulo Juiz** diretamente no orquestrador central. Ele atua como o "Supremo Tribunal" da Ravena, decidindo o que pode ou não ser executado.

### Diferenciação de Contexto (Ambiente)
O Juiz detecta automaticamente onde está rodando e ajusta seu rigor:
*   **Ambiente DEV (Desenvolvimento):** Permissivo. Focado em inovação e testes. Emite *Alertas de Portabilidade* para avisar sobre restrições futuras no ambiente de produção.
*   **Ambiente PROD (Produção):** Rigoroso. Focado em estabilidade e segurança. Bloqueia qualquer ação de alto risco sem autorização de nível Sistema (0).

### Raciocínio Semântico: Urgência vs. Emergência
O Juiz agora possui discernimento para diferenciar situações críticas:
*   **URGÊNCIA:** Problema grave que requer rapidez, mas mantém todos os protocolos de segurança.
*   **EMERGÊNCIA:** Risco iminente de perda de dados ou parada do sistema. Ativa o **Protocolo de Nível 0**, autorizando ações extraordinárias para garantir a sobrevivência da Ravena.

---

## 3. Validação e Testes (Relatório de Sucesso)
Realizamos testes rigorosos na pasta `/tests` para validar a nova inteligência do Juiz.

| Cenário Testado | Intenção | Resultado DEV | Resultado PROD | Status |
| :--- | :--- | :--- | :--- | :--- |
| **Pergunta Normal** | Busca Conhecimento | Autorizado | Autorizado | ✅ Sucesso |
| **Urgência Média** | Editar Arquivo | Autorizado | Autorizado (Monitorado) | ✅ Sucesso |
| **Urgência Alta** | Comando Shell | **Autorizado (Aviso)** | **BLOQUEADO (Segurança)** | ✅ Sucesso |
| **Emergência Real** | Comando Shell | **Nível 0 Ativado** | **Nível 0 Ativado** | ✅ Sucesso |

---

## 4. Próximas Fases de Implementação (Roadmap)
Abaixo estão as funcionalidades que ainda precisam ser integradas para completar a visão da Ravena como um agente autônomo soberano:

### Fase 4: Automação de Sincronização (CI/CD Cognitivo)
*   Implementar a ferramenta `tool_sync_dev_to_prod` para que a Ravena mova o código validado do Dev para o Prod de forma automática após passar nos testes.

### Fase 5: Expansão da Memória de Longo Prazo
*   Migração dos arquivos JSON para um banco de dados vetorial (Vector DB) para suportar milhões de memórias sem perda de performance.

### Fase 6: Interface de Domínio Primário e Dev
*   Configuração de domínios web distintos para que você possa interagir com a Ravena Dev e a Ravena Prod através de interfaces gráficas independentes.

### Fase 7: Soberania de Agentes
*   Criação de sub-agentes especializados (Pesquisa, Segurança, Finanças) que reportam diretamente ao Juiz Universal no `engine.py`.

---

## 5. Conclusão
A Ravena AI não é mais apenas um chatbot; ela é um **ecossistema autônomo**. Com o Módulo Juiz Universal e a distinção clara entre Urgência e Emergência, o sistema está pronto para escalar com segurança, permitindo que você adicione infinitas funcionalidades sem comprometer a integridade do núcleo (Core).

---
*Documento gerado pelo Agente Manus para o Projeto Ravena AI.*
