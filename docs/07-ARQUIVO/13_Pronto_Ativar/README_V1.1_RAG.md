# Ravena AI Trading Bot

**Versão:** 1.0.0  
**Arquitetura:** Modular, baseada nos padrões da Ravena AI Core Infrastructure V2.0.5  
**Plataforma:** Python 3.11+ | Oracle Cloud (OCI) | Bybit API v5

---

## Visão Geral da Arquitetura

Este projeto foi estruturado seguindo os padrões modulares da **Ravena_AI_Core_Infrastructure**, com foco em separação de responsabilidades, segurança por design (credenciais via variáveis de ambiente, nunca em código) e facilidade de manutenção.

O bot opera em um ciclo contínuo: **Leitura de Preço → Análise (Técnica + Sentimento) → Sinal → Execução → Notificação**.

---

## Estrutura de Módulos

| Módulo | Arquivo | Responsabilidade |
| :--- | :--- | :--- |
| **Conectividade** | `src/bybit_connector.py` | Autenticação HMAC, leitura de tickers, criação de ordens |
| **Cérebro de Trade** | `src/trade_brain.py` | Médias Móveis, RSI, Regressão Linear, geração de sinais. **Agora com filtro de Sentimento RAG.** |
| **Emulador de Clique** | `src/click_emulator.py` | Execução via PyAutoGUI para simular comportamento humano |
| **Monitoramento** | `src/monitor_logs.py` | Notificações Telegram, logs locais, heartbeat |
| **Análise de Sentimento RAG** | `src/sentiment_analyzer.py` | Coleta notícias de criptomoedas e calcula score de sentimento para validação de sinais. |
| **Orquestrador** | `src/main.py` | Integra todos os módulos no loop principal |


---

## Módulo 1: Conectividade (bybit_connector.py)

Responsável pela ponte com a corretora Bybit via API v5.

**Autenticação HMAC SHA256:**
```
timestamp + api_key + recv_window + payload → HMAC SHA256 → signature
```

**Endpoints utilizados:**
- `GET /v5/market/tickers` — Preço em tempo real
- `GET /v5/account/wallet-balance` — Saldo da carteira
- `POST /v5/order/create` — Criação de ordens (Market/Limit)

---

## Módulo 2: Cérebro de Trade (trade_brain.py)

Implementa a lógica de análise técnica para capturar a volatilidade do BTC.

**Estratégia:** Cruzamento de Médias Móveis + RSI + Confirmação por Regressão Linear

| Indicador | Parâmetros | Papel na Estratégia |
| :--- | :--- | :--- |
| SMA Curta | 9 períodos | Detectar cruzamento (Golden/Death Cross) |
| SMA Longa | 21 períodos | Referência de tendência principal |
| RSI | 14 períodos | Filtrar sobrecompra (>70) e sobrevenda (<30) |
| Regressão Linear | 20 períodos | Confirmar direção da tendência (slope) |

**Sinal de Compra (BUY):** SMA9 > SMA21 + RSI < 70 + Slope Positivo  
**Sinal de Venda (SELL):** SMA9 < SMA21 + RSI > 30 + Slope Negativo

---

## Módulo 3: Emulador de Clique (click_emulator.py)

Alternativa à API para execução de ordens via interface web.

**Quando usar:**
- Quando a API possui restrições ou está em manutenção
- Para simular comportamento humano e evitar detecção

**Recursos:**
- Movimento de mouse não-linear (curva de Bézier via PyAutoGUI)
- Atrasos aleatórios entre ações
- Modo Dry Run automático em ambientes headless (sem display)

**Dependência:** Requer `pyautogui`. Em Oracle Cloud (headless), instalar `Xvfb`:
```bash
sudo apt install xvfb
Xvfb :99 -screen 0 1920x1080x24 &
export DISPLAY=:99
```

---

## Módulo 4: Monitoramento e Logs (monitor_logs.py)

Integração com Telegram para notificações em tempo real.

**Tipos de notificação:**
- `notify_trade_execution` — Ordem executada (compra/venda)
- `notify_alert` — Alertas de sistema (INFO, WARNING, CRITICAL)
- `notify_heartbeat` — Status periódico de saúde do bot

**Logs locais:** Salvos em `logs/trading_bot_YYYYMMDD.log`

---

## Configuração e Execução

### 1. Instalar dependências
```bash
pip install requests numpy pandas pyautogui
```

### 2. Configurar variáveis de ambiente
```bash
cp config/.env.example config/.env
# Editar config/.env com suas credenciais
export $(cat config/.env | xargs)
```

**Novas variáveis de ambiente necessárias:**
```
CRYPTOPANIC_API_TOKEN=seu_api_token_cryptopanic
```
*Certifique-se de obter seu `CRYPTOPANIC_API_TOKEN` no site do CryptoPanic para ativar a análise de sentimento.*

### 3. Executar o bot
```bash
cd src
python main.py
```

### 4. Executar em background (Oracle Cloud)
```bash
nohup python main.py > ../logs/nohup.log 2>&1 &
```

---

## Segurança

- Credenciais **nunca** são escritas em código — apenas via variáveis de ambiente
- Chaves de API são usadas apenas para assinar requisições (HMAC), nunca logadas
- PyAutoGUI configurado com `FAILSAFE=True` (mover mouse para o canto aborta)
- Tratamento de erros em todos os módulos para evitar travamentos

---

## Próximos Passos

1. **Backtesting:** Validar a estratégia com dados históricos antes de operar com capital real
2. **Gestão de Posições:** Implementar controle de posições abertas e Stop Loss dinâmico
3. **Integração RAG:** Conectar ao módulo RAG da Ravena para análise de sentimento de notícias
4. **Dashboard:** Criar painel de monitoramento em tempo real
