# Relatório de Implementação: Motor de Pesos e Detector de Divergência para o Agente de Busca da Ravena AI

**Autor:** Manus AI
**Data:** 10 de Abril de 2026

## Introdução

Este relatório detalha a implementação do **Motor de Pesos (Weight Engine)**, o "segundo tijolo" na construção do Agente de Busca da Ravena AI. O objetivo principal é capacitar a Ravena a "entender o que é importante" no vasto fluxo de notícias, categorizando, priorizando e detectando divergências de narrativa para identificar oportunidades de alavancagem. A validação inicial foi realizada com os **EUA** como "Paciente Zero", focando no par **USD** e na narrativa de **Taxa de Juros**.

## 1. O Filtro de "Palavras de Poder" (`motor_pesos_config.py`)

Foi definido um dicionário de **"Palavras de Poder"** [1], termos que indicam relevância financeira e geopolítica. Cada categoria de palavras possui um peso associado, que contribui para a nota de urgência da notícia. As categorias implementadas são:

*   **Categoria Econômica Crítica**: Termos como "taxa de juros", "FED", "inflação", "PIB", "banco central", "liquidez", "venda a descoberto". (Peso: 3)
*   **Categoria Cripto/Forex**: Termos como "halving", "ETF", "baleia", "regulação", "stablecoin", "volatilidade", "alavancagem". (Peso: 2)
*   **Categoria de Conflito (Gatilho de Divergência)**: Termos como "crise", "colapso", "boom", "recorde", "incerteza". (Peso: 4)

Além disso, foi implementada uma lista de **"Top 5 Países de Partida"** [1], que inclui EUA, Reino Unido, Brasil, China e Uruguai. A menção a um desses países na notícia confere um bônus de peso, com os EUA recebendo o maior bônus como "Paciente Zero".

## 2. A Lógica do "Ranking de Urgência" (`motor_pesos_config.py`)

Um algoritmo de **Ranking de Urgência** foi desenvolvido para atribuir uma nota de 0 a 10 a cada notícia [1]. Esta nota determina o destino da notícia:

*   **Nota 10**: Notícias de alta urgência, destinadas ao "RESUMO_RAPIDO_07H (Texto Celular)".
*   **Nota 5 a 9**: Notícias de média urgência, encaminhadas para a "TABELA_DETALHADA_11H (Mesa)".
*   **Abaixo de 5**: Notícias de baixa urgência, armazenadas no "BANCO_DE_DADOS (Auditoria Mensal)" sem interrupção imediata ao Comandante.

A nota é calculada somando os pesos das "Palavras de Poder" encontradas e o bônus do país prioritário, com um teto de 10 para a nota final.

## 3. O Motor de Pesos e o Detector de Divergência de Tríade (`motor_pesos_engine.py` e `detector_divergencia_triade.py`)

O `WeightEngine` [2] processa cada notícia, calcula sua nota de urgência e a agrupa por assunto. O **Detector de Divergência de Tríade (D-N-E)** [3] é o coração da inteligência do Agente de Busca. Ele monitora grupos de notícias sobre o mesmo assunto e, se identificar narrativas opostas (ex: "alta" vs. "queda") vindas de diferentes vieses (Esquerda e Direita), ele marca a situação como uma **"Oportunidade de Brutalidade"** e atribui uma Nota 10.

### Exemplo de "Pensamento" do Agente:

> 1.  "Li uma notícia no Jornal A (Esquerda) sobre queda do Dólar." (Nota 5)
> 2.  "Li uma notícia no Jornal B (Direita) sobre alta do Dólar." (Nota 5)
> 3.  "Divergência detectada! Atribuindo Nota 10." (Pelo Detector de Divergência)
> 4.  "Preparando resumo para o Comandante: 'ALERTA: Divergência crítica no par FED. Chance de alavancagem detectada'."

## 4. Teste "Paciente Zero": EUA e o Par USD

Foi realizada uma simulação com os EUA como "Paciente Zero" para validar o funcionamento do Motor de Pesos e do Detector de Divergência. O cenário incluiu:

*   **Jornal A (Esquerda)**: Notícia sobre "Queda do Dólar é inevitável com novas taxas do FED".
*   **Jornal B (Direita)**: Notícia sobre "Alta do Dólar deve continuar com força do FED".
*   **Jornal C (Neutro)**: Notícia sobre "FED mantém taxas de juros estáveis".

### Resultados do Teste:

| Notícia | Nota Calculada | Destino | Observações |
| :--- | :--- | :--- | :--- |
| Jornal A (Esquerda) | 5 | TABELA_DETALHADA_11H (Mesa) | Contém "taxas" e "FED" |
| Jornal B (Direita) | 5 | TABELA_DETALHADA_11H (Mesa) | Contém "FED" e "liquidez" |
| Jornal C (Neutro) | 5 | TABELA_DETALHADA_11H (Mesa) | Contém "taxas de juros" e "Banco Central" |

Ao aplicar o Detector de Divergência de Tríade para o assunto "FED", o sistema identificou corretamente o conflito de narrativa entre o Jornal A (queda do Dólar) e o Jornal B (alta do Dólar). O resultado foi:

*   **STATUS**: `OPORTUNIDADE_DE_BRUTALIDADE`
*   **NOTA FINAL**: `10`
*   **DETALHES**: `Conflito de narrativa detectado entre Jornal A (Esquerda) e Jornal B (Direita).`
*   **RESUMO PARA O COMANDANTE**: `'ALERTA: Divergência crítica no par FED. Chance de alavancagem detectada.'`

## Conclusão

A implementação do Motor de Pesos e do Detector de Divergência de Tríade foi bem-sucedida. O Agente de Busca da Ravena AI agora possui a capacidade de ir além da simples coleta de informações, aplicando inteligência para identificar o que é verdadeiramente importante e acionável. O teste "Paciente Zero" demonstrou a eficácia do sistema em detectar conflitos de narrativa e gerar alertas de alta prioridade para o Comandante, pavimentando o caminho para trades de alavancagem mais precisos e informados.

## Referências

[1] `motor_pesos_config.py` (Configuração de Palavras de Poder e Ranking de Urgência).
[2] `motor_pesos_engine.py` (Implementação do Motor de Pesos).
[3] `detector_divergencia_triade.py` (Implementação do Detector de Divergência de Tríade e Teste "Paciente Zero").
