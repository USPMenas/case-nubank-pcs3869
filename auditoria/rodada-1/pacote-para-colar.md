# Pacote para colar no LLM auditor (ChatGPT ou Gemini)

Copie tudo abaixo da linha e cole numa conversa nova do ChatGPT ou do Gemini. Não use o Claude, que foi o gerador.

---

**Objetivo:** Auditar a proposta de consultoria e apontar falhas financeiras, de cronograma, de coerência e de premissas, antes da entrega ao cliente.

**Domínio:** Auditoria de propostas de consultoria em sistemas de informação para crédito ao consumidor e meios de pagamento.

**Contexto:** Um grupo de alunos escreveu uma proposta de consultoria fictícia para integrar informações entre NuPay e cartão de crédito do Nubank, com foco em alinhar taxas e risco entre os produtos. A proposta foi gerada com apoio de outro LLM. O cenário é hipotético e usa só informação pública; os valores de taxa do exemplo são fictícios.

**Persona:** Você é um auditor sênior de consultoria, cético e objetivo. Seu trabalho é encontrar problemas, não elogiar. Você aponta só o que consegue sustentar com um trecho da proposta.

**Atividades:**
1. Refaça as contas da planilha de custos passo a passo (horas, custos por serviço, subtotal, contingência, tributos, total) e diga se batem.
2. Verifique o cronograma: dependências, sobreposições, caminho crítico e se os marcos são verificáveis.
3. Verifique a coerência entre desafios, serviços, cronograma e custos (todo desafio atendido? algum serviço sem desafio? algum serviço subdimensionado?).
4. Verifique a lógica do alinhamento de taxas: a fórmula, as regras R1 a R6 e o exemplo numérico. Procure contradições, regras impossíveis de checar e lacunas.
5. Aponte premissas frágeis ou afirmações que pareçam fato quando são hipótese.
6. Para cada problema, diga a severidade e recomende uma correção concreta.

**Definições:**
- Crítico: invalida um número, um prazo ou a lógica central; precisa ser corrigido antes da entrega.
- Médio: enfraquece a proposta, mas não a invalida.
- Baixo: forma, clareza ou detalhe.
- Não invente dados externos. Se algo depende de informação que a proposta não tem, diga que é uma lacuna.

**Formato de saída:**
1. "Verificação das contas": o passo a passo do item 1, terminando em "batem" ou "não batem".
2. Tabela de achados com as colunas: ID (A01, A02…), Seção, Tipo (Financeiro, Cronograma, Coerência, Alinhamento de taxas, Premissa), Severidade (Crítico, Médio, Baixo), Evidência (trecho curto da proposta), Recomendação.
3. Um parágrafo final com os três achados mais importantes.

**Descrição de entrada:** Quatro documentos em Markdown, colados em sequência e separados por títulos: proposta v1, anexo de alinhamento de taxas, cronograma e as abas Resumo e Esforço da planilha de custos.

---

## DOCUMENTO 1 — Proposta v1

# Proposta de consultoria — Integração de informações entre NuPay e cartão de crédito

**Versão:** v1 (entrega 3, 24/11/2026) · **Limite:** 7 páginas · **Grupo:** Lucas Carvalho · Ian Magalhães · Rafael Tamasi

> Versão para a auditoria cruzada (rodada 1). Cenário hipotético, construído com informação pública; valores de taxas são fictícios e ilustrativos.

## 1. Contexto e objetivo

O NuPay é o meio de pagamento do Nubank para compras online em estabelecimentos parceiros, com três modalidades: débito, crédito (limite do cartão) e limite adicional, que é temporário, exclusivo do NuPay e sujeito a análise. As compras no crédito e no limite adicional entram na fatura do cartão de crédito.

A hipótese do cenário analisado é que dados e regras de NuPay e cartão não têm uma visão integrada. Sem esse alinhamento, fica difícil ajustar taxas e risco de forma coordenada, e soluções como parcela mínima e post purchase financing exigem mais esforço para comparar e coordenar ofertas.

**Objetivo:** desenhar e pilotar, em 16 semanas, um sistema de informação com dados e regras integrados, para que as taxas de NuPay e cartão sejam coerentes com o contexto de cada produto. Alinhar não significa ter taxas idênticas.

## 2. Desafios identificados

