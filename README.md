# Distribuidora-de-OPME
Case técnico de infraestrutura de TI para distribuidora nacional de OPME — diagnóstico, arquitetura-alvo, plano de 90 dias e governança. Estabilizar → Padronizar → Evoluir.

> **Estabilização e Evolução da Infraestrutura Corporativa — Horizonte 6 a 18 meses**
> Case técnico-executivo para posição de **Especialista de Infraestrutura de TI**.
---
📌 Sobre este repositório
Este repositório documenta, de ponta a ponta, a resposta a um case de infraestrutura de TI
para uma distribuidora de OPME (Órteses, Próteses e Materiais Especiais) com operação nacional.
O desafio: chegar como especialista de infraestrutura e apresentar à gerência de tecnologia uma
proposta de estabilização e evolução do ambiente corporativo, equilibrando criticidade, custo,
prazo, risco e capacidade de execução, com forte tradução de infraestrutura em impacto de negócio.
O material foi estruturado como projeto real, seguindo boas práticas de ITIL 4, e é dividido em
documentos executivos (para a diretoria) e técnicos (para o time de engenharia).
> ℹ️ **Nota sobre dados:** o case não fornece números exatos (unidades, usuários, orçamento). Onde
> necessário, foram assumidas premissas realistas para uma distribuidora de OPME de porte nacional,
> **sempre sinalizadas explicitamente** com o marcador. Substituir por dados reais em
> um cenário de execução.
---
🗂️ Estrutura do repositório
#	Documento	Público	O que responde
00	Sumário Executivo	Diretoria	A proposta em 1 página
01	Diagnóstico do Cenário	Técnico + Executivo	Riscos, fragilidades, dependências e impacto ao negócio
02	Priorização e Roadmap 6–18 meses	Executivo	Curto, médio e longo prazo com critério de priorização
03	Arquitetura-Alvo (TO-BE)	Técnico	Conectividade, rede, identidade, segurança, monitoramento, backup e DR
04	Plano de Ação — Primeiros 90 Dias	Técnico + Executivo	O que atacar primeiro, como medir, resultados esperados
05	Governança Operacional	Técnico + Executivo	KPIs, rituais, RACI, escalonamento, gestão de fornecedores
06	Investimentos e Trade-offs	Executivo	Onde padronizar vs. flexibilizar, CAPEX/OPEX, defesa das escolhas
07	Matriz de Riscos	Técnico + Executivo	Riscos, probabilidade × impacto e mitigação
08	Processos Operacionais (ITIL)	Técnico	Incidente, mudança, disponibilidade, backup/DR, identidade, fornecedores
Diagramas: `docs/diagramas/` — topologia atual (AS-IS), alvo (TO-BE),
conectividade por tier e fluxo de continuidade (Mermaid + orientação para draw.io).
Apresentação: `apresentacao/` — deck executivo (`.pptx`) para a segunda entrevista.
---
🎯 A tese em uma frase
> **Primeiro estabilizar o que para a operação (conectividade crítica, restauração confiável e
> visibilidade de negócio), depois padronizar o que espalha custo e risco (rede, identidade,
> segurança e fornecedores), e só então evoluir para resiliência plena e automação** — nesta ordem,
> porque redundância sem visibilidade é gasto cego, e evolução sobre base instável é retrabalho.
---
🧭 Como ler
Se você é da diretoria: comece pelo Sumário Executivo e pelo
documento de Investimentos e Trade-offs.
Se você é técnico: siga a ordem numérica — diagnóstico → arquitetura → plano 90 dias → processos.
Se você tem 5 minutos: leia o deck em `apresentacao/`.
---
🏗️ Contexto de negócio (por que OPME muda tudo)
Uma distribuidora de OPME não é uma empresa de logística comum. As particularidades do setor elevam
a criticidade da infraestrutura e foram usadas como fio condutor de todas as decisões deste case:
Rastreabilidade regulatória (ANVISA): lote, série, validade e histórico de cada material são
obrigatórios. Perda de dados não é só prejuízo operacional — é não conformidade regulatória.
Consignação hospitalar: grande parte do estoque fica em consignação nos hospitais e é faturado
no uso durante a cirurgia. Sistema indisponível = material não faturado ou cirurgia atrasada.
Faturamento atrelado a procedimento cirúrgico: integrações com hospitais e operadoras (padrões
TISS/TUSS), autorizações e janelas curtas. Indisponibilidade tem impacto direto e imediato em caixa.
Urgência logística: entregas de material cirúrgico têm hora marcada. Um link caído numa unidade
crítica pode significar uma cirurgia adiada.
LGPD + dados sensíveis de saúde: exige segmentação, controle de acesso e trilha de auditoria.
Essas características justificam a régua de alta disponibilidade, continuidade testada e segurança
uniforme que orienta a proposta.
---
📐 Frameworks e padrões de referência
`ITIL 4` · `NIST CSF 2.0` · `CIS Controls v8` · `Backup 3-2-1-1-0` · `Zero Trust (SASE/ZTNA)` ·
`Well-Architected (AWS/Azure)` · `LGPD` · `Boas Práticas de Distribuição ANVISA (RDC 430/2020)`
---
👤 Autor
Durval — Especialista de Infraestrutura de TI
Cloud · Redes Corporativas · Microsoft 365 / Entra ID · AWS · Azure · Segurança · ITIL
> Case desenvolvido como demonstração de raciocínio de arquitetura, priorização e comunicação
> técnico-executiva. Números e nomes são ilustrativos.
