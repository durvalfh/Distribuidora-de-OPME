# 00 · Sumário Executivo

| Campo | Valor |
|-------|-------|
| **Projeto** | Estabilização e Evolução da Infraestrutura Corporativa |
| **Empresa** | Distribuidora Nacional de OPME |
| **Horizonte** | 6 a 18 meses (com plano detalhado dos primeiros 90 dias) |
| **Versão** | 1.0 |
| **Data** | [A PREENCHER] |
| **Autor** | Durval — Especialista de Infraestrutura de TI |

---

## O problema, em linguagem de negócio

A infraestrutura hoje **sustenta a operação, mas não a protege**. O ambiente cresceu de forma pontual:
há unidades críticas com um único link de internet, backups sem restauração testada, monitoramento
que avisa tarde, segurança desigual entre as unidades e fornecedores fragmentados. Em uma distribuidora
de OPME — onde **um sistema fora do ar pode adiar uma cirurgia, travar um faturamento ou gerar não
conformidade com a ANVISA** — cada uma dessas fragilidades é um risco direto a **faturamento, logística,
atendimento e continuidade do negócio**.

O problema não é falta de tecnologia. É **falta de padrão, de previsibilidade e de resiliência testada**.

---

## A proposta, em três movimentos

```
┌─────────────────────┐   ┌─────────────────────┐   ┌─────────────────────┐
│  1. ESTABILIZAR     │   │  2. PADRONIZAR      │   │  3. EVOLUIR         │
│  0–90 dias          │──▶│  3–9 meses          │──▶│  9–18 meses         │
│                     │   │                     │   │                     │
│ Parar o sangramento │   │ Reduzir custo e     │   │ Resiliência plena,  │
│ nas unidades        │   │ risco recorrente    │   │ automação e         │
│ críticas            │   │ com um padrão único │   │ maturidade contínua │
└─────────────────────┘   └─────────────────────┘   └─────────────────────┘
```

1. **Estabilizar (0–90 dias):** redundância de conectividade nas unidades críticas, restauração de
   backup testada de verdade, monitoramento correlacionado ao negócio, MFA e EDR em toda a base.
   *Objetivo: acabar com as indisponibilidades que doem no caixa.*

2. **Padronizar (3–9 meses):** arquitetura única de rede (SD-WAN), identidade centralizada (Entra ID +
   Zero Trust), segurança uniforme nacional, backup imutável, consolidação de fornecedores com SLA.
   *Objetivo: transformar exceções caras em padrão barato e replicável.*

3. **Evoluir (9–18 meses):** DR pleno para sistemas críticos, automação (IaC), FinOps de nuvem e
   melhoria contínua sustentada por indicadores.
   *Objetivo: crescer e abrir novas unidades sem reinventar a roda.*

---

## O que a diretoria ganha

| Antes | Depois |
|-------|--------|
| Unidades críticas com link único | Redundância padronizada por criticidade |
| "Temos backup" (sem certeza de restaurar) | Restauração testada em rotina, com RPO/RTO definidos |
| Monitoramento reativo, sem contexto | Visibilidade de **serviços de negócio**, não só de servidores |
| Segurança desigual entre unidades | Baseline nacional uniforme (CIS/NIST) |
| Vários fornecedores, escalonamento lento | Contratos consolidados, SLA e ponto único de escalonamento |
| Custo imprevisível e disperso | Previsibilidade (OPEX padronizado) e defesa de cada investimento |

---

## Indicadores-alvo (primeiros 90 dias)

| Indicador | Situação típica hoje | Meta 90 dias |
|-----------|----------------------|--------------|
| Disponibilidade de serviços críticos (Tier 1) | Sem medição confiável | ≥ 99,5% medido |
| Unidades críticas com redundância de link | Parcial / ad-hoc | 100% das Tier 1 |
| Backups críticos com **restauração testada** | Próximo de 0% | 100% dos sistemas Tier 1 |
| Cobertura de MFA | Parcial | 100% dos usuários |
| Cobertura de EDR | Parcial | ≥ 95% dos endpoints/servidores |
| Tempo médio de detecção (MTTD) | Alto / desconhecido | Baseline medido + queda de ≥ 40% |

---

## Investimento e postura

A proposta **prioriza quick wins de baixo custo** nos primeiros 90 dias (muitos já cabem em licenças
existentes de Microsoft 365/Entra ID) e reserva os investimentos maiores (SD-WAN nacional, DR em nuvem)
para as fases 2 e 3, **já com o padrão validado em piloto**. Padroniza-se onde reduz risco e custo de
escala (conectividade, identidade, segurança, backup) e flexibiliza-se onde a realidade regional exige
(provedores de última milha, breakout local).

> **Princípio de defesa das escolhas:** cada investimento é justificado pelo **custo da indisponibilidade
> evitada**, não pela tecnologia em si. Redundância numa unidade Tier 1 se paga na primeira cirurgia
> que deixa de ser adiada.

---

**Próximo passo:** aprovar o [Plano de 90 Dias](04-plano-90-dias.md) e a estrutura de
[Governança](05-governanca-operacional.md) para dar partida com resultados medíveis já no primeiro trimestre.