| ID | Desafio | Dimensão (Laudon) | Impacto |
| --- | --- | --- | --- |
| D1 | Dados do cliente divididos entre NuPay e cartão | Tecnologia | Nenhum produto vê sozinho a exposição total |
| D2 | Regras de taxas, prazos e elegibilidade definidas por produto | Administração | Condições podem divergir sem motivo claro |
| D3 | Taxa e risco ajustados sem ver o outro produto | Administração | O risco da fatura muda sem avaliação conjunta |
| D4 | Comparação de condições trabalhosa | Organização | Mais esforço para coordenar ofertas |
| D5 | Mudanças de regra sem versão nem rastreio | Tecnologia | Difícil saber qual regra valia e por quê |

## 3. Como funciona o alinhamento de taxas

Este é o centro da proposta. O detalhe completo está no anexo `alinhamento-de-taxas.md`.

**Alinhar é explicar toda diferença.** Para o mesmo cliente e prazo, as taxas de NuPay e cartão partem da mesma base e do mesmo risco. A única parte que pode diferir é um ajuste de produto, declarado, aprovado e versionado.

**Visão consolidada (S2).** Uma base única calcula, para os dois produtos, a **exposição total** do cliente, o **comprometimento mensal** da fatura (parcelas do cartão e do NuPay) e uma **faixa de risco única**.

**Fórmula comum (S3).** Toda taxa de parcelamento segue:

> **Taxa = Referência + Componente de risco + Ajuste de prazo + Ajuste de produto**

Referência (finanças), risco (risco de crédito) e prazo (política comum) são iguais nos dois produtos. Só o ajuste de produto difere, com justificativa do time do produto.

**Seis regras de coerência (S3, S4, S5).**

| Regra | Enunciado |
| --- | --- |
| R1 Mesmo risco | O componente de risco do cliente é o mesmo nos dois produtos |
| R2 Corredor | A diferença de taxa entre NuPay e cartão (e entre parcelar na compra e depois) fica dentro de um limite definido pela governança |
| R3 Risco melhor nunca paga mais | Faixa melhor nunca tem taxa maior, no mesmo produto e prazo |
| R4 Prazo maior custa mais no total | Mais parcelas nunca reduzem o custo total |
| R5 Teto de comprometimento | Parcelas mensais somadas (cartão + NuPay) abaixo do teto da faixa; se não couber, reduz prazo ou valor |
| R6 Toda oferta tem versão | Cada oferta registra a versão da regra usada |

**Na hora da compra.** O NuPay pede a oferta; o sistema lê a visão consolidada, aplica a versão vigente da fórmula, checa o corredor (R2) e o teto (R5), e o app mostra as modalidades com a versão registrada. Depois da confirmação, a visão consolidada é atualizada na hora.

**Depois da compra.** Parcela mínima e financiamento após a compra seguem o mesmo caminho, com a mesma versão. Por isso "parcelar depois" fica coerente com "parcelar na compra".

**Quando uma taxa muda.** Painel mostra a divergência → o dono do componente propõe → a simulação checa R1 a R5 nos dois produtos → a governança aprova → a nova versão é publicada **ao mesmo tempo** no NuPay e no cartão → o painel acompanha, com volta à versão anterior se preciso.

**Exemplo ilustrativo (valores fictícios).** Cliente da faixa B, compra de R$ 1.200 em 6x, com R$ 450 por mês já comprometidos. Referência 2,0% a.m., risco B +1,5 p.p., ajuste NuPay +0,3 p.p., ajuste do cartão após a compra +0,5 p.p., corredor 0,5 p.p., teto R$ 800 por mês.

| | Com integração | Sem integração (hipotético) |
| --- | --- | --- |
| Parcelar na compra (NuPay) | 3,8% a.m. · R$ 227,43/mês | 4,5% a.m. (NuPay vê o cliente como C) |
| Parcelar depois (cartão) | 4,0% a.m. · R$ 228,91/mês | 3,2% a.m. |
| Diferença | 0,2 p.p., dentro do corredor | 1,3 p.p., sem motivo de produto |
| Teto (R5) | R$ 677,43 ≤ R$ 800: oferta liberada | Não checado |

## 4. Serviços propostos

