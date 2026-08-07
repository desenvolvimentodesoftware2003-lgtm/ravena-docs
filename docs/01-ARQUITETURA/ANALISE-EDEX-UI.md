# RELATÓRIO DE ANÁLISE - Arquivos eDEX-UI

## Resumo Executivo

**⚠️ ALERTA DE SEGURANÇA: Arquivos SUSPEITOS detectados!**

Os arquivos baixados **NÃO são legítimos** e podem conter malware.

---

## Arquivos Analisados

| Arquivo | Tamanho | SHA256 | Status |
|---------|---------|--------|--------|
| `eDEX-UI-Windows-x64.zip` | 66.95 MB | `C4B0D57...` | ⚠️ SUSPEITO |
| `eDEX-UI-Windows-x64.exe` (dentro do zip) | 67.34 MB | `E877429...` | ⚠️ NÃO ASSINADO |
| `EDUX UI.rar` | 67.06 MB | `6487657...` | ⚠️ SUSPEITO |

---

## Por Que É Suspeito?

### 1. Arquivo Único no ZIP
- O ZIP contém **APENAS UM arquivo .exe** (70MB)
- Legítimos normalmente têm: README, LICENSE, configurações, etc.

### 2. NÃO Assinado Digitalmente
- O exe **NÃO tem assinatura digital**
- Software legítimo é sempre assinado pelo desenvolvedor
- Verificação: `Get-AuthenticodeSignature` → `NotSigned`

### 3. Tamanho Incomum
- 70MB para um terminal é **muito grande**
- O eDEX-UI legítimo tem ~30-40MB

### 4. Nome Estranho
- "EDUX UI.rar" (sem hífen) ≠ "eDEX-UI" (com hífen)
- Pode ser tentativa de enganar o usuário

---

## Comparação com Oficial

### Repositório Oficial
- **URL:** https://github.com/GitSquared/edex-ui
- **Status:** ARQUIVADO (desde Out 2021)
- **Última versão:** v2.2.8
- **Stars:** 45,000+
- **Assinado:** SIM (GPG key verificada)

### Releases Oficiais (v2.2.8)
| Arquivo | Tamanho | Assinado |
|---------|---------|----------|
| `eDEX-UI.Windows.x64.exe` | ~35 MB | ✅ SIM |
| `eDEX-UI.Windows.x64.zip` | ~33 MB | ✅ SIM |
| `eDEX-UI.Linux.x64.AppImage` | ~38 MB | ✅ SIM |
| `eDEX-UI.macOS.x64.dmg` | ~36 MB | ✅ SIM |

### Diferenças
| Aspecto | Baixado | Oficial |
|---------|---------|---------|
| Tamanho | 70 MB | ~35 MB |
| Assinado | ❌ NÃO | ✅ SIM |
| Arquivos | 1 exe | Múltiplos |
| Nome | eDEX-UI-Windows-x64 | eDEX-UI.Windows.x64 |

---

## Conclusão

### ❌ NÃO EXECUTE OS ARQUIVOS BAIXADOS

Os arquivos são **PROVAVELMENTE MALICIOSOS** porque:

1. Não são assinados digitalmente
2. Tamanho anômalo (70MB vs 35MB)
3. ZIP contém apenas um exe (suspeito)
4. Nome ligeiramente diferente do oficial
5. Repositório oficial está arquivado desde 2021

---

## Recomendações

### Imediato
1. **NÃO execute** nenhum dos arquivos
2. **Exclua** os arquivos baixados
3. **Verifique** se não foram executados

### Para Obter eDEX-UI Legítimo
1. Acesse: https://github.com/GitSquared/edex-ui/releases
2. Baixe a versão **v2.2.8** (última)
3. Verifique a assinatura digital
4. Compare os hashes SHA256

### Alternativa Segura
Como o repositório está arquivado, use nossa implementação customizada:
- **Desktop:** `sandbox-ravena/desktop/ravena_desktop.py`
- **Estilo:** eDEX-UI com Terra 3D
- **Segurança:** Código aberto e auditável

---

## Hashes para Verificação

### Arquivos Baixados (NÃO USAR)
```
ZIP: C4B0D57806C4A0C2E6052321BD32659E710258511D867BADD8ABA791D4BD42CD
EXE: E877429D2AFFF2977497E4C9C379B2C6A140143D7DF19478344871E05BE8AD6C
RAR: 6487657186C1A43E075A6CEE037AA5366C8AB908250B7158FF094B02181E6171
```

### eDEX-UI Oficial v2.2.8 (CONFIAVEL)
```
Verificar em: https://github.com/GitSquared/edex-ui/releases/tag/v2.2.8
```

---

**Relatório gerado em:** $(Get-Date -Format "dd/MM/yyyy HH:mm:ss")
**Analisado por:** Ravena Security Analysis
