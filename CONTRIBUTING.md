# Guia de contribuição

Este guia vale para **todos os repositórios da organização Zoov**. Repositórios
podem adicionar regras próprias em seu `CONTRIBUTING.md` local, mas não podem
afrouxar o que está aqui.

## Antes de começar

1. Confirme que existe uma issue ou card descrevendo o trabalho. Mudanças sem
   rastreabilidade só passam em correções triviais (typo, link quebrado).
2. Leia as [convenções](docs/convencoes.md) de nomes de repositório, branch e
   commit.
3. Para mudanças de arquitetura ou de contrato público, alinhe antes de abrir o
   PR — ver [`GOVERNANCE.md`](GOVERNANCE.md).

## Fluxo

```bash
git switch main
git pull --ff-only
git switch -c feat/DEV-123-descricao-curta
# ... trabalho ...
git push -u origin feat/DEV-123-descricao-curta
```

Abra o PR contra `main`. Commits direto em `main` são bloqueados.

## Padrão de branch

`<tipo>/<CARD>-<slug-kebab-case>`

| Tipo | Uso |
|---|---|
| `feat` | Nova funcionalidade |
| `fix` | Correção de bug |
| `chore` | Configuração, tooling, dependências |
| `docs` | Somente documentação |
| `refactor` | Sem mudança de comportamento |
| `hotfix` | Correção crítica em produção |

## Padrão de commit

`<emoji> <tipo>: <assunto no imperativo>`

- Assunto em **inglês**, até 72 caracteres, sem ponto final.
- Corpo (quando o *porquê* não for óbvio) em **português**.
- Um commit por mudança lógica. Nada de `git add .` em árvore suja.

Tabela completa de emojis em [`docs/convencoes.md`](docs/convencoes.md#commits).

## Pull request

Um PR está pronto para review quando:

- [ ] O template de PR está preenchido — nada de seções em branco.
- [ ] CI está verde.
- [ ] O escopo é único. PR que mistura refactor com feature é devolvido.
- [ ] Não há segredo, credencial, token ou dado de cliente no diff.
- [ ] Documentação e testes acompanham a mudança de comportamento.

Aprovação mínima: **1 review** de um code owner. Mudanças em infraestrutura,
autenticação ou movimentação de dinheiro exigem **2**.

Merge por **squash**, mantendo o título do PR como mensagem do commit.

## Review

Quem revisa deve responder três perguntas: o código faz o que o PR diz que faz,
falha de forma segura, e alguém que não participou consegue mantê-lo. Comentário
de review é sobre o código, nunca sobre a pessoa.

## O que não fazer

- Force-push em branch com review em andamento.
- Commit de código comentado, `print`/`console.log` de debug ou arquivos que a
  tarefa não tocou.
- Dependência nova sem justificativa no corpo do PR.
- Action de terceiro sem pin por SHA.