| Serviço | Objetivo | Desafios | Entregáveis principais |
| --- | --- | --- | --- |
| S1 Diagnóstico de dados e regras | Mapear dados e regras atuais dos dois produtos | D1, D2, D5 | Inventário de dados; mapa de regras; BPMN as-is |
| S2 Visão integrada do cliente | Base única com exposição, comprometimento e faixa de risco | D1, D3 | Modelo de dados; dicionário; especificação de integração |
| S3 Regras versionadas | Fórmula comum, regras R1 a R6 e fluxo de aprovação | D2, D5 | Catálogo de regras; fluxo de aprovação; matriz de responsabilidades |
| S4 Painel de taxas e risco | Leitura comum de taxas, risco e divergências | D3, D4 | Dicionário de indicadores; protótipo do painel |
| S5 Simulação de coerência | Testar mudanças nos dois produtos antes de publicar | D3, D4 | Cenários; relatório de testes das regras |
| S6 Piloto e gestão da mudança | Rodar o ciclo de revisão de taxas com um grupo piloto | D1 a D5 | Plano de piloto; treinamento; lições aprendidas |

## 5. Solução proposta

A solução tem dois fluxos, modelados em BPMN (`solucao-processo.bpmn`): a **compra coordenada**, que consulta a visão integrada e aplica as regras vigentes; e a **governança de taxas e regras**, que simula, aprova e publica regras versionadas para os dois produtos. Os dois compartilham a base integrada e o repositório de regras.

[Figura: BPMN da solução, omitida no pacote]

## 6. Cronograma de atividades

| Serviço | Semanas | Depende de |
| --- | --- | --- |
| S1 Diagnóstico | 1 a 3 | — |
| S2 Visão integrada | 3 a 8 | S1 |
| S3 Regras versionadas | 4 a 8 | S1 |
| S4 Painel | 7 a 11 | S2 |
| S5 Simulação | 8 a 12 | S2, S3 |
| S6 Piloto | 12 a 16 | S4, S5 |

**Marcos:** M1 diagnóstico aprovado (semana 3) · M2 base e regras definidas (semana 8) · M3 alinhamento validado, com R1 a R6 aprovadas na simulação (semana 12) · M4 piloto concluído (semana 16). **Caminho crítico:** S1 → S2 → S5 → S6. Detalhe em `cronograma.md`.

## 7. Investimento

| Serviço | Horas | Valor (R$) |
| --- | --- | --- |
| S1 Diagnóstico de dados e regras | 264 | 48.000,00 |
| S2 Visão integrada do cliente | 408 | 88.800,00 |
| S3 Repositório de regras versionadas | 340 | 68.000,00 |
| S4 Painel de taxas, risco e divergências | 340 | 63.000,00 |
| S5 Simulação de coerência | 340 | 76.000,00 |
| S6 Piloto e gestão da mudança | 350 | 69.500,00 |
| **Subtotal** | **2.042** | **413.300,00** |
| Contingência (10%) | | 41.330,00 |
| Tributos (15% sobre o valor com contingência) | | 68.194,50 |
| **Total** | | **522.824,50** |

Esforço por perfil, valores/hora e fórmulas em `planilha-custos.xlsx`; raciocínio em `prompts/03-custos-cot.md`.

## 8. Premissas e condições

- O problema é uma hipótese do cenário analisado, não uma falha comprovada do Nubank; a proposta usa só informação pública.
- Consultoria fictícia; valores/hora, contingência e tributos são premissas do grupo, editáveis na planilha.
- Valores reais de taxas, faixas, corredor e teto são decididos pelo cliente na governança, com apoio da simulação (S5).
- Pagamento sugerido por marco: 20% em M1, 30% em M2, 30% em M3 e 20% em M4.


## DOCUMENTO 2 — Anexo: alinhamento de taxas

# Anexo técnico — Como funciona o alinhamento de taxas entre NuPay e cartão

**Versão:** v1 (24/11/2026) · **Parte de:** Item A, proposta de consultoria · **Serviços relacionados:** S2, S3, S4, S5, S6

> Este anexo descreve a solução proposta pela consultoria. O problema é uma hipótese do cenário analisado, construída com informação pública; não descreve os sistemas internos do Nubank. Todos os valores numéricos são **fictícios e ilustrativos**.

## 1. O que significa alinhar taxas

Alinhar **não** é cobrar a mesma taxa nos dois produtos. NuPay e cartão têm contextos diferentes (canal, momento da decisão, prazo, se o limite é regular ou adicional) e podem ter taxas diferentes.

