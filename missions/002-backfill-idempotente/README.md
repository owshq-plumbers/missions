# 002 — Rodar de novo sem estragar

## O caso

Um time de dados tem um job que roda toda madrugada: pega os eventos de venda do dia anterior e escreve uma linha por dia numa tabela de resumo (`vendas_diarias`), que alimenta os painéis. Roda às 6h, para "ontem", e ninguém olha — até parar.

Semana passada uma credencial da fonte expirou e o job **não rodou por três dias**. Quando perceberam, tinham dois problemas de uma vez. O primeiro: um buraco de três dias na tabela. O segundo, pior: quem tentou "só rodar de novo" descobriu que o job **soma em cima** do que já existe — rodar o mesmo dia duas vezes **dobra os números**. E o dia em que o job morreu no meio ficou **carregado pela metade**.

Agora ninguém quer encostar. Fazer o backfill dos três dias pode duplicar. Re-rodar o dia que carregou pela metade pode piorar. O time trava toda vez que precisa reprocessar qualquer coisa.

A pergunta que trouxeram: *como fazer esse job poder rodar de novo — para um dia ou para um intervalo — sem medo, sempre chegando no mesmo resultado certo?*

## O que você recebe

Em [`dados/`](dados/):

- Os **eventos crus** da fonte (`eventos.csv`), cobrindo o período — incluindo os dias do buraco. É o dado real, com a bagunça real: algumas entregas duplicadas do mesmo evento e alguns eventos que chegaram atrasados (o evento é de um dia, mas só apareceu no lote do dia seguinte).
- O **estado atual** da tabela de resumo (`vendas_diarias_atual.csv`): alguns dias já carregados corretos, **um dia carregado pela metade**, e os três dias do buraco ausentes.
- A **especificação do resumo** (`dados/spec.md`): qual é o grão (uma linha por dia por chave), como cada evento vira número, e o que fazer com duplicata e evento atrasado.

## O que se espera de você

Uma transformação que você possa rodar para **um dia** ou para **um intervalo de dias** e que seja **idempotente e segura para re-rodar**:

- Rodar o mesmo dia duas vezes leva a tabela ao **mesmo estado** — não duplica.
- Fazer o backfill dos dias que faltam preenche o buraco com os números certos.
- Re-rodar o dia que carregou pela metade **conserta** aquele dia, em vez de somar em cima do pedaço que já estava lá.

O ponto inteiro é esse: reprocessar tem que ser uma operação sem medo. Mostre no README **como rodar** (para um dia e para um intervalo) e **como alguém confirma** que rodar de novo não mudou o resultado.

## Restrições

- Roda na máquina de quem revisa com **um comando**, parametrizado por data ou intervalo (documente qual).
- Não pode depender de serviço pago nem de nada que precise de chave para rodar.
- Não altere o arquivo de eventos de origem — ele é a fonte, é só leitura.
- A tabela de resumo **começa do estado fornecido** — não vale simplesmente apagar tudo e reconstruir do zero *sem justificar*. Reconstrução total é uma estratégia idempotente legítima; se for o seu caminho, diga por que ela é aceitável aqui (custo, volume) em vez de um incremental.

## Tempo estimado

Faixa honesta: **4 a 7 horas.** É a primeira turma; o tempo será calibrado com as entregas.

## Como entregar

Ver [`ENTREGA.md`](../../ENTREGA.md) na raiz.

## Critérios de aceite

Ver [`CRITERIOS.md`](CRITERIOS.md), nesta pasta. **Leia antes de começar.**
