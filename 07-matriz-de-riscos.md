# 07 · Matriz de Riscos

| Versão | Data | Autor | Revisão |
|--------|------|-------|---------|
| 1.0 |  | Durval | Inicial |

---

## 1. Método

Avaliação no formato ITIL: **identificar → avaliar (probabilidade × impacto) → mitigar → atribuir dono**.

- **Probabilidade:** Baixa (1) · Média (2) · Alta (3)
- **Impacto:** Baixo (1) · Médio (2) · Alto (3)
- **Nível = Probabilidade × Impacto** → 🟩 Baixo (1–2) · 🟨 Médio (3–4) · 🟧 Alto (6) · 🟥 Crítico (9)

```
IMPACTO
  Alto  │  🟨 3   🟧 6   🟥 9
  Médio │  🟩 2   🟨 4   🟧 6
  Baixo │  🟩 1   🟩 2   🟨 3
        └───────────────────────
           Baixa  Média  Alta   PROBABILIDADE
```

---

## 2. Riscos do ambiente (o que existe hoje)

| ID | Risco | Prob. | Impacto | Nível | Mitigação | Dono |
|----|-------|:-----:|:-------:|:-----:|-----------|------|
| R01 | Perda de dados por backup sem restauração testada (inclui rastreabilidade ANVISA) | 2 | 3 | 🟥 9 | Rotina de restore testado, RPO/RTO, cópia imutável 3-2-1-1-0 | Especialista Infra |
| R02 | Parada de unidade Tier 1 por link único | 3 | 3 | 🟥 9 | Redundância de link + failover SD-WAN | Especialista Infra |
| R03 | Ransomware se alastra por falta de segmentação | 3 | 3 | 🟥 9 | Segmentação, EDR/XDR, MFA, backup imutável | Especialista Infra |
| R04 | Comprometimento de credencial (sem MFA universal) | 3 | 3 | 🟥 9 | MFA 100% + Acesso Condicional + PAM | Especialista Infra |
| R05 | Incidente de segurança em unidade menos protegida | 3 | 2 | 🟧 6 | Baseline CIS nacional uniforme | Especialista Infra |
| R06 | Detecção tardia de incidente (monitoramento reativo) | 3 | 2 | 🟧 6 | Monitoramento de negócio + SIEM + alertas priorizados | Especialista Infra |
| R07 | Custo de nuvem sem governança (dispersão multi-provedor) | 2 | 2 | 🟨 4 | Landing zone + FinOps + consolidação | Gerência TI |
| R08 | Escalonamento lento por fornecedores fragmentados | 3 | 2 | 🟧 6 | Consolidação + SLA + matriz de escalonamento | Gerência TI |
| R09 | Não conformidade LGPD (dados de saúde) | 2 | 3 | 🟧 6 | Segmentação, DLP, controle de acesso, trilha de auditoria | Especialista Infra |
| R10 | Retrabalho ao escalar por falta de arquitetura-alvo | 3 | 2 | 🟧 6 | Framework de decisão + padrão nacional documentado | Especialista Infra |

---

## 3. Riscos de execução do projeto (o que a própria mudança pode causar)

| ID | Risco | Prob. | Impacto | Nível | Mitigação | Dono |
|----|-------|:-----:|:-------:|:-----:|-----------|------|
| E01 | Mudança causa indisponibilidade em unidade crítica | 2 | 3 | 🟧 6 | Janela de manutenção, CAB, plano de rollback pronto | Especialista Infra |
| E02 | Rollout big-bang falha nacionalmente | 1 | 3 | 🟨 3 | Piloto obrigatório antes de escalar | Especialista Infra |
| E03 | Orçamento travado no meio do roadmap | 2 | 2 | 🟨 4 | Fases entregam valor isolado; começar pelo barato | Gerência TI |
| E04 | Resistência dos usuários (MFA, novos processos) | 2 | 1 | 🟩 2 | Comunicação, rollout faseado, suporte reforçado | Especialista Infra |
| E05 | Dependência de operadora atrasa redundância/SD-WAN | 2 | 2 | 🟨 4 | Múltiplos fornecedores; frente não bloqueia demais | Gerência TI |
| E06 | Equipe enxuta sobrecarregada | 2 | 2 | 🟨 4 | Priorização rígida, automação, apoio de fornecedores | Gerência TI |

---

## 4. Riscos que exigem atenção imediata (top 5)

Ordenados por nível e alinhados ao [Plano de 90 Dias](04-plano-90-dias.md):

1. **R01 — Backup sem restauração testada** → Sprint 1/2: auditoria + restore testado + imutabilidade.
2. **R02 — Link único em Tier 1** → Sprint 2: redundância de link.
3. **R03 — Ransomware sem contenção** → Sprint 1–3: MFA + EDR + segmentação.
4. **R04 — Credencial sem MFA** → Sprint 1: MFA universal (quick win).
5. **R06/R08 — Detecção e escalonamento lentos** → Sprint 2–3: monitoramento + matriz de escalonamento.

> Os cinco combinam **alta probabilidade e alto impacto** e são atacados **sem grande investimento** —
> por isso lideram o primeiro trimestre.

---

## 5. Reavaliação

A matriz é revisada:
- **Mensalmente** no Steering de TI (novos riscos, mudança de nível).
- **Após cada incidente P1/P2** (o PIR pode revelar riscos não mapeados).
- **A cada marco de fase** (o que foi mitigado sai; o que emergiu entra).