Alinhar é garantir que **toda diferença de taxa entre os produtos tenha um motivo declarado, aprovado e rastreável**. Para o mesmo cliente, no mesmo prazo, as taxas partem da mesma base e do mesmo risco; o que muda é só o ajuste de produto, que é explícito e fica dentro de um limite combinado.

## 2. Onde o desalinhamento nasce

O limite adicional e as parcelas do NuPay entram na **mesma fatura** do cartão. Na prática, o cliente tem dois caminhos para parcelar uma compra:

- **Parcelar na compra**, pelo NuPay (crédito ou limite adicional);
- **Parcelar depois**, pela fatura do cartão (por exemplo, post purchase financing ou parcela mínima).

Se cada produto calcula o risco e a taxa com a sua própria visão do cliente, três coisas podem acontecer:

1. O mesmo cliente recebe uma classificação de risco diferente em cada produto.
2. A mesma dívida custa bem mais num caminho do que no outro, sem motivo de produto.
3. Nenhum produto enxerga o comprometimento total da fatura ao oferecer mais crédito.

## 3. Os três blocos da solução

| Bloco | O que faz | Serviço |
| --- | --- | --- |
| **Visão consolidada do cliente** | Junta em um lugar tudo o que pesa na fatura | S2 |
| **Política de taxa comum** | Uma única fórmula, com componentes e donos definidos | S3 |
| **Regras de coerência e governança** | Seis regras checadas na simulação, na oferta e no painel | S3, S4, S5 |

## 4. Bloco 1 — Visão consolidada do cliente

A base integrada (S2) reúne, por cliente:

- limite regular do cartão e quanto dele está em uso;
- limite adicional do NuPay concedido e em uso;
- parcelas futuras já lançadas na fatura, do cartão e do NuPay;
- histórico de pagamento da fatura e uso de parcela mínima ou de financiamento após a compra.

A partir disso, o sistema calcula três números, **uma vez só, para os dois produtos**:

| Indicador | Definição |
| --- | --- |
| **Exposição total** | Tudo o que o cliente deve ou vai dever na fatura: saldo atual + parcelas futuras (cartão e NuPay) |
| **Comprometimento mensal** | Soma das parcelas que caem em cada fatura futura |
| **Faixa de risco única** | Classificação do cliente (por exemplo, A, B, C, D) feita sobre a visão consolidada, usada pelos dois produtos |

## 5. Bloco 2 — Política de taxa comum

Toda taxa de parcelamento, nos dois produtos, segue a mesma estrutura:

> **Taxa = Referência + Componente de risco + Ajuste de prazo + Ajuste de produto**

| Componente | O que representa | Depende de | Dono (quem propõe) |
| --- | --- | --- | --- |
| **Referência** | Custo do dinheiro para a instituição | Mercado | Finanças |
| **Componente de risco** | Perda esperada da faixa de risco | Faixa única do cliente | Risco de crédito |
| **Ajuste de prazo** | Diferença por número de parcelas | Prazo | Política comum |
| **Ajuste de produto** | O que é próprio de cada produto (por exemplo, limite temporário do NuPay, renegociação após a compra no cartão) | Produto | Time do produto, com justificativa |

O ponto central: **referência, risco e prazo são iguais para os dois produtos.** Só o ajuste de produto pode diferir, e ele é declarado, justificado e versionado. Assim, qualquer diferença de taxa entre NuPay e cartão se explica olhando uma única linha.

O parcelamento sem juros oferecido por uma loja parceira é uma condição comercial do estabelecimento e fica fora desta fórmula.

## 6. Bloco 3 — Regras de coerência

Seis regras definem o que é uma oferta alinhada. Elas são checadas em três momentos: na **simulação** (antes de uma regra nova entrar), na **oferta** (a cada compra) e no **painel** (acompanhamento).

