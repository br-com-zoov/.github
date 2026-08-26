# `.github`

Repositório de **governança** da organização Zoov. É a fonte da verdade dos
arquivos de saúde da comunidade (*community health files*), dos templates de
issue/PR e dos starter workflows usados por todos os repositórios da org.

> **Componente:** `core.plataforma.governanca` — o nome do repositório é
> `.github` porque é um nome reservado pelo GitHub. Ver a
> [exceção na convenção de nomes](docs/convencoes.md#nome-de-reposit%C3%B3rio).

---

## Como o GitHub aplica estes arquivos

Por se chamar exatamente `.github`, este repositório é a fonte de *defaults* da
organização `br-com-zoov`. O GitHub aplica cada arquivo automaticamente:

| O que | Como chega nos outros repositórios |
|---|---|
| `profile/README.md` | Vira a página pública de [github.com/br-com-zoov](https://github.com/br-com-zoov) |
| `CONTRIBUTING.md`, `SECURITY.md`, `SUPPORT.md`, `CODE_OF_CONDUCT.md` | Herdados por qualquer repositório da org que não tenha o seu próprio |
| `.github/ISSUE_TEMPLATE/`, `.github/PULL_REQUEST_TEMPLATE.md` | Templates padrão ao abrir issue ou PR em repositórios sem template local |
| `workflow-templates/` | Aparecem em **Actions → New workflow**, seção "Workflows da organização" |

O repositório precisa continuar **público** para que os defaults valham em
repositórios públicos e para que o perfil da org seja visível.

### Quando o sync ainda é necessário

A herança do GitHub é *virtual*: o arquivo não existe no repositório que o
herda, e some assim que ele cria o seu próprio. Para os casos em que o arquivo
precisa estar versionado localmente — auditoria, repositório com
`CONTRIBUTING.md` próprio que deve permanecer alinhado, ferramenta que lê o
arquivo do disco — o workflow
[`sync-health-files.yml`](.github/workflows/sync-health-files.yml) abre PRs nos
repositórios listados em [`sync/targets.txt`](sync/targets.txt).

Se você só quer a herança automática, não precisa preencher `targets.txt`.

---

## 📁 Estrutura

```
.
├── profile/
│   └── README.md              # Perfil público da organização (github.com/br-com-zoov)
├── .github/
│   ├── ISSUE_TEMPLATE/        # Templates de issue padrão da org
│   │   ├── config.yml
│   │   ├── bug.yml
│   │   ├── feature.yml
│   │   └── tarefa-tecnica.yml
│   ├── workflows/             # CI deste repositório
│   │   ├── validate.yml
│   │   └── sync-health-files.yml
│   ├── CODEOWNERS
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── dependabot.yml
├── workflow-templates/        # Starter workflows oferecidos aos repos da org
│   ├── ci-node-nest.yml
│   ├── ci-node-next.yml
│   ├── ci-python.yml
│   ├── ci-dart-flutter.yml
│   ├── codeql.yml
│   └── dependency-review.yml
├── sync/
│   ├── targets.txt            # Repositórios que recebem os arquivos de governança
│   └── files.txt              # Arquivos propagados pelo sync
├── docs/
│   └── convencoes.md          # Nomes de repo, branch e commit
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── GOVERNANCE.md
├── SECURITY.md
└── SUPPORT.md
```

Os arquivos de saúde da comunidade ficam na **raiz** — o GitHub aceita raiz,
`.github/` ou `docs/`, e a raiz é a convenção mais legível.

---

## 🚀 Uso

### Alterar um padrão da organização

1. Abra uma branch a partir de `main` (ver [convenções](docs/convencoes.md)).
2. Edite o arquivo correspondente.
3. Abra um PR. O workflow `validate` checa a sintaxe YAML e a consistência dos
   templates.
4. Após o merge, a mudança já vale para toda a org por herança. Se houver
   repositórios em `sync/targets.txt`, rode o workflow **Sync health files**
   para propagar a cópia local deles.

### Adicionar um repositório ao sync

Inclua o nome dele em [`sync/targets.txt`](sync/targets.txt). O sync abre um PR —
nunca faz push direto na branch padrão do alvo.

---

## 🔐 Segredos necessários

| Segredo | Escopo | Usado por |
|---|---|---|
| `ZOOV_GOVERNANCA_TOKEN` | PAT fine-grained ou token de GitHub App com `contents: write` e `pull_requests: write` nos repositórios-alvo | `sync-health-files.yml` |

O `GITHUB_TOKEN` padrão não serve: ele não tem permissão fora deste repositório.

---

## ✅ Pendências de configuração

O boilerplate usa valores de referência que precisam ser confirmados antes de
valer como padrão da organização:

| Item | Onde | O que confirmar |
|---|---|---|
| Times do GitHub | [`.github/CODEOWNERS`](.github/CODEOWNERS) | `@br-com-zoov/plataforma`, `@br-com-zoov/tech-leads` e `@br-com-zoov/seguranca` precisam existir na org — time inexistente faz a regra ser ignorada em silêncio |
| E-mail de segurança | [`SECURITY.md`](SECURITY.md) | `seguranca@zoov.com.br` |
| E-mail de conduta | [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) | `conduta@zoov.com.br` |
| Canal de suporte | [`SUPPORT.md`](SUPPORT.md) | `#plataforma-suporte` no Slack |
| SLAs | [`SECURITY.md`](SECURITY.md), [`SUPPORT.md`](SUPPORT.md) | Prazos de resposta e correção |
| Alvos do sync | [`sync/targets.txt`](sync/targets.txt) | Lista vazia — opcional, só para repositórios que precisam dos arquivos versionados localmente |
| Token do sync | Segredos do repositório | Criar `ZOOV_GOVERNANCA_TOKEN` |
| Linguagens do CodeQL | [`workflow-templates/codeql.yml`](workflow-templates/codeql.yml) | A matriz vem só com `javascript-typescript`; repositórios Python precisam adicionar `python`. O CodeQL não analisa Dart |

---

Mantido pela equipe de Plataforma — ver [`CODEOWNERS`](.github/CODEOWNERS).
