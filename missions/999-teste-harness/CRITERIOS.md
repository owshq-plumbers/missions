# Critérios de aceite — Mission 999 (FIXTURE DE TESTE)

Estes critérios são públicos e completos. O que fica no repositório privado é a régua (o gabarito), não a lista.

## Como a revisão lê

Cada dimensão recebe **Atende**, **Atende com ressalva** ou **Não atende**. O veredito final é **aprovado**, **ajustes** ou **reprovado**.

## Dimensões

### 1. O problema foi entendido
- [ ] O harness mede **qualidade/alucinação** do agente, não outra coisa
- [ ] As premissas (o que conta como "certo") estão escritas
- [ ] O que ficou fora de escopo está dito

### 2. A solução funciona e dá para verificar
- [ ] Roda com **um comando** documentado no README
- [ ] Existe um conjunto de casos de teste explícito
- [ ] Há um limiar de qualidade e o processo **falha (exit code != 0)** quando fica abaixo dele
- [ ] Roda sem chave paga (modo mock/offline)

### 3. As decisões estão justificadas
- [ ] Por que essas métricas/casos
- [ ] Por que esse limiar
- [ ] Alternativas descartadas, com o porquê

### 4. Aguenta a realidade
- [ ] Trata caso de borda (resposta vazia, timeout, base sem a resposta)
- [ ] Falha de forma legível
- [ ] Outra pessoa consegue adicionar um caso novo sem ler o código todo

### 5. Higiene
- [ ] Nenhuma credencial, chave, token ou dado de cliente no repositório **ou no histórico**
- [ ] Histórico de commits legível
- [ ] Sem arquivos mortos

> A primeira linha da dimensão 5 é **eliminatória**. Segredo commitado reprova sem revisão de mérito; a orientação é rotacionar a credencial.

## O que não é avaliado
- Escolha de linguagem/framework
- Elegância estética
- Volume de código
