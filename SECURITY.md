# Política de segurança

## Reportando uma vulnerabilidade

**Não abra issue pública** para relatar vulnerabilidade.

Use um destes canais:

1. **GitHub Security Advisory** (preferencial) — aba *Security* → *Report a
   vulnerability* no repositório afetado. Cria um canal privado com os
   mantenedores.
2. **E-mail** — `seguranca@zoov.com.br`, com `[SECURITY]` no assunto.

Inclua no relato:

- Componente e versão afetados (commit, tag ou URL do ambiente).
- Passos para reproduzir.
- Impacto observado ou estimado.
- Sua avaliação de severidade, se tiver.

## Nosso compromisso

| Etapa | Prazo |
|---|---|
| Confirmação de recebimento | 2 dias úteis |
| Avaliação inicial e severidade atribuída | 5 dias úteis |
| Correção de severidade crítica ou alta | 15 dias corridos |
| Correção de severidade média ou baixa | Próximo ciclo de release |

Mantemos você informado do progresso e creditamos a descoberta na publicação do
advisory, salvo pedido em contrário.

## Escopo

Estão no escopo os repositórios sob `github.com/br-com-zoov` e os serviços em
produção operados a partir deles.

Fora de escopo: engenharia social, ataques de negação de serviço, relatos
gerados só por scanner automatizado sem prova de impacto, e vulnerabilidades em
dependências de terceiros já corrigidas upstream (reporte ao projeto de origem).

## Divulgação

Praticamos divulgação coordenada. Pedimos que a publicação aguarde a correção
estar em produção ou 90 dias a partir do relato, o que ocorrer primeiro.

## Segredos vazados

Suspeita de credencial exposta em um repositório: trate como incidente crítico.
Comunique pelo canal acima **antes** de tentar remover o commit — a rotação da
credencial vem primeiro; reescrever o histórico não a invalida.
