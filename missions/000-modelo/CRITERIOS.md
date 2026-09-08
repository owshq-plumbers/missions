# Critérios de aceite — Mission 000 (modelo)

Estes critérios são **públicos e completos**. Não existe critério secreto: o que decide a revisão está escrito aqui.

O que fica no repositório privado é o *gabarito* — a solução de referência e as notas de quem revisa. Isso é separado pelo mesmo motivo que uma prova tem gabarito à parte.

---

## Como a revisão lê

Cada dimensão recebe um de três estados:

| Estado | Significa |
| -- | -- |
| **Atende** | Faz o que se pede, de forma verificável |
| **Atende com ressalva** | Chega ao resultado, mas com um problema que valeria corrigir |
| **Não atende** | Falta, ou não é possível verificar |

O veredito final é **aprovado**, **ajustes** ou **reprovado**. A regra de composição fica em ⟨ definir ⟩ — não invente uma regra aqui até que ela esteja decidida.

---

## Dimensões

> ⟨ As dimensões abaixo são as candidatas. **Precisam ser confirmadas antes da primeira Mission real.** O jeito de confirmar não é discutir em abstrato: é pegar três entregas — uma que seria aprovada, uma reprovada e uma no limite — e ver quais dimensões de fato separam as três. ⟩

### 1. O problema foi entendido

O que foi entregue responde à pergunta que foi feita, e não a uma pergunta vizinha mais confortável.

- [ ] A entrega ataca o problema do enunciado
- [ ] As premissas assumidas estão escritas
- [ ] O que ficou fora de escopo está dito explicitamente

### 2. A solução funciona e dá para verificar

- [ ] Existe um caminho reproduzível para chegar ao resultado
- [ ] Roda a partir de instruções do README, sem conhecimento tácito
- [ ] O resultado é o que o README afirma que é

### 3. As decisões estão justificadas

A parte que mais separa níveis. Não é sobre acertar a escolha — é sobre saber por que escolheu.

- [ ] As escolhas não óbvias têm motivo escrito
- [ ] Alternativas descartadas aparecem, com o porquê
- [ ] Os trade-offs assumidos estão nomeados

### 4. Aguenta a realidade

- [ ] Trata os casos de borda que o enunciado sugere
- [ ] Falha de forma legível, e não em silêncio
- [ ] Alguém que não é o autor consegue mexer nisso depois

### 5. Higiene

- [ ] Nenhuma credencial, chave, token ou dado de cliente no repositório **ou no histórico**
- [ ] Histórico de commits legível
- [ ] Sem arquivos mortos ou sobras de tentativa

> A primeira linha da dimensão 5 é eliminatória. Segredo commitado reprova sem revisão de mérito, e a orientação é **rotacionar a credencial** — apagar o arquivo não resolve, o histórico guarda.

---

## O que **não** é avaliado

Dizer isso importa tanto quanto dizer o que é.

- Escolha de linguagem ou framework, quando o enunciado não restringe
- Elegância estética do código
- Volume de código — entrega curta que resolve vale mais que longa que impressiona
- Velocidade de entrega, dentro do prazo
