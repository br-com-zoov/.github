# Convenções

## Nome de repositório

Namespace reverso, tudo em minúsculas, separado por ponto:

```
br.com.zoov.<dominio>.<subdominio>.<componente>
```

| Parte | Regra | Exemplo |
|---|---|---|
| `br.com.zoov` | Fixo. Namespace da organização | — |
| `<dominio>` | Área de negócio ou plataforma | `core`, `produto`, `infra` |
| `<subdominio>` | Capacidade dentro do domínio | `plataforma`, `pagamentos`, `identidade` |
| `<componente>` | Nome do artefato, kebab-case se composto | `governanca`, `gateway-pix` |

Sem acento, sem `_`, sem maiúscula. O nome é imutável depois de criado — renomear
quebra remotes, pipelines e referências de pacote.

**Exceção — nomes reservados:** quando o GitHub exige um nome específico para
que a funcionalidade exista, o nome reservado vence a convenção. É o caso de
[`.github`](https://github.com/br-com-zoov/.github), que só é lido como fonte de
defaults da organização com esse nome exato. O componente lógico
(`core.plataforma.governanca`) fica registrado no README do repositório.

A exceção vale só para nomes que o GitHub reserva — não é uma porta para
encurtar nomes por conveniência.

### Tópicos obrigatórios

Todo repositório declara ao menos: o domínio (`dominio-core`), o estado
(`ativo` / `maintenance` / `deprecated`) e a stack principal (`python`, `node`,
`terraform`, …). Os tópicos são o que torna o inventário da org navegável.

---

## Branch

```
<tipo>/<CARD>-<slug-kebab-case>
```

Exemplos: `feat/DEV-402-migrar-padrao-zoov`, `fix/DEV-511-timeout-webhook`,
`chore/boilerplate-org-github` (sem card, aceito só em trabalho interno de
tooling).

Tipos: `feat`, `fix`, `chore`, `docs`, `refactor`, `test`, `hotfix`, `revert`.

`main` é protegida: sem push direto, sem force-push, review obrigatório, CI
verde como gate.

---

## Commits

```
<emoji> <tipo>: <assunto no imperativo>
```

Assunto em inglês, ≤ 72 caracteres, sem ponto final. Corpo, quando existir, em
português, explicando o **porquê** — o *o quê* já está no diff.

| Emoji | Tipo | Uso |
|---|---|---|
| ✨ | `feat` | Nova funcionalidade |
| 🐛 | `fix` | Correção de bug |
| ♻️ | `refactor` | Sem mudança de comportamento |
| 🔥 | `remove` | Remoção de código ou arquivos |
| 📝 | `docs` | Somente documentação |
| ✅ | `test` | Adiciona ou corrige testes |
| 🎨 | `style` | Formatação, sem lógica |
| ⚡️ | `perf` | Performance |
| 🔒 | `security` | Correção ou endurecimento de segurança |
| ⬆️ | `deps` | Atualização de dependências |
| 🔧 | `chore` | Configuração, tooling |
| 🚀 | `deploy` | CI/CD, release |
| 🗃️ | `db` | Migração, schema |
| 🚑 | `hotfix` | Correção crítica em produção |
| ⏪ | `revert` | Reversão de commit |

Um commit por mudança lógica. Diff misto vira vários commits, com `git add` por
caminho — nunca `git add .`.

---

## Versionamento

[SemVer](https://semver.org/lang/pt-BR/) em tags anotadas: `v1.4.2`.

- `MAJOR` — quebra de contrato público.
- `MINOR` — funcionalidade retrocompatível.
- `PATCH` — correção retrocompatível.

Release é criada a partir da tag, com changelog gerado dos commits desde a tag
anterior.

---

## Código

- **Identificadores** (variáveis, funções, classes, tabelas, colunas, endpoints)
  em **inglês**.
- **Comentários e documentação** em **português**, exceto docstrings de
  bibliotecas públicas.
- Mensagens voltadas ao usuário final em português.

A regra existe para que o código seja legível por ferramentas e por quem vem de
fora, sem que a documentação deixe de servir ao time.
