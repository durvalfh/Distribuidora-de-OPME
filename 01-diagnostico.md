# 01 · Diagnóstico do Cenário

| Versão | Data | Autor | Revisão |
|--------|------|-------|---------|
| 1.0 |  | Durval | Inicial |

---

## 1. Objetivo do diagnóstico

Ler o ambiente atual sob a ótica de **risco ao negócio** — não apenas de deficiências técnicas.
Cada fragilidade abaixo é traduzida em **impacto sobre faturamento, logística, atendimento e
continuidade**, porque é assim que a diretoria decide onde investir primeiro.

> ⚙️ **Método:** as fragilidades vêm do cenário-base do case. A leitura de impacto usa o contexto
> específico de OPME (rastreabilidade ANVISA, consignação, faturamento por procedimento). As premissas
> de dimensionamento estão marcadas com `» Premissa`.

---

## 2. Premissas de dimensionamento

> `» Premissa` — Assumidas para tornar a proposta concreta. Substituir por inventário real na execução.

| Dimensão | Premissa assumida |
|----------|-------------------|
| Unidades | ~15 a 25 (matrizes, filiais e centros de apoio) em quase todas as regiões |
| Usuários | ~800 a 1.500 (corporativo + operação + desenvolvimento interno) |
| Sistemas críticos | ERP/WMS de distribuição, faturamento, portal de pedidos, integrações TISS/hospitais |
| Nuvem | Múltiplos provedores em uso (parte de dev e sistemas internos), sem landing zone formal |
| Identidade | Base Microsoft 365 / Entra ID já existente (ponto de alavancagem) |
| Equipe de TI | Enxuta, sem suporte in-loco na maioria das unidades |

---

## 3. Classificação de criticidade das unidades

Toda priorização deste case parte de classificar as unidades em **tiers**, porque tratar tudo como
igual é o que gera desperdício e cegueira. Critério: impacto no faturamento + volume operacional +
dependência de terceiros (hospitais).

| Tier | Perfil | Exemplo | Régua de disponibilidade |
|------|--------|---------|--------------------------|
| **Tier 1 — Crítica** | Alto faturamento, hub logístico, integração direta com hospitais | Matrizes regionais, CDs principais | Alta — redundância obrigatória |
| **Tier 2 — Importante** | Operação relevante, mas com alternativas de contorno | Filiais médias | Média — redundância recomendada |
| **Tier 3 — Apoio** | Baixo volume, função de apoio | Centros de apoio, escritórios pequenos | Padrão — link único aceitável com contingência simples |

---

## 4. Fragilidades identificadas e impacto ao negócio

### 4.1 Conectividade sem padrão e sem redundância nas unidades críticas

- **O que é:** unidades críticas operando com **link único**; outras com redundância parcial, sem
  padrão de arquitetura definido.
- **Impacto ao negócio:** a queda de um único link numa unidade Tier 1 **para a operação inteira**
  daquela unidade — sem acesso ao ERP não se autoriza, separa ou fatura material cirúrgico. Em OPME,
  isso pode significar **cirurgia adiada, material não faturado e desgaste com o hospital**.
- **Dependência crítica:** provedor único de última milha = ponto único de falha externo.

### 4.2 Ambiente híbrido sem arquitetura-alvo

- **O que é:** mistura de on-premises e nuvem **sem definição formal de arquitetura alvo** nem
  critérios objetivos para decidir entre local, cloud ou híbrido.
- **Impacto ao negócio:** cada decisão vira caso isolado → **custo imprevisível**, dificuldade de
  padronizar, retrabalho a cada nova unidade ou sistema. Impede a diretoria de ter **previsibilidade
  de custo e visão centralizada**.

### 4.3 Backup sem restauração testada

- **O que é:** backups existem, mas a **confiança em restauração e recuperação de desastre é baixa** —
  os testes não seguem rotina madura.
- **Impacto ao negócio:** este é o risco **mais silencioso e mais grave**. "Ter backup" sem restaurar
  testado é ter uma **falsa sensação de segurança**. Em OPME, a perda de dados de rastreabilidade
  (lote/série/validade) é **não conformidade regulatória com a ANVISA**, além de perda fiscal e
  operacional. Um ransomware sem restauração confiável pode **parar a empresa por dias**.

### 4.4 Monitoramento reativo e sem correlação com o negócio

