# PLANO DE EXECUÇÃO — ACERVO TÉCNICO RAVENA (Consolidação de Reels + Repositórios)

> **Objetivo:** consolidar o acervo técnico do Sistema Ravena a partir dos dois arquivos-fonte
> (`repo.docx` — Acervo Técnico Consolidado; `Exportação do Gemini_...docx` — Execução do Lote 3),
> definindo 1) o **padrão único de consolidação** (como o usuário quer que fique) e 2) um **plano de
> execução** em fases para processar os reels do Instagram, mapear ferramentas/repositórios e
> padronizar o formato. Formato de entrega: **Markdown (.md)**.

---

## 1. Visão Geral e Fontes

| Fonte | Conteúdo | Uso no Projeto |
| :--- | :--- | :--- |
| `repo.docx` | Acervo Técnico Consolidado (Lotes 60–72, itens 2047–2514) + infraestrutura de rede/Nomad | Define a **estrutura padrão** do acervo e a base de itens já consolidados |
| `Exportação do Gemini_... (1).docx` | Execução do Lote 3 (Itens 21–30), pasta "Reels e carrosseis do insta" | Modelo de **paginação/processamento** dos screenshots |

**Decisão:** usar a estrutura do `repo.docx` (Item, Perfil/Criador, Assunto, Repositório, Descrição,
Status) **fundida** com os campos de detalhe do processamento do reels (Título do Arquivo, Métricas/
Engajamento, Hashtags/CTA).

---

## 2. Estrutura Única de Consolidação (PADRÃO DEFINIDO)

> Toda tabela de consolidação, em qualquer lote, DEVE usar exatamente estas 9 colunas:

| # | Coluna | Origem | Regra de preenchimento |
| :---: | :--- | :--- | :--- |
| 1 | **Item #** | Ambos | Identificador sequencial contínuo global (não reinicia por lote) |
| 2 | **Título do Arquivo** | Instagram | Nome exato do screenshot (ex: `Screenshot_20260717_134100_Rposty.jpg`) |
| 3 | **Perfil / Criador** | Ambos | Tag do criador (ex: `@globalaiforce`) |
| 4 | **Assunto / Tema Principal** | Acervo | Tema central do conteúdo (ex: "Roteamento com Traefik v3") |
| 5 | **Repositório / Ferramenta Mapeada** | repo.docx | Repo/ferramenta real associada (ex: `github.com/...`) — ver seção 4 |
| 6 | **Descrição e Aplicação Prática** | Ambos | Explicação do conteúdo e onde pode ser aplicado no Ravena |
| 7 | **Métricas / Engajamento** | Instagram | Dados de desempenho (curtidas, interações, tempo, tokens) |
| 8 | **Hashtags / CTA** | Instagram | Hashtags usadas e chamada de ação do post |
| 9 | **Status** | repo.docx | `Consolidado` / `Pendente` / `Em processamento` |

### Exemplo aplicado (item do Lote 3 refeito no padrão do acervo)

```markdown
| Item # | Título do Arquivo | Perfil/Criador | Assunto / Tema Principal | Repositório/Ferramenta Mapeada | Descrição e Aplicação Prática | Métricas / Engajamento | Hashtags / CTA | Status |
| :---: | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :---: |
| 21 | Screenshot_20260717_134100_Rposty.jpg | @globalaiforce | Open Source Free LLM API Directory | github.com/... (a mapear) | Diretório de APIs LLM gratuitas e vitalícias para desenvolvedores | 5.442 curtidas | Comentar "AI" p/ link no direct | Consolidado |
```

---

## 3. Regras de Organização por Lote

1. **Tamanho do lote:** 10 itens por lote (padrão usado no Lote 3 — manter).
2. **Sequência global:** a numeração de itens **nunca reinicia**; cada lote continua do último item.
3. **Nomenclatura:** `Execução do Lote N (Itens X a Y)` como título do capítulo; ao final, sentinela de
   continuidade: `Lote N/M concluído. Posso prosseguir com o Lote N+1 (Itens Z a W)?`
4. **Ordenação:** processar pela ordem cronológica do nome do arquivo (timestamp
   `Screenshot_YYYYMMDD_HHMMSS`).
