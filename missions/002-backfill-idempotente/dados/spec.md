# Especificação do resumo — vendas diárias

O que a tabela de resumo (`vendas_diarias`) deve conter, e como cada evento vira número. É contra isto que o seu reprocesso tem que chegar sempre no mesmo resultado.

## Os arquivos que você recebe

### `eventos.csv` — a fonte (só leitura)

| Coluna | Tipo | O que é |
| -- | -- | -- |
| `evento_id` | texto | Identificador único do evento (a venda). **É a chave natural para deduplicar.** |
| `event_time` | timestamp (`AAAA-MM-DDThh:mm:ss`) | Quando a venda aconteceu. O **dia** do resumo sai daqui. |
| `loja_id` | texto | A loja. |
| `valor` | número decimal | Valor da venda (ponto como separador decimal). |
| `data_lote` | data (`AAAA-MM-DD`) | O dia em que aquele registro **chegou** no seu lado. Informativo — ver "evento atrasado". |

### `vendas_diarias_atual.csv` — o estado atual da tabela de resumo

| Coluna | Tipo | O que é |
| -- | -- | -- |
| `dia` | data (`AAAA-MM-DD`) | O dia da venda. |
| `loja_id` | texto | A loja. |
| `pedidos` | inteiro | Quantidade de vendas naquele dia/loja. |
| `valor_total` | decimal | Soma dos valores naquele dia/loja. |

Este arquivo já tem dias corretos, **um dia carregado pela metade** e **três dias faltando**. É o ponto de partida do seu reprocesso — não um rascunho pra jogar fora sem pensar.

## O grão do resumo

**Uma linha por (`dia`, `loja_id`).** Para cada uma:

- `pedidos` = quantidade de `evento_id` **distintos**.
- `valor_total` = soma de `valor` sobre esses `evento_id` distintos.
- `dia` = a **data do `event_time`** (não a do `data_lote`).

## As duas regras que decidem tudo

**Duplicata de entrega.** O mesmo `evento_id` pode aparecer mais de uma vez (foi reentregue num lote posterior). Conta **uma vez**. Duas entregas do mesmo evento não são duas vendas.

**Evento atrasado.** Um evento pertence ao **dia do `event_time`**, mesmo que tenha chegado num `data_lote` posterior. Ou seja: reprocessar um dia tem que capturar os eventos daquele `event_time` que chegaram atrasados — é justamente por isso que reprocessar precisa ser seguro e dar o resultado certo, não o resultado "de quando rodou pela primeira vez".

> Repare no encaixe entre as duas regras e a idempotência: se o seu reprocesso apaga-e-recalcula a partição de um dia a partir do `event_time`, duplicata e atraso se resolvem sozinhos e rodar de novo não muda nada. Se ele soma em cima do que já existe, os dois viram bug.