- **O que é:** monitoramento **reativo em parte relevante** do ambiente, com pouca correlação entre
  disponibilidade técnica e impacto no negócio.
- **Impacto ao negócio:** o time descobre o problema **quando o usuário liga reclamando** → MTTD e
  MTTR altos. Pior: não se sabe **qual queda realmente dói**. Um servidor secundário fora do ar pode
  gerar mais alarme do que a integração de faturamento travando.

### 4.5 Sistemas de desenvolvimento interno dispersos (local + múltiplas nuvens)

- **O que é:** sistemas internos com muitos usuários, parte local e parte em **diversos provedores de nuvem**.
- **Impacto ao negócio:** dispersão = **shadow IT**, superfície de ataque ampliada, identidade
  fragmentada, custo de nuvem sem governança (FinOps inexistente) e dificuldade de aplicar segurança
  uniforme.

### 4.6 Segurança pontual e desigual entre unidades

- **O que é:** controles existem em alguns pontos, com **baixa uniformidade nacional, pouca segmentação
  e maturidade desigual**.
- **Impacto ao negócio:** a unidade **menos protegida** define o risco de toda a rede. Sem segmentação,
  um incidente numa filial pequena tem **potencial de se alastrar** (movimento lateral) até os sistemas
  críticos. Somado a dados de saúde (LGPD), o risco é **operacional, regulatório e reputacional**.

### 4.7 Gestão de fornecedores fragmentada

- **O que é:** múltiplos provedores de internet, suporte de sistemas e parceiros regionais, com
  **dificuldade de escalonamento coordenado**.
- **Impacto ao negócio:** durante um incidente, o tempo se perde **descobrindo com quem falar** e
  empurrando responsabilidade entre fornecedores. Sem SLA consolidado, **ninguém é dono do problema**.

---

## 5. Mapa de calor de riscos (visão consolidada)

Escala: 🟥 Crítico · 🟧 Alto · 🟨 Médio

| Fragilidade | Probabilidade de ocorrência | Impacto no negócio | Nível |
|-------------|:---------------------------:|:------------------:|:-----:|
| Backup sem restauração testada | Média | Muito alto | 🟥 Crítico |
| Link único em unidade Tier 1 | Alta | Alto | 🟥 Crítico |
| Segurança desigual / sem segmentação | Alta | Alto | 🟥 Crítico |
| Monitoramento reativo sem contexto | Alta | Médio-alto | 🟧 Alto |
| Ausência de arquitetura-alvo | Certa (já ocorre) | Médio (acumulativo) | 🟧 Alto |
| Fornecedores fragmentados | Alta | Médio | 🟧 Alto |
| Nuvem sem governança / FinOps | Média | Médio | 🟨 Médio |

> A matriz detalhada, com plano de mitigação e responsáveis, está em
> [07 · Matriz de Riscos](07-matriz-de-riscos.md).

---

## 6. Dependências e interações (por que a ordem importa)

Alguns problemas **não podem ser resolvidos isoladamente** — há uma ordem lógica:

- **Monitoramento antes de redundância:** investir em link redundante sem visibilidade é gasto cego.
  Primeiro é preciso **enxergar** onde e quando as quedas acontecem e o que elas afetam.
- **Identidade antes de Zero Trust:** não há como aplicar acesso condicional e ZTNA sem uma
  **identidade centralizada** (Entra ID) como base.
- **Segmentação antes de expandir segurança avançada:** EDR e SIEM rendem muito mais sobre uma rede
  **segmentada**, que limita o raio de um incidente.
- **Padrão de arquitetura antes de escalar:** definir os critérios local/cloud/híbrido **antes** de
  abrir novas unidades evita multiplicar o problema.

Essa cadeia de dependências é o que sustenta o sequenciamento proposto no
[Roadmap](02-priorizacao-e-roadmap.md).

---

## 7. Síntese do diagnóstico

> O ambiente **funciona no dia a dia, mas está exposto**. Os três riscos que exigem ação imediata —
> porque combinam alta probabilidade e alto impacto — são: **(1) restauração de backup não confiável,
> (2) unidades críticas sem redundância e (3) segurança desigual sem segmentação**. Eles formam o
> núcleo do [Plano de 90 Dias](04-plano-90-dias.md). O restante é evolução estruturada, não emergência.
