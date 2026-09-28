# 999 — Harness de avaliação de um agente (FIXTURE DE TESTE)

> ⚠️ **Isto NÃO é uma Mission real.** É um fixture criado para exercitar o pipeline do Reviewer ponta a ponta (Steel Thread, LYTICS-230) enquanto as Missions reais (LYTICS-264) e a rubrica oficial (LYTICS-262) não existem. Pode ser removida sem dó.

## O caso

Um time mantém um agente que responde perguntas sobre uma base de documentos internos. De vez em quando ele responde com confiança uma coisa que não está na base — e ninguém percebe até um usuário reclamar. Hoje não existe nenhuma forma automática de dizer se uma mudança no prompt ou no modelo melhorou ou piorou a qualidade.

## O que se espera de você

Um **harness de avaliação**: um conjunto de casos de teste rodado contra o agente que produz um número de qualidade e **falha (exit code diferente de zero)** quando a qualidade cai abaixo de um limiar que você definir. O objetivo é que esse harness possa rodar num CI e barrar uma regressão antes de ir pro ar.

Não estamos avaliando o agente em si — estamos avaliando o **harness que mede o agente**.

## Restrições

- Roda na máquina de quem revisa com **um comando** (documente qual).
- Não pode depender de serviço pago obrigatório; se usar um modelo, deixe um modo mock/offline para a revisão rodar sem chave.

## Tempo estimado

Faixa honesta: 3 a 6 horas. É a primeira turma; o tempo será calibrado.

## Como entregar

Ver [`ENTREGA.md`](../../ENTREGA.md) na raiz.

## Critérios de aceite

Ver [`CRITERIOS.md`](CRITERIOS.md), nesta pasta. **Leia antes de começar.**
