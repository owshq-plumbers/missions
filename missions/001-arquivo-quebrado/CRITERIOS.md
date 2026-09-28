# Critérios de aceite — Mission 001 (O arquivo que chega quebrado)

Estes critérios são **públicos e completos**. Não existe critério secreto: o que decide a revisão está escrito aqui.

O que fica no repositório privado é o *gabarito* — a solução de referência e as notas de quem revisa. Isso é separado pelo mesmo motivo que uma prova tem gabarito à parte.

> **Nível: Fácil.** As dimensões abaixo são as mesmas em toda Mission. O que muda entre níveis é a altura da barra dentro delas — aqui pede-se o essencial de cada uma. Missions mais difíceis sobem essa barra (ex.: em "aguenta a realidade", uma difícil pediria idempotência e observabilidade; aqui, tratar o arquivo vazio e falhar legível já atende).

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

O portão decide **entrada de arquivo** contra o esquema combinado — não vira um limpador de dados nem um validador genérico que ignora o caso.

- [ ] O que o portão checa sai do `esquema.md` (colunas, tipos, chave, obrigatoriedade), não de regras inventadas fora do combinado
- [ ] Está escrito o que conta como "arquivo que pode entrar" versus "arquivo barrado"
- [ ] O que ficou fora de escopo está dito (ex.: "não corrijo o arquivo, só barro")

### 2. A solução funciona e dá para verificar

- [ ] Um comando documentado roda o portão sobre um arquivo
- [ ] Passa nos arquivos bons e **barra** os quebrados — e barra pelo motivo certo, não por acaso
- [ ] Barrou → sai com **código diferente de zero** e mensagem legível dizendo qual regra quebrou e onde
- [ ] Roda a partir do README, sem conhecimento tácito e sem chave

### 3. As decisões estão justificadas

A parte que mais separa níveis. Não é sobre acertar a escolha — é sobre saber por que escolheu.

- [ ] Está escrito **por que** cada regra é bloqueante ou só um aviso (ex.: coluna faltando barra; coluna extra talvez só avise)
- [ ] Aparece ao menos uma alternativa descartada com o porquê (ex.: "usei checagem própria em vez de biblioteca X porque…")
- [ ] Os trade-offs assumidos estão nomeados (ex.: "rejeito o arquivo inteiro em vez de dropar as linhas ruins, porque…")

### 4. Aguenta a realidade

- [ ] Trata os tipos de quebra que os arquivos de exemplo sugerem, incluindo o arquivo vazio
- [ ] Falha de forma legível, e não em silêncio nem com stack trace cru
- [ ] Está dito como adicionar uma regra nova quando o parceiro mudar o formato de novo — outra pessoa consegue mexer nisso depois

### 5. Higiene

- [ ] Nenhuma credencial, chave, token ou dado de cliente no repositório **ou no histórico**
- [ ] Histórico de commits legível
- [ ] Sem arquivos mortos ou sobras de tentativa

> A primeira linha da dimensão 5 é eliminatória. Segredo commitado reprova sem revisão de mérito, e a orientação é **rotacionar a credencial** — apagar o arquivo não resolve, o histórico guarda.

---

## O que **não** é avaliado

- Escolha de linguagem, biblioteca ou framework — resolva do jeito que você domina
- Elegância estética do código
- Volume de código — um portão curto que barra o arquivo certo vale mais que um framework longo
- Velocidade de entrega, dentro do prazo
