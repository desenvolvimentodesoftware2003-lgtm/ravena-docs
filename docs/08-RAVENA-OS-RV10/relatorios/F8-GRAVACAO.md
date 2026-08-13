# F8 — Gravação Final no Pendrive + Verificação

**Status:** ✅ Gravado e verificado (3/3 blocos íntegros)
**Data:** 2026-08-13 ~00:15

## Gravação

- **Alvo**: SanDisk Cruzer Blade (114.6 GB, Disco 1, MBR)
- **Método**: Rufus, modo DD (gravação bruta do ISO)
- **ISO**: `ravena-remaster-RV10.iso` (hash conferido ANTES da gravação)

### Controle de hash (antes)

```
sha512(ravena-remaster-RV10.iso) =
3b99d52dfdce205ad2992723714189e3579fbb0992df5a709d5cdf8e915813a636fe80297aa8bbd19395f5b5f008564cda69750d1a4c358c877aea234c9f7d10
```

## Verificação física pós-gravação

Script `VERIFICAR_PENDRIVE.ps1` (requer admin) lê setores físicos
(`\\.\PHYSICALDRIVE1`) e compara hashes SHA512 com o ISO original.

| Bloco verificado | Resultado |
|---|---|
| MBR — assinatura `55AA` | ✅ |
| Boot isohybrid (1 MB @ offset 0) | ✅ hash idêntico |
| Squashfs (4 MB @ offset 8 MB) | ✅ hash idêntico |
| Final do ISO (2 MB) | ✅ hash idêntico |

**RESULTADO: GRAVAÇÃO ÍNTEGRA — todos os blocos conferem com o ISO.**

## Estrutura de partição observada (Windows)

- Partição EFI de 23 MB em offset 7.788.873.728 (padrão isohybrid do Arch:
  ISO inteiro + ESP no gap final)

## Entregáveis relacionados

- `GRAVAR_RV10.ps1` — gravação com conferência de hash + confirmação obrigatória
- `VERIFICAR_PENDRIVE.ps1` — verificação física pós-gravação
- `ROTEIRO_INSTALACAO.md` — passo a passo de instalação no PC real

## Próximo passo (teste real no PC)

1. Ligar o Latitude 5400 → **F12** → escolher o SanDisk
2. O sistema cria o LUKS e imprime a **chave de recuperação** (imprimir/guardar)
3. Configurar WiFi no OOBE
4. Validar: `net`, `ravena-hardware`, `horas`, dev tools, eDEX-UI, `intel`, `llm`
5. (Opcional) `ravena-instalar` para instalação definitiva no NVMe
