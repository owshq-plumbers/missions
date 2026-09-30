# Critérios de aceite — Mission 002 (Rodar de novo sem estragar)

Estes critérios são **públicos e completos**. Não existe critério secreto: o que decide a revisão está escrito aqui.

O que fica no repositório privado é o *gabarito* — a solução de referência e as notas de quem revisa. Isso é separado pelo mesmo motivo que uma prova tem gabarito à parte.

> **Nível: Média.** As dimensões são as mesmas de toda Mission; o que muda é a altura da barra. Em relação à Mission 001 (fácil), aqui a barra sobe principalmente na dimensão 2 (não basta rodar — tem que rodar **de novo** e dar o mesmo resultado) e na 3 (a escolha da estratégia de reprocesso é o coração da entrega).

---

## Como a revisão lê

Cada dimensão recebe um de três estados:

| Estado | Significa |
| -- | -- |
| **Atende** | Faz o que se pede, de forma verificável |
| **Atende com ressalva** | Chega ao resultado, mas com um problema que valeria corrigir |
| **Não atende** | Falta, ou não é possível verificar |

O veredito final é **aprovado**, **ajustes** ou **reprovado**, composto a partir dos estados por dimensão.

---

## Dimensões

### 1. O problema foi entendido

O que se ataca é **re-rodar com segurança contra uma tabela que já tem estado** — não um carregamento único do zero.

- [ ] O grão do resumo (uma linha por dia por chave) está respeitado e escrito
- [ ] Está claro o que acontece ao re-rodar um dia que já existe e ao preencher um dia que falta
- [ ] O que ficou fora de escopo está dito

### 2. A solução funciona e dá para verificar

Aqui está o coração: não basta produzir a tabela — tem que **poder rodar de novo**.

- [ ] Um comando documentado roda a transformação para um dia **e** para um intervalo
- [ ] Rodar o mesmo dia duas vezes leva ao **mesmo estado** (nada duplica) — e dá para demonstrar isso
- [ ] O backfill dos dias que faltam preenche com os números corretos
- [ ] Re-rodar o dia carregado pela metade **conserta**, em vez de somar em cima
- [ ] Roda a partir do README, sem conhecimento tácito e sem chave

### 3. As decisões estão justificadas

A parte que mais separa níveis. A estratégia de reprocesso é uma escolha, não um detalhe.

- [ ] Está escrito **qual** estratégia garante a idempotência (ex.: `upsert`/merge por chave, apagar-e-reinserir a partição do dia, sobrescrever partição, reconstrução total) e **por quê**
- [ ] Aparece ao menos uma alternativa descartada com o porquê
- [ ] As decisões sobre **duplicata de evento** e **evento atrasado** estão nomeadas e justificadas (o que conta, em que dia entra)

### 4. Aguenta a realidade

- [ ] Trata duplicata de evento e evento atrasado conforme a `spec.md`
- [ ] Lida com o dia carregado pela metade e com um intervalo que inclui dias sem evento
- [ ] Falha de forma legível, e não em silêncio nem com stack trace cru
- [ ] Outra pessoa consegue rodar um backfill de um novo intervalo sem ler o código todo

### 5. Higiene

- [ ] Nenhuma credencial, chave, token ou dado de cliente no repositório **ou no histórico**
- [ ] Histórico de commits legível
- [ ] Sem arquivos mortos ou sobras de tentativa

> A primeira linha da dimensão 5 é eliminatória. Segredo commitado reprova sem revisão de mérito, e a orientação é **rotacionar a credencial** — apagar o arquivo não resolve, o histórico guarda.

---

## O que **não** é avaliado

- Escolha de linguagem, biblioteca ou engine (pandas, DuckDB, SQL puro, Spark…) — resolva do jeito que você domina
- Elegância estética do código
- Volume de código — uma transformação curta que re-roda sem medo vale mais que um framework longo
- Velocidade de entrega, dentro do prazo
