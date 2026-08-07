# RAVENA - Security Sandbox

## O Que É Este Projeto?

O **Ravena** é um sistema de segurança completo que inclui:

- **Sistema operacional** Arch Linux com hardening de segurança
- **Desktop** estilo eDEX-UI com Terra 3D
- **Interface web** estilo Manus AI (tema roxo e preto)
- **Criptografia pós-quântica** (CRYSTALS-Kyber, Dilithium, FALCON, SPHINCS+)
- **TLS 1.3** exclusivamente
- **Docker** com todos os serviços

---

## Estrutura da Pasta

```
ravena/
├── sandbox-ravena/          # Código-fonte do sistema
│   ├── app.py               # Servidor principal
│   ├── web/                 # Interface web
│   ├── desktop/             # Desktop eDEX-UI
│   ├── scripts/             # Scripts de segurança
│   └── docker-compose.yml   # Serviços Docker
│
├── ravena-archiso/          # Configuração da ISO
│   ├── archiso/             # Perfil do Archiso
│   ├── scripts/             # Scripts de build
│   └── BUILD_README.md      # Instruções de compilação
│
└── output/                  # ISO compilada (gerado)
```

---

## Como Compilar a ISO

### Pré-requisitos

- **Arch Linux** (ou use uma VM)
- **4GB+ de RAM**
- **20GB+ de espaço livre**

### Passos

```bash
# 1. Copiar esta pasta para um Arch Linux
# 2. Abrir terminal na pasta ravena-archiso/scripts/
# 3. Rodar:

sudo ./build_env.sh        # Preparar ambiente
./generate_passwords.sh    # Gerar senhas
sudo ./build_iso.sh        # Compilar ISO (15-30 min)
```

### Resultado

A ISO será gerada em:
```
ravena/output/ravena-archlinux-YYYY.MM.DD.iso
```

---

## Como Instalar

### 1. Gravar no Pendrive

**Linux:**
```bash
sudo dd if=output/ravena-archlinux-*.iso of=/dev/sdX bs=4M status=progress
```

**Windows:**
- Use [Etcher](https://www.balena.io/etcher/) ou [Rufus](https://rufus.ie/)

### 2. Bootar pelo Pendrive

1. Reiniciar computador
2. Pressionar **F12** para boot menu
3. Selecionar pendrive

### 3. Pronto!

A Ravena já estará rodando:
- **Desktop:** Interface eDEX-UI (sem senha)
- **Web:** `https://localhost` (com senha)

---

## Senhas Padrão

| Serviço | Usuário | Senha |
|---------|---------|-------|
| Sistema | ravena | (sem senha) |
| Web | admin | ravena2024 |
| Web | user | user2024 |

---

## Funcionalidades

### Desktop (eDEX-UI Style)
- Terminal integrado
- Terra 3D (mapa do mundo)
- Monitor de sistema
- Monitor de rede
- Painel de pentest

### Interface Web (Manus AI Style)
- Login com JWT (90 dias)
- Chat com agente
- Terminal ao vivo
- Dashboard com status
- Tema roxo e preto

### Segurança
- Criptografia pós-quântica
- TLS 1.3 apenas
- Firewall configurado
- Monitoramento de integridade
- Backup automático

---

## Suporte

Em caso de problemas, consulte:
- `BUILD_README.md` - Instruções detalhadas de compilação
- `INSTALL_ARCHLINUX.md` - Guia de instalação do Arch Linux

---

**Feito com ❤️ pela Ravena Security Lab**
