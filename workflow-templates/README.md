# Workflow templates

Starter workflows oferecidos aos repositórios da organização. Aparecem na aba
**Actions → New workflow** de qualquer repositório de `br-com-zoov`, na seção
"Workflows da organização".

> Só aparecem quando este repositório se chama `.github`. Ver a seção
> [Como o GitHub aplica estes arquivos](../README.md#️-como-o-github-aplica-estes-arquivos).

## Disponíveis

| Template | Para que serve |
|---|---|
| `ci-node.yml` | Lint, typecheck, testes e build em Node 20 e 22 |
| `ci-python.yml` | Ruff e pytest em Python 3.11 e 3.12 |
| `codeql.yml` | Análise estática de segurança, por PR e semanal |
| `dependency-review.yml` | Bloqueia PRs com dependência vulnerável ou licença incompatível |

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
  versão em comentário ao lado.
- O Dependabot **não** atualiza os arquivos deste diretório. Quando ele abrir PR
  subindo uma action em `.github/workflows/`, replique a versão aqui.