| Regra | Enunciado | Como é checada |
| --- | --- | --- |
| **R1 Mesmo risco** | O componente de risco de um cliente é o mesmo nos dois produtos | A faixa vem da visão consolidada, não de cada produto |
| **R2 Corredor entre produtos** | Para o mesmo cliente, prazo e valor, a diferença de taxa entre NuPay e cartão fica dentro de um corredor máximo, definido pela governança. Vale também entre parcelar na compra e parcelar depois | Diferença calculada na simulação e na oferta |
| **R3 Risco melhor nunca paga mais** | No mesmo produto e prazo, uma faixa melhor nunca tem taxa maior que uma faixa pior | Teste em todas as faixas antes de publicar |
| **R4 Prazo maior custa mais no total** | Mais parcelas nunca deixam o custo total menor | Teste em todos os prazos antes de publicar |
| **R5 Teto de comprometimento** | A soma das parcelas mensais (cartão + NuPay) fica abaixo do teto da faixa; se uma oferta ultrapassar, o prazo ou o valor são reduzidos, ou a oferta não aparece | Checada a cada oferta, com o comprometimento consolidado |
| **R6 Toda oferta tem versão** | Cada oferta registra a versão da regra que a gerou | Campo obrigatório no registro da transação |

## 7. Como funciona na hora da compra

1. O cliente escolhe NuPay no checkout de um estabelecimento parceiro.
2. O NuPay pede uma oferta ao sistema integrado.
3. O sistema lê a **visão consolidada**: faixa de risco, exposição e comprometimento mensal.
4. O sistema aplica a **versão vigente** da política: calcula a taxa de cada prazo com a fórmula comum.
5. O sistema checa **R2 e R5**: a taxa está no corredor e as novas parcelas cabem no teto? Se não couberem, reduz o prazo ou o valor do limite adicional.
6. O app mostra as modalidades possíveis (débito, crédito e, se elegível, limite adicional), cada uma com o número da versão da regra.
7. O cliente confirma; a compra e as parcelas entram na fatura.
8. O sistema atualiza a visão consolidada na hora, para a próxima oferta, de qualquer produto, já enxergar a nova parcela.

## 8. Como funciona depois da compra

Quando o cliente, já com a fatura fechada, consulta parcela mínima ou financiamento após a compra, o cartão segue **o mesmo caminho**: lê a mesma visão consolidada, usa a mesma versão da política e checa as mesmas regras. É isso que faz o "parcelar depois" ser coerente com o "parcelar na compra".

## 9. Como funciona quando uma taxa muda

1. **Painel:** o painel integrado (S4) mostra taxas, risco e divergências; por exemplo, ofertas fora do corredor ou faixas com comprometimento alto.
2. **Proposta:** o dono do componente propõe a mudança (por exemplo, risco propõe subir o componente da faixa C).
3. **Simulação:** o sistema (S5) aplica a mudança na carteira dos dois produtos e checa R1 a R5 em todas as faixas e prazos. O relatório mostra quantas ofertas mudam e quanto.
4. **Decisão:** se alguma regra falhar, a proposta volta para ajuste. Se passar, a governança aprova.
5. **Publicação:** a nova versão (por exemplo, v13) entra em vigor **ao mesmo tempo** no NuPay e no cartão. A versão anterior fica guardada.
6. **Acompanhamento:** o painel compara antes e depois. Se algo sair do esperado, a versão anterior pode ser restaurada.

## 10. Indicadores do painel

| Indicador | Pergunta que responde |
| --- | --- |
| Ofertas fora do corredor (R2) | Os produtos estão coerentes entre si? |
| Comprometimento médio por faixa (R5) | A fatura está ficando pesada para alguma faixa? |
| Ofertas com versão registrada (R6) | Toda oferta é rastreável? |
| Tempo entre aprovação e publicação nos dois produtos | A mudança chegou junto aos dois produtos? |
| Diferença de custo entre parcelar na compra e depois | A mesma dívida custa coerentemente nos dois caminhos? |

## 11. Exemplo ilustrativo (valores fictícios)

**Premissas fictícias:** referência 2,0% a.m.; componente de risco da faixa B +1,5 p.p.; ajuste de prazo para 6 parcelas 0; ajuste de produto: NuPay limite adicional +0,3 p.p.; financiamento após a compra +0,5 p.p.; corredor R2 = 0,5 p.p.; teto de comprometimento da faixa B = R$ 800 por mês. O cálculo ignora IOF e outros encargos.

**Situação:** cliente da faixa B, compra de R$ 1.200 em 6 parcelas, com R$ 450 por mês já comprometidos em parcelas do cartão.

