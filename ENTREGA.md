# Como entregar uma Mission

A entrega é **uma issue neste repositório**, apontando para o seu.

## Antes de abrir a issue

- [ ] O seu repositório existe e está **público** (veja abaixo o porquê)
- [ ] O `README.md` do seu repositório explica **o que você fez e por quê** — não apenas como rodar
- [ ] Existe uma forma de reproduzir o resultado (comando, script, notebook, `docker compose`, o que for)
- [ ] Você leu o `CRITERIOS.md` da Mission e checou cada item
- [ ] Nenhuma credencial, chave, token ou dado de cliente foi commitado

> A última linha não é formalidade. Uma entrega com segredo commitado é reprovada sem revisão de mérito — e a orientação é **rotacionar a credencial**, não apenas apagar o arquivo. O histórico do Git guarda o que foi apagado.

## Abrindo a issue

Use o template **Entrega de Mission**. Ele pede:

| Campo | Por quê |
| -- | -- |
| Mission | Qual enunciado você resolveu |
| Link do seu repositório | Onde está o trabalho |
| Commit de referência | Congela o que será avaliado |
| O que você faria diferente com mais tempo | É a parte que mais diz sobre senioridade |
| Onde você travou | Não conta contra você. Ajuda a melhorar o enunciado |

## O seu repositório precisa ser público

A revisão é **automática**: o agente Reviewer lê o seu repositório direto do GitHub para montar o parecer. Ele lê repositórios **públicos** — um repositório privado na sua conta ele não consegue abrir, e a entrega fica parada sem revisão.

Então deixe o seu repositório **público antes de abrir a issue**. Se você prefere trabalhar em privado enquanto desenvolve, tudo bem — é só tornar público na hora da entrega. É a mesma lógica do enunciado: o critério de avaliação é público (`CRITERIOS.md`), a sua solução também.

> Não quer deixar público de jeito nenhum? Diga isso na issue. A revisão vira **manual** — sem o parecer automático e sem a meta de 72h — e alguém do time pede acesso ao seu repositório.

## Prazo de retorno

A meta é **72 horas**. Se passar disso, comente na própria issue.

## Reentrega

Pode. Corrija, aponte o novo commit num comentário da mesma issue e peça nova revisão. Reentrega não é demérito — o Evidence Card registra a versão aprovada, não o número de tentativas.
