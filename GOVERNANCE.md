# Governança

Como decisões técnicas são tomadas nos repositórios da organização Zoov.

## Papéis

| Papel | Responsabilidade | Como se torna |
|---|---|---|
| **Contribuidor** | Abre issues e PRs | Qualquer pessoa da organização |
| **Mantenedor** | Revisa e aprova PRs, tria issues do repositório | Indicado pelo code owner do domínio |
| **Code owner** | Aprovação obrigatória nos caminhos que lhe pertencem, definidos em `CODEOWNERS` | Time responsável pelo domínio |
| **Plataforma** | Mantém este repositório de governança e os padrões da org | Time de Plataforma |

## Decisões de rotina

Mudanças dentro de um único repositório, sem impacto em contrato público, são
decididas pelos mantenedores daquele repositório via review de PR.

## Decisões estruturais

Precisam de alinhamento explícito antes da implementação:

- Mudança de contrato público (API, evento, schema de banco compartilhado).
- Adoção ou remoção de tecnologia de base (linguagem, framework, banco, broker).
- Mudança em padrão desta organização (qualquer arquivo deste repositório).
- Criação ou depreciação de repositório.

Fluxo:

1. Abra uma issue descrevendo problema, alternativas consideradas e a proposta.
2. Discussão aberta por, no mínimo, 3 dias úteis.
3. Decisão registrada na própria issue pelo code owner do domínio afetado.
4. Decisões de impacto duradouro viram um ADR em `docs/adr/` do repositório
   correspondente.

Empate ou impasse escala para o time de Plataforma, que decide e registra a
justificativa.

## Ciclo de vida de repositório

| Estado | Significado | Sinalização |
|---|---|---|
| `ativo` | Mantido e recebendo mudanças | Padrão |
| `manutenção` | Só correções de bug e segurança | Tópico `maintenance` |
| `depreciado` | Substituído; sem suporte | Tópico `deprecated` + aviso no topo do README |
| `arquivado` | Somente leitura | Repositório arquivado no GitHub |

Depreciar exige apontar o substituto e um prazo de desligamento no README antes
do arquivamento.

## Alterando este documento

Via PR neste repositório, com aprovação do time de Plataforma.
