# it-operations-cases

Estudos de caso de operação e infraestrutura de TI, escritos a partir de trabalho
real em produção — não de laboratório.

Cada caso tem um número medido, a decisão técnica que o produziu, **as
alternativas que foram descartadas e por quê**, e o que eu faria diferente. Essa
terceira parte é o ponto: relatar o que deu certo é fácil, e sozinho não diz nada
sobre como alguém pensa.

---

## Os casos

### 1. [Governança de licenciamento Microsoft 365](casos/01-governanca-licenciamento-m365.md)

**R$ 30.682/ano capturados** em 51 contas tratadas e verificadas; R$ 43.212/ano
adicionais identificados e ainda pendentes de decisão.

Uma auditoria em tenant de ~1.900 caixas. O trabalho não foi contar licenças —
foi separar 249 alertas iniciais em 55 candidatas reais, e provar que 8 de 11
"demitidos licenciados" estavam trabalhando naquele dia. Inclui o defeito de
processo que a medição revelou: um offboarding executado 45 vezes que nunca
removeu ninguém das listas de distribuição.

E inclui o incidente que veio três semanas depois, em que uma operação em massa
no mesmo terreno apagou 1,18 milhão de itens em 732 caixas.

### 2. [Ruído de alerta em monitoramento](casos/02-ruido-de-alerta-monitoramento.md)

**396 de 418 problemas ativos — 94,7% — tinham causa única.**

Uma investigação que começou com um alerta e terminou descobrindo que o
monitoramento fabricava a maior parte da própria fila. A aplicação quebrada que o
alerta apontava era a geradora do ruído que a escondia.

### 3. [Migração de runtime de containers sem downtime](casos/03-migracao-docker-ce.md)

**13 containers migrados, zero perda comprovada por diferença de conjuntos.**

O problema real não era o runtime: era que a produção inteira só subia quando uma
pessoa específica fazia login. Uma tentativa fracassada com rollback, duas rotas
de rede testadas e descartadas, oito dias perdidos num bug de contas homônimas —
e um cutover que acabou se executando sozinho, em produção, sem intervenção.

---

## Capturado × diagnosticado

A distinção aparece no cabeçalho de cada caso, e vale explicar o critério.

| Caso | Situação |
|---|---|
| 1 — Licenciamento | **Remediação executada e verificada.** Parte da economia segue identificada e pendente. |
| 2 — Ruído de alerta | **Diagnóstico apenas.** A correção foi proposta e priorizada; nunca foi aprovada nem aplicada. O ganho projetado não foi medido. |
| 3 — Migração | **Remediação concluída e validada**, com ausência de perda demonstrada por diferença de conjuntos. |

Custo *identificado* é análise. Custo *capturado* é execução verificada. Misturar
os dois infla o número e destrói a credibilidade do resto — então eles aparecem
separados, inclusive quando isso deixa o resultado menor.

## O que cada caso contém

```
problema  →  contexto  →  alternativas descartadas  →  decisão
          →  implementação  →  resultado medido  →  o que eu faria diferente
```

A seção de **alternativas descartadas** é obrigatória. É onde a decisão técnica
de fato acontece, e é o que separa um relato de execução de um raciocínio de
arquitetura. "Usei X" não informa nada; "avaliei X, Y e Z, escolhi Y por causa
disto, aceitando este risco" informa tudo.

Os diagramas mostram mecanismo — como uma coisa causa outra — e não organograma.
Onde uma frase bastaria, está escrita a frase.

## Sobre a sanitização

Os casos vêm de ambiente corporativo real. Razão social, domínios, hostnames,
IPs, identificadores de objeto, valores de contrato de fornecedor e nomes de
pessoas foram removidos ou generalizados.

**Os números agregados são reais** e não foram arredondados para ficarem
melhores. Onde um número é projeção e não medição, está dito.

## Ferramentas relacionadas

Parte do código que produziu o caso 1 está em
**[powershell-toolkit](https://github.com/anondaniel/powershell-toolkit)** —
auditoria de caixas, offboarding em quatro etapas com dry-run por padrão, e
varredura de conflitos de sincronização.

---

**Daniel Figueira** · Coordenador de TI
[linkedin.com/in/danielmaranhaofigueira](https://linkedin.com/in/danielmaranhaofigueira)

Textos sob [CC BY 4.0](LICENSE).
