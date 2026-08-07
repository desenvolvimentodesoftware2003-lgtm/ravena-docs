# Guia de SeguranÃ§a: ProteÃ§Ã£o de APIs e Tokens (Lockdown V2.2)

**Projeto:** Ravena Modular  
**Data:** 05 de Abril de 2026  
**Status:** **ATIVO**  

---

## ðŸ›¡ï¸ 1. O que Ã© a ProteÃ§Ã£o de Tokens?

Na arquitetura **Ravena Modular**, o mÃ³dulo **Juiz Universal** atua como um firewall de inteligÃªncia. Ele monitora todas as entradas e saÃ­das do sistema para evitar o vazamento acidental ou malicioso de credenciais sensÃ­veis (Tokens e API Keys).

---

## ðŸ” 2. Como o Sistema Protege VocÃª?

O **Protocolo Lockdown V2.2** utiliza padrÃµes de reconhecimento (Regex) para identificar e bloquear instantaneamente:

| Tipo de Credencial | PadrÃ£o Identificado | AÃ§Ã£o |
| :--- | :--- | :--- |
| **OpenAI (sk-...)** | Chaves de API da OpenAI | **BLOQUEIO IMEDIATO** |
| **Telegram Bot Token** | Tokens do BotFather | **BLOQUEIO IMEDIATO** |
| **GitHub (ghp_...)** | Tokens de Acesso Pessoal | **BLOQUEIO IMEDIATO** |
| **Google Cloud (AIza...)** | Chaves de API do Google | **BLOQUEIO IMEDIATO** |

---

## âš¡ 3. DemonstraÃ§Ã£o de Bloqueio em Tempo Real

Durante os testes de estresse, o sistema validou os seguintes bloqueios:

- **Tentativa:** "Meu token Ã© sk-abcdef..."
- **Resultado:** `[JUIZ_UNIVERSAL] BLOQUEADO: PadrÃ£o malicioso detectado (api_token_protection)`

---

## ðŸ’¡ 4. Boas PrÃ¡ticas Recomendadas

Para manter sua arquitetura Ravena segura, siga estas diretrizes:

1. **Nunca escreva Tokens no cÃ³digo:** Use variÃ¡veis de ambiente (`os.environ.get`).
2. **Use o arquivo `.env`:** Armazene segredos localmente e adicione `.env` ao seu `.gitignore`.
3. **Auditoria Ativa:** O Juiz Universal registra todas as tentativas de vazamento no log de auditoria.
4. **RotaÃ§Ã£o de Chaves:** Se um token for detectado pelo Juiz, considere-o comprometido e gere um novo.

---

**Assinado:** Manus AI  
**Sistema:** Ravena Modular V1.8.1-SECURITY-ENHANCED
