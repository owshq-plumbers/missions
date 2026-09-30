# 003 — O agente que inventa

## O caso

Um time colocou no ar um agente que responde perguntas sobre a base de documentos internos da empresa — políticas, procedimentos, números. Na maior parte do tempo funciona. Mas de vez em quando ele responde, com toda a confiança do mundo, uma coisa que **não está na base**: inventa um prazo, um valor, um passo que ninguém escreveu. Ninguém percebe na hora — até um usuário agir pela resposta errada.

E tem um problema por baixo desse: toda vez que alguém mexe no prompt ou troca o modelo "pra melhorar", **não existe forma de saber se melhorou ou piorou**. O time está no escuro. Uma mudança que conserta uma pergunta e quebra outras cinco passa despercebida até virar reclamação.

O que trouxeram: *dá pra ter uma forma automática de dizer se uma versão do agente é melhor ou pior que a anterior — e barrar uma regressão antes dela ir pro ar?*

Não estamos avaliando o agente. Estamos avaliando **o harness que mede o agente** — a régua que decide se uma versão pode subir.

## O que você recebe

Em [`dados/`](dados/):

- **A base** (`base/`): alguns documentos internos curtos. É sobre isto que o agente deveria responder — e nada além disto.
- **Os casos** (`casos.jsonl`): um conjunto de perguntas. Parte tem resposta na base; **parte é de propósito fora da base** — nesses, a resposta fiel é *"não sei / não está na base"*, e inventar é o erro.
- **Dois conjuntos de respostas gravadas** (`respostas_v1.jsonl`, `respostas_v2.jsonl`): as respostas de duas versões do agente para os mesmos casos. Uma é melhor que a outra — **sem etiqueta de qual**. Descobrir isso é justamente o trabalho do seu harness.

Trabalhar com respostas gravadas é de propósito: deixa o harness rodar offline, sem chave e sem custo. Se você quiser plugar um agente de verdade depois, deixe a porta aberta — mas o que se avalia roda sobre esses conjuntos.

## O que se espera de você

Um **harness de avaliação** que:

- **Mede a qualidade** de um conjunto de respostas contra os casos — com peso especial em **fidelidade**: acertar o que está na base **e recusar o que não está**. Uma versão que responde bonito mas inventa nas perguntas fora da base é pior, não melhor.
- Produz um número e **falha (exit code diferente de zero)** quando fica abaixo de um limiar que você define e defende — pronto pra rodar num CI e **barrar uma regressão** antes de subir.
- É **confiável o suficiente pra que verde signifique alguma coisa**: rodar duas vezes no mesmo conjunto dá o mesmo veredito. Um harness que às vezes deixa a regressão passar não serve.

O coração da Mission é o problema difícil de verdade: **como medir automaticamente a qualidade de uma resposta em texto livre — e pegar uma alucinação — de um jeito que dê pra confiar.** Match exato não funciona; similaridade é grosseira; usar outro LLM como juiz levanta a pergunta de quem julga o juiz. A escolha é sua; o que se cobra é que ela seja consciente e que você saiba onde ela falha.

## Restrições

- Roda na máquina de quem revisa com **um comando**, pronto pra CI (documente qual).
- **Offline**: sem serviço pago, sem chave. Os conjuntos gravados existem pra isso.
- **Determinístico o suficiente**: o mesmo conjunto tem que dar sempre o mesmo veredito. Se usar algo não-determinístico, controle (semente, cache, agregação) e explique.
- Não altere a base nem os conjuntos de respostas de origem.

## Tempo estimado

Faixa honesta: **8 a 14 horas.** É a primeira turma; o tempo será calibrado com as entregas.

## Como entregar

Ver [`ENTREGA.md`](../../ENTREGA.md) na raiz.

## Critérios de aceite

Ver [`CRITERIOS.md`](CRITERIOS.md), nesta pasta. **Leia antes de começar.**
