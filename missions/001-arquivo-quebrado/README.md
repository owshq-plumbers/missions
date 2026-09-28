# 001 — O arquivo que chega quebrado

## O caso

Todo dia de manhã cedo cai um arquivo na pasta de um time de dados: o extrato de pedidos que um parceiro exporta e manda por FTP. Um job pega esse arquivo, carrega numa tabela, e essa tabela alimenta o relatório de vendas que a diretoria olha antes das 9h.

Umas poucas vezes por mês o arquivo vem diferente do combinado — uma coluna a menos, a data em outro formato, linhas repetidas, o encoding trocado, ou às vezes o parceiro exporta o arquivo vazio por erro dele. O job carrega assim mesmo. O número do relatório sai errado, ninguém percebe na hora, e o problema só aparece dias depois quando o financeiro cruza com outra fonte e reclama.

O time está cansado de descobrir tarde. A pergunta que trouxeram é: *dá pra parar o arquivo ruim antes de ele entrar, em vez de limpar a bagunça depois?*

## O que você recebe

Em [`dados/`](dados/):

- Alguns arquivos **bons**, do jeito que o parceiro exporta num dia normal.
- Alguns arquivos **quebrados**, cada um de um jeito diferente (coluna faltando, tipo trocado numa coluna, linhas duplicadas na chave, encoding errado, arquivo vazio). Não está escrito qual é qual — faz parte.
- O **esquema esperado** do arquivo: nomes e tipos das colunas, qual é a chave, o que é obrigatório, e o combinado com o parceiro (`dados/esquema.md`).

## O que se espera de você

Um mecanismo que, dado um arquivo, **decide se ele pode entrar ou não** e **falha de forma barulhenta** quando não pode: sai com código diferente de zero e diz, em linguagem que um humano de plantão às 6h entende, *qual regra quebrou e onde* (qual arquivo, qual coluna, quantas linhas).

Pense nele rodando **antes** da carga — num agendamento ou num CI — como um portão: arquivo bom passa e o job segue; arquivo ruim é barrado e alguém é avisado, em vez de a tabela ser corrompida em silêncio.

Não estamos avaliando o pipeline de carga inteiro. Estamos avaliando **o portão** que decide se o arquivo merece entrar.

## Restrições

- Roda na máquina de quem revisa com **um comando** (documente qual no README).
- Não pode depender de serviço pago nem de nada que precise de chave para rodar.
- Não altere os arquivos de origem em `dados/` — o portão inspeciona, não conserta.

## Tempo estimado

Faixa honesta: **2 a 4 horas.** É a primeira turma; o tempo será calibrado com as entregas.

## Como entregar

Ver [`ENTREGA.md`](../../ENTREGA.md) na raiz.

## Critérios de aceite

Ver [`CRITERIOS.md`](CRITERIOS.md), nesta pasta. **Leia antes de começar.**