| | Com integração | Sem integração (cenário hipotético) |
| --- | --- | --- |
| Faixa de risco | B nos dois produtos | NuPay classifica como C (não vê o histórico do cartão); cartão classifica como B |
| Taxa no NuPay (parcelar na compra) | 2,0 + 1,5 + 0,3 = **3,8% a.m.** | 4,5% a.m. |
| Taxa no cartão (parcelar depois) | 2,0 + 1,5 + 0,5 = **4,0% a.m.** | 3,2% a.m. |
| Diferença entre os caminhos | 0,2 p.p. → **dentro do corredor** | 1,3 p.p. → fora de qualquer corredor |
| Parcela mensal | R$ 227,43 (NuPay) · R$ 228,91 (cartão) | R$ 232,65 (NuPay) · R$ 222,99 (cartão) |
| Custo total das 6 parcelas | R$ 1.364,56 · R$ 1.373,49 (diferença de R$ 8,93) | R$ 1.395,92 · R$ 1.337,93 (diferença de R$ 57,99) |
| Teto de comprometimento (R5) | R$ 450 + R$ 227,43 = R$ 677,43 ≤ R$ 800 → oferta liberada | Não checado: o NuPay não vê os R$ 450 do cartão |

**Leitura:** com integração, a diferença entre os dois caminhos é pequena e explicada só pelo ajuste de produto. Sem integração, o mesmo cliente paga mais para parcelar na compra do que depois, sem motivo de produto, e a oferta é feita sem saber o comprometimento real da fatura.

## 12. Fora do escopo

- Valores reais de taxas, faixas ou tetos: são decididos pelo cliente na governança, com apoio da simulação.
- Exibição de custo efetivo total e encargos ao cliente final: segue as exigências regulatórias vigentes e não é tratada aqui.
- Detalhes dos sistemas internos atuais do Nubank: o diagnóstico (S1) é que vai levantá-los.


## DOCUMENTO 3 — Cronograma

# Cronograma da consultoria

**Atividade do cronograma do grupo:** 3.1 · **Papel:** Analista financeiro (Rafael) · **Versão:** v1 (24/11/2026)

A consultoria dura **16 semanas**, em quatro fases. As semanas são relativas ao início do contrato (semana 1 = primeira semana após a assinatura).

## Serviços por semana

| Serviço | Semanas | Duração | Depende de | Entregáveis |
| --- | --- | --- | --- | --- |
| S1 Diagnóstico de dados e regras | 1 a 3 | 3 sem. | — | Inventário de dados; mapa de regras; BPMN as-is |
| S2 Visão integrada do cliente | 3 a 8 | 6 sem. | S1 | Modelo de dados; dicionário; especificação de integração |
| S3 Repositório de regras versionadas | 4 a 8 | 5 sem. | S1 | Catálogo de regras; fluxo de aprovação; matriz de responsabilidades |
| S4 Painel de taxas, risco e divergências | 7 a 11 | 5 sem. | S2 | Dicionário de indicadores; protótipo do painel |
| S5 Simulação de coerência | 8 a 12 | 5 sem. | S2, S3 | Regras de coerência; cenários; relatório de testes |
| S6 Piloto e gestão da mudança | 12 a 16 | 5 sem. | S4, S5 | Plano de piloto; treinamento; lições aprendidas |

S2 começa na semana 3, junto com o fim do S1, porque o modelo de dados parte do inventário já levantado. S3 começa uma semana depois, quando o mapa de regras está fechado.

## Marcos

| Marco | Semana | Critério de aceite |
| --- | --- | --- |
| M1 Diagnóstico aprovado | 3 | Os times de NuPay e cartão reconhecem o mapa as-is |
| M2 Base e regras definidas | 8 | Modelo de dados e catálogo de regras versionadas aprovados |
| M3 Alinhamento validado | 12 | Painel em uso e simulação aprovando as regras de coerência R1 a R6 |
| M4 Piloto concluído | 16 | Ciclo de revisão de taxas rodado no piloto com painel e repositório |

## Gráfico de Gantt (semanas 1 a 16)

| Serviço | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 |
| --- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| S1 Diagnóstico | ■ | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |
| S2 Visão integrada |  |  | ■ | ■ | ■ | ■ | ■ | ■ |  |  |  |  |  |  |  |  |
| S3 Regras versionadas |  |  |  | ■ | ■ | ■ | ■ | ■ |  |  |  |  |  |  |  |  |
| S4 Painel |  |  |  |  |  |  | ■ | ■ | ■ | ■ | ■ |  |  |  |  |  |
| S5 Simulação |  |  |  |  |  |  |  | ■ | ■ | ■ | ■ | ■ |  |  |  |  |
| S6 Piloto |  |  |  |  |  |  |  |  |  |  |  | ■ | ■ | ■ | ■ | ■ |
| Marcos |  |  | M1 |  |  |  |  | M2 |  |  |  | M3 |  |  |  | M4 |

