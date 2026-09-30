# Critérios de aceite — Mission 003 (O agente que inventa)

Estes critérios são **públicos e completos**. Não existe critério secreto: o que decide a revisão está escrito aqui.

O que fica no repositório privado é o *gabarito* — a solução de referência e as notas de quem revisa. Isso é separado pelo mesmo motivo que uma prova tem gabarito à parte.

> **Nível: Difícil.** As dimensões são as mesmas de toda Mission; o que muda é a altura da barra. Aqui a barra está no teto: não basta um harness que roda (isso é a fácil) nem um que dá o mesmo resultado ao re-rodar (isso é a média) — o harness precisa **medir algo difícil de medir (fidelidade em texto livre) de um jeito confiável**, e provar que pega uma regressão.

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

O que se mede é **fidelidade** — acertar o que está na base e **recusar o que não está** — não "respondeu alguma coisa".

- [ ] Está escrito o que conta como qualidade aqui, e por que recusar uma pergunta fora da base é acerto, não falha
- [ ] O harness avalia o conjunto de respostas contra os casos, não o agente em abstrato
- [ ] O que ficou fora de escopo está dito

### 2. A solução funciona e dá para verificar

- [ ] Um comando documentado, pronto pra CI, roda o harness sobre um conjunto de respostas
- [ ] Produz um número e **sai com código diferente de zero** abaixo do limiar
- [ ] **Distingue os dois conjuntos**: aprova o melhor e reprova o pior (é o teste central — um harness que aprova os dois, ou reprova os dois, não mede nada)
- [ ] Rodar duas vezes no mesmo conjunto dá o **mesmo veredito** (determinístico)
- [ ] Roda offline, sem chave, a partir do README

### 3. As decisões estão justificadas

A parte que mais separa níveis — e numa difícil, o centro de gravidade.

- [ ] Está escrito **como** a qualidade de uma resposta é medida (match de fatos, similaridade, LLM-juiz, regra…) e **por quê**, com os **modos de falha** dessa escolha nomeados
- [ ] O **limiar** é defendido — por que esse número, o que ele deixa passar e o que barra
- [ ] O problema de **quem julga o juiz** é enfrentado (se usou um modelo pra avaliar, como você confia nele; se usou regra, o que ela não pega)
- [ ] Aparece ao menos uma alternativa de medição descartada, com o porquê

### 4. Aguenta a realidade

- [ ] Lida com não-determinismo (semente, cache ou agregação) para o veredito não oscilar
- [ ] Trata um caso que o medidor não consegue julgar com confiança, em vez de fingir certeza
- [ ] A saída diz **quais casos** puxaram a nota pra baixo — dá pra agir, não só um número
- [ ] Está dito como adicionar um caso novo; outra pessoa consegue estender

### 5. Higiene

- [ ] Nenhuma credencial, chave, token ou dado de cliente no repositório **ou no histórico**
- [ ] Histórico de commits legível
- [ ] Sem arquivos mortos ou sobras de tentativa

> A primeira linha da dimensão 5 é eliminatória. Segredo commitado reprova sem revisão de mérito, e a orientação é **rotacionar a credencial** — apagar o arquivo não resolve, o histórico guarda. (Harness de agente é onde chave de API mais vaza — atenção redobrada.)

---

## O que **não** é avaliado

- Escolha de linguagem, biblioteca ou framework de eval — resolva do jeito que você domina
- Ter usado ou não um LLM como juiz — os dois caminhos podem atender, o que importa é a justificativa e a confiabilidade
- Elegância estética do código
- Volume de código — um harness curto e confiável vale mais que um framework longo e frouxo
- Velocidade de entrega, dentro do prazo
