# 06 · Investimentos e Trade-offs (Visão Executiva)

| Versão | Data | Autor | Revisão |
|--------|------|-------|---------|
| 1.0 | [A PREENCHER] | Durval | Inicial |

---

## 1. Como eu defendo cada investimento

O case pede **visão de investimento relativo, custo-benefício e complexidade** — não valores exatos de
fornecedor. A lógica de defesa é uma só:

> **Todo investimento se justifica pelo custo da indisponibilidade que ele evita, não pela tecnologia
> em si.** Se uma cirurgia adiada por link caído custa contrato e reputação com um hospital, um link
> redundante que custa uma fração disso **se paga na primeira ocorrência evitada**.

---

## 2. Investimento relativo por frente

Escala: 💲 Baixo · 💲💲 Médio · 💲💲💲 Alto · Complexidade: ⚙️ a ⚙️⚙️⚙️

| Frente | Horizonte | Investimento | Complexidade | Modelo | Retorno principal |
|--------|:---------:|:------------:|:------------:|--------|-------------------|
| MFA + Acesso Condicional | 0–90d | 💲 | ⚙️ | OPEX (licença existente) | Corta o vetor nº 1 de ataque |
| Restauração testada / rotina de backup | 0–90d | 💲 | ⚙️ | OPEX (processo) | Elimina o maior risco silencioso |
| Monitoramento de negócio (Zabbix/Grafana) | 0–90d | 💲 | ⚙️⚙️ | OPEX (open-source) | Reduz MTTD/MTTR; visão de negócio |
| EDR/XDR | 0–90d | 💲💲 | ⚙️ | OPEX | Reduz raio de ransomware |
| Redundância de link Tier 1 | 0–90d | 💲💲 | ⚙️⚙️ | OPEX | Fim do ponto único que para o caixa |
| Segmentação de rede | 0–90d | 💲 | ⚙️⚙️ | CAPEX leve | Contém movimento lateral |
| SD-WAN nacional | 3–9m | 💲💲💲 | ⚙️⚙️⚙️ | CAPEX + OPEX | Padrão, failover e visibilidade central |
| Zero Trust (ZTNA/SASE) | 3–9m | 💲💲 | ⚙️⚙️ | OPEX | Acesso remoto seguro sem VPN legada |
| SIEM centralizado | 3–9m | 💲💲 | ⚙️⚙️⚙️ | OPEX | Detecção e conformidade |
| Backup imutável 3-2-1-1-0 | 3–9m | 💲💲 | ⚙️⚙️ | OPEX/CAPEX | Resiliência anti-ransomware |
| DR completo em nuvem | 9–18m | 💲💲💲 | ⚙️⚙️⚙️ | OPEX | Continuidade real do Tier 1 |
| SOC/MDR 24×7 | 9–18m | 💲💲💲 | ⚙️⚙️ | OPEX | Resposta gerenciada contínua |
| IaC + FinOps | 9–18m | 💲 | ⚙️⚙️ | OPEX | Escala barata + previsibilidade de custo |

> **Leitura executiva:** o gasto pesado (SD-WAN, DR, SOC) fica nas fases 2 e 3 — **depois** de o padrão
> ser validado em piloto. Os primeiros 90 dias entregam a maior redução de risco pelo **menor custo**.

---

## 3. Onde padronizar vs. onde flexibilizar

Esta é a decisão central do case — e a resposta não é "padronizar tudo".

| Domínio | Decisão | Justificativa |
|---------|---------|---------------|
| **Identidade (Entra ID)** | 🔒 Padronizar (nacional) | Um IdP único é a base de segurança e operação remota. Sem exceção. |
| **Baseline de segurança (CIS)** | 🔒 Padronizar (nacional) | A unidade mais fraca define o risco de todas. |
| **Arquitetura de rede/VLANs** | 🔒 Padronizar (nacional) | Mesmo layout em toda unidade = suporte remoto viável e barato. |
| **Backup e política de retenção** | 🔒 Padronizar (nacional) | Conformidade ANVISA/fiscal não admite variação regional. |
| **Orquestração SD-WAN** | 🔒 Padronizar (nacional) | Visibilidade e failover só funcionam com padrão único. |
| **Provedor de última milha** | 🔓 Flexibilizar (regional) | Cobertura varia por cidade; o que importa é atender o SLA. |
| **Breakout de internet** | 🔓 Flexibilizar (local) | Saída local reduz latência e custo, dentro da política SASE. |
| **Tier de redundância** | 🔓 Flexibilizar (por criticidade) | Tier 1 tem dois links; Tier 3 tem link + 4G. Não faz sentido igualar. |

> **Princípio:** padroniza-se **o que reduz risco e custo de escala** (núcleo); flexibiliza-se
> **o que a realidade regional impõe** (borda) — sempre dentro da mesma régua de qualidade.

---

## 4. Trade-offs principais (e como eu decido)

| Trade-off | Opção A | Opção B | Decisão e porquê |
|-----------|---------|---------|------------------|
| Velocidade vs. robustez | Big-bang nacional | Piloto → rollout | **B.** Piloto reduz risco de execução; um erro em big-bang para o país. |
| CAPEX vs. OPEX | Comprar tudo | Consumir como serviço | **Misto.** OPEX onde há elasticidade (nuvem, SASE); CAPEX onde já amortizado (on-prem core). |
| On-premises vs. nuvem | Tudo local | Tudo nuvem | **Híbrido intencional** (ver framework na arquitetura): núcleo sensível a latência fica local, DR e apps internos vão à nuvem. |
| Open-source vs. comercial | Zabbix, Wazuh | Datadog, Sentinel | **Misto por maturidade.** Open-source no monitoramento (economia); comercial onde suporte e integração pesam (segurança). |
| Redundância vs. custo | Redundar tudo | Redundar por tier | **Por tier.** Redundância total é desperdício; foco na criticidade. |
| Fazer vs. contratar (SOC) | SOC interno | MDR gerenciado | **MDR.** 24×7 interno é inviável com equipe enxuta; MDR entrega cobertura sem headcount. |

---

## 5. Alavancagem do que já existe (economia inteligente)

O maior ganho de custo-benefício vem de **usar melhor o que já está pago**:

- **Microsoft 365 / Entra ID** já licenciado → MFA, Acesso Condicional, SSO e (conforme tier) PIM/PAM
  e Defender **sem novo fornecedor**.
- **Zabbix + Grafana** (open-source) → monitoramento robusto sem licença.
- **Terraform** → automação com ferramenta padrão de mercado, sem custo de licença.

> Isso permite que os 90 dias entreguem alto valor com **desembolso mínimo** — argumento forte diante
> de "apoio da liderança, mas sem autonomia irrestrita de orçamento".

---

## 6. Resumo executivo do investimento

```
Fase 1 (0-90d)   ▐ Investimento BAIXO  ▐ Redução de risco ALTA  → aprovar já
Fase 2 (3-9m)    ▐ Investimento MÉDIO  ▐ Padronização e escala  → aprovar por marcos
Fase 3 (9-18m)   ▐ Investimento ALTO   ▐ Resiliência plena      → aprovar após ganhos das fases 1-2
```

**A defesa em uma frase para a diretoria:**
> "Começamos barato, provando valor e cortando os riscos que mais doem no caixa. Só pedimos os
> investimentos maiores **depois** de mostrar resultado — e cada real é justificado pela
> indisponibilidade que ele evita, com número na mão."

---

**Base de priorização:** [02 · Roadmap](02-priorizacao-e-roadmap.md).
**Riscos que sustentam a urgência:** [07 · Matriz de Riscos](07-matriz-de-riscos.md).
