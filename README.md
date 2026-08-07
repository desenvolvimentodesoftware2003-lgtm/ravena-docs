# Ravena DOCS

Documentação oficial do **Ravena OS** — remaster de Arch Linux para trading na B3, terminal-only (eDEX-UI).

## Estrutura

```
DOCS/
├── 00_PDFs/              # Biblioteca técnica (33 PDFs: arquitetura, segurança, redes, LLM)
├── 01-ARQUITETURA/       # Arquitetura e implantação (RV6/RV7), triagem de repos, análise eDEX-UI
├── 02-INFRA-BIOS/        # Provisionamento de BIOS, boot, chroot, VM, guia de configuração do bot
├── 03-AIRLLM-LLM/        # Otimização/particionamento de memória para LLMs (airLLM)
├── 04-SEGURANCA/         # Relatórios de vulnerabilidade, VPN, hardening
├── 05-NOTAS-RAVENA/      # Notas do desenvolvedor
├── 06-LOGS-BOOT/         # Logs de boot e telas de diagnóstico
├── 07-ARQUIVO/           # Biblioteca técnica (157 .md: relatórios, docs de sistema cognitivo)
└── README.md             # Este arquivo
```

## Documentos-chave

- **Arquitetura:** `01-ARQUITETURA/Documento_Completo_de_Arquitetura.txt` (Sistema RV6)
- **BIOS:** `02-INFRA-BIOS/` (provisionamento, boot, chroot)
- **LLM:** `03-AIRLLM-LLM/` (otimização de memória para LLMs)
- **Segurança:** `04-SEGURANCA/` (vulnerability_report, VPN)
- **Biblioteca técnica:** `07-ARQUIVO/` e `00_PDFs/`

## Versionamento

Este repositório contém **somente documentação**. O código-fonte está em:
- **CODE:** `github.com/desenvolvimentodesoftware2003-lgtm/ravena-code`
- **DOCS:** `github.com/desenvolvimentodesoftware2003-lgtm/ravena-docs` (este repo)
