# Esquema esperado — extrato de pedidos do parceiro

Este é o **combinado com o parceiro**: o formato que um arquivo precisa ter para poder entrar. É contra isto que o seu portão decide.

## Formato do arquivo

| Item | Combinado |
| -- | -- |
| Formato | CSV |
| Separador | vírgula (`,`) |
| Encoding | UTF-8 |
| Primeira linha | cabeçalho, com os nomes das colunas exatamente como abaixo |
| Separador decimal | ponto (`.`) — ex.: `150.00`. Sem símbolo de moeda, sem separador de milhar |
| Formato de data | `AAAA-MM-DD` — ex.: `2026-08-01` |
| Campo de texto com vírgula | entre aspas duplas (`"..."`) |

## Colunas

| Coluna | Tipo | Obrigatória? | Observação |
| -- | -- | -- | -- |
| `pedido_id` | texto | sim | **Chave.** Único no arquivo — não pode repetir |
| `data_pedido` | data (`AAAA-MM-DD`) | sim | |
| `cliente_id` | texto | sim | Pode repetir (o mesmo cliente faz vários pedidos) |
| `valor_total` | número decimal | sim | Ponto como separador decimal; sem `R$` |
| `status` | texto (lista fechada) | sim | Um de: `criado`, `pago`, `enviado`, `entregue`, `cancelado` |
| `cupom` | texto | não | Pode vir vazio |
| `itens` | número inteiro | sim | Quantidade de itens; inteiro positivo |
| `observacao` | texto livre | não | Pode vir vazio; pode ter acentos |

## O que torna um arquivo "bom"

Um arquivo pode entrar quando:

- Abre em UTF-8 sem erro de encoding.
- Tem exatamente as colunas do cabeçalho acima (nem faltando, nem sobrando o que não foi combinado).
- Toda coluna obrigatória está preenchida em toda linha.
- `valor_total` é número, `itens` é inteiro, `data_pedido` é uma data válida no formato combinado.
- `status` está na lista fechada.
- Nenhum `pedido_id` repetido.

## O que o parceiro já mandou quebrado antes

Não é lista exaustiva — é o histórico de dor que motivou a Mission. Seu portão deve pegar pelo menos estes tipos:

- Uma coluna a menos que o combinado.
- Um valor no tipo errado (texto onde era número, valor com `R$` ou vírgula decimal).
- `pedido_id` repetido no mesmo arquivo.
- Arquivo salvo em encoding errado (acentos ilegíveis).
- Arquivo vazio.

> Os arquivos em `dados/` misturam bons e quebrados, **sem etiqueta de qual é qual**. Descobrir isso faz parte.
