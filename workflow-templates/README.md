# Workflow templates

Starter workflows oferecidos aos repositórios da organização. Aparecem na aba
**Actions → New workflow** de qualquer repositório de `br-com-zoov`, na seção
"Workflows da organização".

> Disponíveis para toda a organização porque este repositório se chama `.github`
> e é público. Ver [Como o GitHub aplica estes arquivos](../README.md#como-o-github-aplica-estes-arquivos).

## Disponíveis

| Template | Para que serve |
|---|---|
| `ci-node-nest.yml` | Backend NestJS: lint, formatação, typecheck, testes unitários e e2e com Postgres, build |
| `ci-node-next.yml` | Frontend Next.js: lint, typecheck, testes e build com cache do `.next` |
| `ci-python.yml` | Ruff (lint e formatação) e pytest em Python 3.11 e 3.12 |
| `ci-dart-flutter.yml` | Flutter: formatação, analyze, testes com cobertura, build Android e Web |
| `codeql.yml` | Análise estática de segurança, por PR e semanal |
| `dependency-review.yml` | Bloqueia PRs com dependência vulnerável ou licença incompatível |

Os quatro templates de CI usam o nome de workflow `CI`, então um repositório
adota **um** deles. Repositório monorepo com backend e frontend: copie os dois e
renomeie os arquivos e o campo `name`.

## Adicionando um template

Cada template são **dois arquivos** com o mesmo nome-base:

- `<nome>.yml` — o workflow. Use o placeholder `$default-branch`; o GitHub o
  substitui pela branch padrão do repositório que adotar o template.
- `<nome>.properties.json` — metadados (`name`, `description`, `iconName`,
  `categories`, `filePatterns`).

O workflow `validate` falha se um dos dois faltar.

## Política de actions

- Actions de `actions/*` e `github/*` podem usar tag de major (`@v4`).
- **Qualquer action de terceiro precisa ser fixada por SHA completo**, com a
  versão em comentário ao lado. Nenhum template atual usa action de terceiro —
  é por isso que `ci-dart-flutter.yml` instala o SDK clonando
  `flutter/flutter` em vez de usar uma action pronta de terceiro.
- O Dependabot **não** atualiza os arquivos deste diretório. Quando ele abrir PR
  subindo uma action em `.github/workflows/`, replique a versão aqui.
