# Contas a Pagar — Painel financeiro

Dashboard interativo de contas a pagar feito em HTML, CSS e JavaScript puro (sem build, sem framework).
Tem visão geral, pagamentos, saldo a pagar, tabela de contas, filtros por categoria, centro de custo,
status, filial e período, e um assistente que responde perguntas sobre os dados.

## Como abrir

Baixe o repositório e dê dois cliques no `index.html`. Não precisa instalar nada.
É necessário internet só para carregar o Chart.js e a fonte (via CDN).

## Estrutura

```
.
├── index.html               # estrutura da página (layout, abas, cartões, painel do assistente)
├── css/
│   ├── styles.css           # tema, layout, cartões, gráficos, tabela, assistente
│   └── foco.css             # estilos do modo "foco" (mini-cartões ao clicar num cartão)
└── js/
    ├── chartjs-fallback.js  # carrega o Chart.js de um CDN alternativo se o principal falhar
    ├── data.js              # base de dados (RAW_ROWS) — uma linha por conta
    ├── core.js              # formatadores (R$, datas), preparo dos dados e filtros
    ├── charts.js            # cálculo das estatísticas e funções auxiliares dos gráficos
    ├── render.js            # desenha KPIs e gráficos conforme os filtros
    ├── chat.js              # assistente: motor de respostas, interface e linhas até os gráficos
    ├── analysis.js          # tabelas e indicadores de análise
    ├── tabs-table.js        # troca de abas, botões de ano e tabela de contas
    ├── assistant-tour.js    # roteiro da pergunta: escolhe aba, gráficos e cartões a destacar
    ├── local-ai.js          # IA local opcional (Phi-3.5 via WebLLM, roda no navegador)
    ├── focus.js             # modo foco: clicar num cartão abre análises em volta
    └── main.js              # ponto de partida: desenha o painel
```

Os scripts são carregados em ordem no `index.html` e compartilham variáveis globais,
então **a ordem das tags `<script>` importa**.

## Usando seus próprios dados

Substitua o conteúdo de `js/data.js`. Cada conta é uma lista com 16 campos, nesta ordem:

| # | Campo | Exemplo |
|---|-------|---------|
| 0 | Competência (AAAA-MM) | `"2025-08"` |
| 1 | Status (`Pago`, `Vencido`, `Em aberto`, `Agendado`, `Cancelado`) | `"Vencido"` |
| 2 | Categoria | `"Software"` |
| 3 | Centro de custo | `"Financeiro"` |
| 4 | Filial | `"Matriz"` |
| 5 | Fornecedor | `"Fornecedor X"` |
| 6 | Valor pago | `0.0` |
| 7 | Saldo em aberto | `12980.12` |
| 8 | Juros | `1546.26` |
| 9 | Multa | `224.19` |
| 10 | Dias de atraso | `418` |
| 11 | Nº da NF | `"NF-809570"` |
| 12 | Vencimento (AAAA-MM-DD) | `"2025-08-06"` |
| 13 | Valor original | `11209.67` |
| 14 | Forma de pagamento | `"Boleto"` |
| 15 | Responsável | `"Gabriel"` |

## Tecnologias

- [Chart.js 4.4.4](https://www.chartjs.org/) para os gráficos
- Fonte [Inter](https://fonts.google.com/specimen/Inter)
- [WebLLM](https://github.com/mlc-ai/web-llm) (opcional) para a IA local
