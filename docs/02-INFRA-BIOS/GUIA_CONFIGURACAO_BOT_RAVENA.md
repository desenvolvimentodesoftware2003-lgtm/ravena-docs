# Guia Passo a Passo: Configuração do Bot Ravena no Telegram

Este guia detalha o processo de configuração e ativação do seu bot Ravena no Telegram, permitindo que ele envie notificações sobre o status da sincronização GitHub-Drive e responda a comandos para monitoramento de logs.

## Pré-requisitos

Antes de começar, certifique-se de que você tem:

-   Acesso ao seu ambiente de execução onde o projeto Ravena AIM está clonado (`/home/ubuntu/ravena-aim`).
-   O script `sync_ravena.py` modificado e o módulo `bot_ravena.py` presentes em seus respectivos locais no repositório (`/home/ubuntu/ravena-aim/sync_ravena.py` e `/home/ubuntu/ravena-aim/modulos/api/bot_ravena.py`).
-   O script `start_bot.sh` em `/home/ubuntu/ravena-aim/scripts/start_bot.sh`.

## Passo 1: Criar o Bot no BotFather e Obter o Token

O BotFather é o bot oficial do Telegram para gerenciar seus bots. Ele fornecerá o `BOT_TOKEN` necessário para que seu bot Ravena se conecte à API do Telegram.

1.  **Abra o Telegram:** No seu aplicativo Telegram, procure por `@BotFather` e inicie uma conversa.
2.  **Crie um Novo Bot:** Envie o comando `/newbot` para o BotFather.
3.  **Escolha um Nome:** O BotFather pedirá um nome para o seu bot (ex: `Ravena AIM Bot`). Digite e envie.
4.  **Escolha um Username:** Em seguida, ele pedirá um username para o seu bot. Este deve ser único e terminar com `bot` (ex: `RavenaAIM_bot`). Digite e envie.
5.  **Obtenha o `BOT_TOKEN`:** Após o sucesso, o BotFather enviará uma mensagem com o `HTTP API Token` do seu bot. Este é o seu `BOT_TOKEN`. **Copie este token e guarde-o em segurança.** Ele se parecerá com algo como `123456789:ABCDEFGH-IJKLMNOPQRSTUVWYZX_abcdefghij`.

## Passo 2: Obter o ID do Chat (`CHAT_ID`)

Para que o bot Ravena possa enviar notificações para você (ou para um grupo específico), ele precisa saber o `CHAT_ID` do chat de destino.

1.  **Inicie uma Conversa com Seu Bot:** No Telegram, procure pelo username que você acabou de criar para o seu bot (ex: `@RavenaAIM_bot`) e inicie uma conversa com ele. Você pode enviar um simples `Olá`.
2.  **Execute o Bot Localmente (Temporariamente):** Para obter o `CHAT_ID`, você precisará executar o bot Ravena uma vez. Abra um terminal no seu ambiente de execução e navegue até o diretório do projeto:
    ```bash
    cd /home/ubuntu/ravena-aim
    ```
    Agora, execute o script `bot_ravena.py` diretamente, substituindo `YOUR_BOT_TOKEN` pelo token que você obteve no Passo 1:
    ```bash
    export TELEGRAM_BOT_TOKEN="SEU_TOKEN_DO_BOTFATHER_AQUI"
    python3 modulos/api/bot_ravena.py
    ```
    *Nota: O bot pode reclamar que o `CHAT_ID` não está configurado, mas isso é esperado neste momento.*
3.  **Envie o Comando `/get_chat_id`:** De volta ao Telegram, no chat com o seu bot, envie o comando `/get_chat_id`.
4.  **Copie o `CHAT_ID`:** O bot responderá com o ID do chat. Este será um número (ex: `123456789`) ou um número negativo para grupos (ex: `-1234567890123`). **Copie este `CHAT_ID` e guarde-o.**
5.  **Pare o Bot Localmente:** No terminal onde o bot está rodando, pressione `Ctrl+C` para pará-lo.

## Passo 3: Configurar Variáveis de Ambiente e Iniciar o Bot em Segundo Plano

Agora que você tem o `BOT_TOKEN` e o `CHAT_ID`, você pode configurar o ambiente e iniciar o bot para execução contínua.

1.  **Edite o Script `start_bot.sh`:** Abra o arquivo `/home/ubuntu/ravena-aim/scripts/start_bot.sh` em um editor de texto.
    ```bash
    nano /home/ubuntu/ravena-aim/scripts/start_bot.sh
    ```
2.  **Descomente e Preencha as Variáveis:** Descomente as linhas `export TELEGRAM_BOT_TOKEN` e `export TELEGRAM_CHAT_ID` e substitua os placeholders pelos seus valores reais:
    ```bash
    #!/bin/bash

    # Navega para o diretório do projeto
    cd /home/ubuntu/ravena-aim

    # Define as variáveis de ambiente necessárias (Substitua pelos seus valores reais)
    export TELEGRAM_BOT_TOKEN="SEU_TOKEN_DO_BOTFATHER_AQUI"
    export TELEGRAM_CHAT_ID="SEU_CHAT_ID_AQUI"

    # Inicia o bot em segundo plano usando nohup
    # Os logs do bot serão salvos em logs/bot_output.log
    nohup python3 modulos/api/bot_ravena.py > logs/bot_output.log 2>&1 &

    echo "Bot Ravena iniciado em segundo plano (PID: $!)"
    echo "Logs disponíveis em: /home/ubuntu/ravena-aim/logs/bot_output.log"
    ```
    Salve e feche o arquivo (no `nano`, `Ctrl+X`, `Y`, `Enter`).
3.  **Inicie o Bot:** Execute o script `start_bot.sh` para iniciar o bot em segundo plano:
    ```bash
    cd /home/ubuntu/ravena-aim
    ./scripts/start_bot.sh
    ```
    Você verá uma mensagem confirmando que o bot foi iniciado e o PID do processo.

## Passo 4: Testar o Bot e as Notificações

Com o bot rodando em segundo plano, é hora de testar suas funcionalidades.

1.  **Teste os Comandos do Bot:** No Telegram, no chat com o seu bot, tente os seguintes comandos:
    -   `/start`
    -   `/help`
    -   `/logs <nome_de_um_arquivo_de_log_existente>` (ex: `/logs bot_output.log` ou `/logs log_ravena.txt` se você tiver um)
2.  **Teste as Notificações de Sincronização:** Como o script `sync_ravena.py` foi modificado para enviar notificações, você pode forçar uma sincronização para ver as mensagens no Telegram.
    ```bash
    cd /home/ubuntu/ravena-aim
    python3 sync_ravena.py
    ```
    Você deverá receber mensagens no Telegram informando sobre o início e o fim da sincronização, ou quaisquer falhas.

## Gerenciamento do Bot

-   **Verificar Logs do Bot:** Os logs do bot são salvos em `/home/ubuntu/ravena-aim/logs/bot_output.log`.
-   **Parar o Bot:** Para parar o bot, você precisará encontrar o PID do processo e terminá-lo. Você pode usar `pgrep -f bot_ravena.py` para encontrar o PID e `kill <PID>` para pará-lo.

Este guia completo deve ajudá-lo a ter seu bot Ravena no Telegram totalmente operacional e integrado ao seu fluxo de trabalho de sincronização!

---
*Guia gerado automaticamente pelo sistema de integração.*