## Caminho crítico

S1 → S2 → S5 → S6. Um atraso no S2 (visão integrada) atrasa a simulação de coerência, que é o coração do alinhamento de taxas, e com ela o piloto.


## DOCUMENTO 4 — Planilha de custos (valores calculados)

### Premissas

| Perfil | Valor/hora (R$) |
| --- | --- |
| Gerente de projeto | 250 |
| Arquiteto de dados | 230 |
| Especialista de risco | 240 |
| Analista de negócios | 180 |
| Analista de dados | 180 |
| Analista de processos | 170 |
| Designer de produto | 170 |

| Parâmetro | Valor |
| --- | --- |
| Horas por semana | 40 |
| Contingência (sobre o subtotal) | 0,10 |
| Tributos (sobre o valor com contingência) | 0,15 |

### Esforço

| Serviço | Perfil | Semanas | Dedicação | Horas | Valor/hora | Custo |
| --- | --- | --- | --- | --- | --- | --- |
| S1 Diagnóstico de dados e regras | Analista de negócios | 3 | 1 | 120 | 180 | 21600 |
| S1 Diagnóstico de dados e regras | Analista de processos | 3 | 1 | 120 | 170 | 20400 |
| S1 Diagnóstico de dados e regras | Gerente de projeto | 3 | 0,20 | 24 | 250 | 6000 |
| S2 Visão integrada do cliente | Arquiteto de dados | 6 | 1 | 240 | 230 | 55200 |
| S2 Visão integrada do cliente | Analista de negócios | 6 | 0,50 | 120 | 180 | 21600 |
| S2 Visão integrada do cliente | Gerente de projeto | 6 | 0,20 | 48 | 250 | 12000 |
| S3 Repositório de regras versionadas | Analista de processos | 5 | 1 | 200 | 170 | 34000 |
| S3 Repositório de regras versionadas | Especialista de risco | 5 | 0,50 | 100 | 240 | 24000 |
| S3 Repositório de regras versionadas | Gerente de projeto | 5 | 0,20 | 40 | 250 | 10000 |
| S4 Painel de taxas, risco e divergências | Analista de dados | 5 | 1 | 200 | 180 | 36000 |
| S4 Painel de taxas, risco e divergências | Designer de produto | 5 | 0,50 | 100 | 170 | 17000 |
| S4 Painel de taxas, risco e divergências | Gerente de projeto | 5 | 0,20 | 40 | 250 | 10000 |
| S5 Simulação de coerência | Especialista de risco | 5 | 1 | 200 | 240 | 48000 |
| S5 Simulação de coerência | Analista de dados | 5 | 0,50 | 100 | 180 | 18000 |
| S5 Simulação de coerência | Gerente de projeto | 5 | 0,20 | 40 | 250 | 10000 |
| S6 Piloto e gestão da mudança | Analista de negócios | 5 | 1 | 200 | 180 | 36000 |
| S6 Piloto e gestão da mudança | Gerente de projeto | 5 | 0,50 | 100 | 250 | 25000 |
| S6 Piloto e gestão da mudança | Designer de produto | 5 | 0,25 | 50 | 170 | 8500 |
| Total |  |  |  | 2042 |  | 413300 |

### Resumo

| Serviço | Semanas | Horas | Custo | % do subtotal |
| --- | --- | --- | --- | --- |
| S1 Diagnóstico de dados e regras | 3 | 264 | 48000 | 0,12 |
| S2 Visão integrada do cliente | 6 | 408 | 88800 | 0,21 |
| S3 Repositório de regras versionadas | 5 | 340 | 68000 | 0,16 |
| S4 Painel de taxas, risco e divergências | 5 | 340 | 63000 | 0,15 |
| S5 Simulação de coerência | 5 | 340 | 76000 | 0,18 |
| S6 Piloto e gestão da mudança | 5 | 350 | 69500 | 0,17 |
| Subtotal |  | 2042 | 413300 |  |
| Contingência |  |  | 41330 |  |
| Valor com contingência |  |  | 454630 |  |
| Tributos |  |  | 68.194,50 |  |
| Total da proposta |  |  | 522.824,50 |  |
