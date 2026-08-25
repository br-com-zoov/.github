# `br.com.zoov.core.plataforma.governanca..github`

Repositório de **governança** da organização Zoov. É a fonte da verdade dos
arquivos de saúde da comunidade (*community health files*), dos templates de
issue/PR e dos templates de workflow usados por todos os repositórios da org.

> **Namespace:** `br.com.zoov` · **Domínio:** `core` · **Subdomínio:** `plataforma` ·
> **Componente:** `governanca`

---

## ⚠️ Como o GitHub aplica estes arquivos

O GitHub só usa um repositório como fonte de *defaults* de organização quando ele
se chama **exatamente `.github`**. Este repositório segue a convenção de nomes
Zoov (`br.com.zoov.core.plataforma.governanca..github`) e, portanto, **não é lido
automaticamente pelo GitHub**.

Por isso o repositório trabalha em dois modos:

| Modo | Como funciona | Estado |
|---|---|---|
| **Defaults de organização** | O layout deste repo é idêntico ao de um `.github` oficial. Renomeie-o para `.github` (ou espelhe o conteúdo em `br-com-zoov/.github`) e todos os defaults passam a valer para a org inteira. | Pendente da decisão de rename |
| **Sync explícito** | O workflow [`sync-health-files.yml`](.github/workflows/sync-health-files.yml) abre PRs em repositórios-alvo listados em [`sync/targets.txt`](sync/targets.txt), copiando os arquivos de governança. | Ativo (manual) |

O modo *sync* existe justamente para cobrir o intervalo em que o rename ainda não
aconteceu — e continua útil depois, para repositórios que precisam dos arquivos
versionados localmente.

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
4. Após o merge, rode o workflow **Sync health files** para propagar as mudanças
   aos repositórios listados em `sync/targets.txt`.

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
| Alvos do sync | [`sync/targets.txt`](sync/targets.txt) | Lista vazia — o workflow não faz nada até ser preenchida |
| Token do sync | Segredos do repositório | Criar `ZOOV_GOVERNANCA_TOKEN` |
| Linguagens do CodeQL | [`workflow-templates/codeql.yml`](workflow-templates/codeql.yml) | A matriz vem com `javascript-typescript` |
| Rename para `.github` | Configurações do repositório | Decisão pendente — ver tabela acima |

---

Mantido pela equipe de Plataforma — ver [`CODEOWNERS`](.github/CODEOWNERS).
