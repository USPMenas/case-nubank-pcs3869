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