5. **Nunca pular item:** se um item não tiver dado de alguma coluna, preencher `—` em vez de omitir a linha.

---

## 4. Mapeamento de Repositórios / Ferramentas (Regra de Ouro)

Cada ferramenta destacada no reel DEVE ser completada com um **repositório ou link real e verificável**:

| Origem da ferramenta | Como mapear | Onde registrar |
| :--- | :--- | :--- |
| Link indicado pelo criador no post/perfil | Captar a URL exata indicada | Coluna 5 |
| Ferramenta conhecida (ex: llama.cpp, vLLM) | `github.com/<org>/<repo>` oficial | Coluna 5 |
| Ferramenta nova/desconhecida | Buscar no GitHub e validar antes de gravar | Coluna 5 + nota |

> **Cuidado:** não inventar URLs. Se a ferramenta não puder ser identificada/validada, gravar
> `a mapear` e deixar `Status` como `Pendente` (rastreável no checklist).

---

## 5. Plano de Execução em Fases

### Fase 0 — Inventário
- [ ] Listar todos os screenshots da pasta "Reels e carrosseis do insta"
- [ ] Confirmar a quantidade total de itens e quantos lotes (10/lote) serão processados
- [ ] Verificar a numeração global já existente (origem dos itens no processo)
- [ ] Definir a pasta de saída do acervo consolidado

### Fase 1 — Processamento dos Reels (paginação)
- [ ] Processar em lotes de 10, usando a estrutura da seção 2 + sentinela da seção 3
- [ ] Preencher todas as colunas (arquivo, perfil, conteúdo, métricas, hashtags/CTA)
- [ ] Atualizar `Status` de cada item a cada lote concluído

### Fase 2 — Mapeamento de Ferramentas → Repositórios
- [ ] Enriquecer cada item processado com a ferramenta/repositório (seção 4)
- [ ] Validar URLs (GitHub) — marcar `a mapear` quando não confirmar
- [ ] Priorizar ferramentas de interesse do Ravena (IA, rede, kernel, segurança — conforme seção 3 do `repo.docx`)

### Fase 3 — Consolidação Total do Acervo
- [ ] Unificar todos os lotes (já existentes no `repo.docx` + novos lotes de reels) em **um único documento**, padrão da seção 2
- [ ] Reenumerar os itens sequencialmente (se houver sobreposição)
- [ ] Gerar índice/sumário do acervo (por lote e por tema)

### Fase 4 — Padronização e Validação
- [ ] Confirmar que todos os lotes seguem o template padrão
- [ ] Rodar o checklist de qualidade em todos os lotes
- [ ] Revisão final comparando com os arquivos-fonte

### Fase 5 — Entrega e Manutenção
- [ ] Gerar o documento consolidado final em Markdown
- [ ] (Opcional) Converter para DOCX se necessário para o Word/Ravena
- [ ] Definir rotina de atualização (novo reels → novo lote → reconsolidação do acervo)

---

## 6. Checklist de Qualidade (Definition of Done — por lote)

- [ ] 10 itens processados seguindo a seção 3
- [ ] Todos os campos das 9 colunas preenchidos (ou marcados `—` / `a mapear`)
- [ ] Ferramentas/repositórios validados (seção 4)
- [ ] Nenhum item duplicado de lotes anteriores
- [ ] `Status = Consolidado` apenas para linhas completas

---

## 7. Critérios de Aceite Final

- [ ] Acervo consolidado em 1 único documento, padrão da seção 2
- [ ] Todos os itens enumerados sequencialmente (sem lacunas)
- [ ] Repositórios/ferramentas conferidos ou marcados como pendentes
- [ ] Checklist da seção 6 OK para todos os lotes
- [ ] Chaveamento numérico entre lotes OK

---

## 8. Próximo Passo (ação imediata)

Após a aprovação deste documento, executar a **Fase 0 (Inventário)**: extrair a lista de todos os
screenshots da pasta "Reels e carrosseis do insta" e quantificar os lotes a processar. Em seguida,
inicia-se o **Lote 4 (Itens 31–40)**.