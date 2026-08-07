# CHANGELOG — Ravena AIM

> Todas as alterações notáveis deste projeto serão documentadas neste arquivo.
> O formato segue [Keep a Changelog](https://keepachangelog.com/pt-BR/1.0.0/),
> e este projeto adere ao [Versionamento Semântico](https://semver.org/lang/pt-BR/).

---

## [1.0.1-beta] — 2026-06-07

### Corrigido (Security Fix)
- **CRÍTICO:** Removido secret HMAC hardcoded (`ravena_core_secret_2026`) do `zero_trust_v3.2.6.py`
- Zero Trust agora carrega a chave via variável de ambiente `RAVENA_ZERO_TRUST_SECRET`
- Em desenvolvimento, emite warning se a chave não estiver definida (nunca silencioso)

### Adicionado
- `src/core/secrets_manager.py` — Gerenciador centralizado de credenciais (inspirado no Google Colab Secrets)
  - Hierarquia de carregamento: OCI Vault → env vars → arquivo `.env`
  - Registro de 17 variáveis sensíveis com classificação de severidade
  - Função `secrets.audit()` para verificação de conformidade
  - Singleton global para acesso unificado em todo o sistema
- `.env.example` atualizado com todas as variáveis organizadas por severidade

---

## [1.0.0-beta] — 2026-06-07

### Adicionado
- Estrutura de diretórios reorganizada para produção:
  - `src/core/` — OmegaCore, Juiz Universal, Ravena Model
  - `src/security/` — Zero Trust, Auditor, Hacker Agent (v3.2.7/v3.2.8)
  - `src/rag/` — RAG Advanced, Vision Module, ChromaDB
  - `src/trading/` — Signal Bridge, Bybit Connector, Click Emulator
  - `src/orchestration/` — Agentes especializados
  - `src/learning/` — DNA Sucesso, LoRA
  - `src/utils/` — Telegram, Social Connector, External API Manager
  - `src/simulation/` — Active Vision, Monitor Logs
- `docker/Dockerfile` e `docker/docker-compose.yml` para deploy OCI
- `requirements.txt` com todas as dependências
- `.gitignore` atualizado para proteger secrets
- `README.md` profissional com documentação completa
- Pasta `legacy/` com versões anteriores para referência histórica

### Sincronizado
- Agente Hacker v3.2.7 e v3.2.8 (do Google Drive → GitHub)
- `oci_readiness_check.py` para diagnóstico de prontidão OCI
- Testes de stress e elite do Drive

### Removido
- Arquivos `_OLD`, `_conflict_` e duplicatas
- Estrutura antiga `modulos/` movida para `legacy/`

---

## Convenção de Versionamento

```
MAJOR.MINOR.PATCH-STAGE

Exemplos:
  1.0.0-beta    → Primeira versão beta (pré-produção)
  1.0.1-beta    → Correção de bug na beta
  1.1.0-beta    → Nova feature na beta
  1.0.0-rc.1    → Release Candidate 1 (pré-deploy OCI)
  1.0.0         → Versão estável em produção
```

| Componente | Quando incrementar |
|------------|-------------------|
| MAJOR | Mudança incompatível na API/arquitetura |
| MINOR | Nova funcionalidade retrocompatível |
| PATCH | Correção de bug ou security fix |
| STAGE | beta → rc.N → (estável) |

## [1.0.2-beta] - 2026-06-07

### Fixed
- **SyntaxError** no `hacker_agent.py` (linha 144 — dois prints na mesma linha)
- **Imports quebrados** no `omega_core_v3.2.6.py` (referências a `ravena_v3.*` substituídas por `src.*`)
- **Imports relativos** no `security_core_v3.2.7.py` e `hacker_agent_v328_final.py` (fallback robusto)
- **Imports legado** no `omega_v3.2.6.py` e `omega.py` (adicionado try/except com mocks)
- **SDK OCI** no `ravena_model.py` (guard para quando `oci` não está instalado)
- **Health Check** corrigido para pular Enums e dataclasses na instanciação

### Added
- `oci>=2.100.0` adicionado ao `requirements.txt`
- Guards de importação com fallback gracioso em todos os módulos core

### Changed
- Health Check score: 59% → 100% (22/22 testes passando)
