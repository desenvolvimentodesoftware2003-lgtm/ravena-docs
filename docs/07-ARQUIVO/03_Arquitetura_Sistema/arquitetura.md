# Arquitetura do Sistema Ravena AIM

## Componentes Principais

### 1. Engine Cognitivo (`modulos/engine/`)
Motor principal responsável pelo processamento de linguagem natural, raciocínio e tomada de decisão.

### 2. Módulo RAG (`modulos/rag/`)
Sistema de Recuperação Aumentada por Geração para consulta de base de conhecimento.

### 3. Subagentes Especializados (`modulos/subagentes/`)
Agentes independentes com especialidades específicas (análise, síntese, execução).

### 4. Camada de API (`modulos/api/`)
Interface RESTful para integração com sistemas externos.

## Fluxo de Dados

```
Entrada → Engine → RAG → Subagentes → Resposta
                ↕
           Memória Semântica
```

## Integração com Drive

Os artefatos persistentes são sincronizados automaticamente com a pasta `RAVENA_MODULAR` no Google Drive.
