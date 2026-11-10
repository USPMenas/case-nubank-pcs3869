# Prompt 02 — Serviços da consultoria — few shot

| Campo | Valor |
| --- | --- |
| Atividade do cronograma | 2.4 — Desenhar os serviços da consultoria |
| Técnica | Few shot (2 exemplos de serviço bem escrito, de outro setor) |
| Modelo usado (gerador) | Claude Opus 5.5, no claude.ai |
| Data da execução | 09/11/2026 |
| Operado por | Claude, a pedido do grupo (papéis: Analista de negócios e Engenheiro de prompts — Ian) |
| Entrada | Saída do Prompt 01 (desafios D1 a D5) |
| Saída usada em | `item-a-proposta/proposta.md`, seção 3 |

## Prompt

**Objetivo:** Propor os serviços de consultoria que resolvem os desafios D1 a D5, no mesmo formato dos exemplos.

**Domínio:** Consultoria em sistemas de informação para crédito ao consumidor e meios de pagamento.

**Contexto:** A consultoria propõe um sistema de informação com dados e regras integrados entre NuPay e cartão de crédito. A solução tem dois fluxos (modelados em BPMN): a compra coordenada, que consulta uma visão integrada do cliente e aplica regras vigentes, e a governança de taxas e regras, que analisa indicadores, simula a coerência entre produtos e publica regras versionadas para os dois produtos.

**Persona:** Você é um sócio de consultoria que escreve propostas comerciais objetivas, que um cliente consegue aprovar e acompanhar.

**Atividades:**
1. Leia os desafios de entrada.
2. Agrupe desafios que um mesmo serviço resolve.
3. Para cada serviço, siga exatamente a estrutura dos exemplos.
4. Garanta que todo desafio seja atendido por ao menos um serviço.
5. Termine com uma matriz serviço × desafio.

**Definições:**
- Serviço: um pacote de trabalho com objetivo, atividades e entregáveis verificáveis.
- Critério de sucesso: algo que o cliente consegue observar ao fim do serviço, sem números inventados.
- Não estime horas nem preços; isso será feito no Prompt 03.
- Alinhamento não pressupõe taxas idênticas.

**Formato de saída:** Entre 4 e 6 serviços, cada um com os campos Nome, Objetivo, Desafios atendidos, Atividades (até 4), Entregáveis (até 3), Perfis envolvidos e Critério de sucesso. Depois, uma tabela serviço × desafio com "●" onde houver atendimento.

**Descrição de entrada:** Tabela de desafios D1 a D5 (saída do Prompt 01), colada abaixo.

### Exemplos (few shot)

**Exemplo 1 — rede de farmácias**

- **Nome:** Visão única de estoque entre lojas
- **Objetivo:** Dar a todas as lojas a mesma informação de estoque em tempo próximo do real.
- **Desafios atendidos:** Estoque consultado em sistemas separados; rupturas não percebidas.
- **Atividades:** Mapear as fontes de estoque; definir o modelo de dados comum; especificar a integração; validar com duas lojas piloto.
- **Entregáveis:** Modelo de dados de estoque; especificação da integração; relatório do piloto.
- **Perfis envolvidos:** Analista de negócios; arquiteto de dados.
- **Critério de sucesso:** As lojas piloto consultam o estoque das demais sem ligar para elas.

**Exemplo 2 — operadora de saúde**

- **Nome:** Catálogo de regras de autorização
- **Objetivo:** Reunir as regras de autorização de exames num único catálogo versionado.
- **Desafios atendidos:** Regras espalhadas em planilhas; decisões diferentes para o mesmo caso.
- **Atividades:** Levantar as regras vigentes; padronizar a escrita; criar o fluxo de aprovação de mudanças; publicar o catálogo.
- **Entregáveis:** Catálogo de regras; fluxo de aprovação em BPMN; guia de manutenção.
- **Perfis envolvidos:** Analista de processos; especialista do negócio.
- **Critério de sucesso:** Toda decisão de autorização aponta a versão da regra usada.

---

**Entrada:**

| ID | Desafio |
| --- | --- |
| D1 | Dados do cliente divididos entre NuPay e cartão (limite regular, limite adicional, parcelas e fatura) |
| D2 | Regras de taxas, prazos e elegibilidade definidas por produto, sem uma base comum |
| D3 | Ajuste de taxas e risco feito sem considerar o efeito no outro produto |
| D4 | Comparação de condições trabalhosa, com bases e critérios diferentes |
| D5 | Mudanças de regra sem versionamento e rastreio comuns |

## Saída obtida

**S1 — Diagnóstico de dados e regras (as-is)**
- **Objetivo:** Mapear onde estão hoje os dados e as regras de NuPay e cartão que afetam taxas e risco.
- **Desafios atendidos:** D1, D2, D5.
- **Atividades:** Entrevistar os times de NuPay e cartão; inventariar as fontes de dados; levantar as regras de taxas, prazos e elegibilidade; modelar o processo atual em BPMN.
- **Entregáveis:** Inventário de dados; mapa de regras por produto; BPMN as-is.
- **Perfis envolvidos:** Analista de negócios; analista de processos.
- **Critério de sucesso:** Os dois times reconhecem o mapa como fiel ao que fazem hoje.

**S2 — Visão integrada do cliente**
- **Objetivo:** Definir uma base única com histórico de compras e crédito, limites e fatura de cada cliente.
- **Desafios atendidos:** D1, D3.
- **Atividades:** Desenhar o modelo de dados integrado; escrever o dicionário de dados; especificar como cada produto alimenta e consulta a base; validar com casos reais anonimizados.
- **Entregáveis:** Modelo conceitual de dados; dicionário de dados; especificação de integração.
- **Perfis envolvidos:** Arquiteto de dados; analista de negócios.
- **Critério de sucesso:** Para um cliente de teste, a base mostra a exposição somada de cartão e limite adicional.

**S3 — Repositório de regras versionadas e governança**
- **Objetivo:** Reunir as regras dos dois produtos num repositório versionado, com fluxo de aprovação.
- **Desafios atendidos:** D2, D5.
- **Atividades:** Padronizar a escrita das regras; definir o versionamento; desenhar o fluxo de aprovação em BPMN; definir papéis de quem propõe, aprova e publica.
- **Entregáveis:** Catálogo de regras versionadas; fluxo de aprovação em BPMN; matriz de responsabilidades.
- **Perfis envolvidos:** Analista de processos; especialista de risco.
- **Critério de sucesso:** Toda oferta aponta a versão da regra que a gerou.

**S4 — Painel integrado de taxas, risco e divergências**
- **Objetivo:** Dar aos times uma leitura comum das condições e do risco dos dois produtos.
- **Desafios atendidos:** D3, D4.
- **Atividades:** Definir os indicadores com os times; especificar as fontes a partir da visão integrada; prototipar o painel; validar a leitura com os usuários.
- **Entregáveis:** Dicionário de indicadores; protótipo do painel; guia de uso.
- **Perfis envolvidos:** Analista de dados; designer de produto.
- **Critério de sucesso:** Os times comparam as condições de NuPay e cartão numa única tela.

**S5 — Simulação de coerência entre produtos**
- **Objetivo:** Avaliar o efeito de uma mudança de regra nos dois produtos antes de publicá-la.
- **Desafios atendidos:** D3, D4.
- **Atividades:** Definir os critérios de coerência; montar cenários de parcela mínima e post purchase financing; especificar a simulação; testar com mudanças hipotéticas.
- **Entregáveis:** Critérios de coerência; biblioteca de cenários; relatório de testes.
- **Perfis envolvidos:** Especialista de risco; analista de dados.
- **Critério de sucesso:** Nenhuma regra é aprovada sem um relatório de simulação anexado.

**S6 — Piloto e gestão da mudança**
- **Objetivo:** Colocar a solução em uso com um grupo piloto e preparar os times para adotá-la.
- **Desafios atendidos:** D1 a D5 (consolida os demais).
- **Atividades:** Planejar o piloto; treinar os times; acompanhar o uso; registrar ajustes.
- **Entregáveis:** Plano de piloto; material de treinamento; relatório de lições aprendidas.
- **Perfis envolvidos:** Gerente de projeto; analista de negócios.
- **Critério de sucesso:** Os times do piloto passam a usar o painel e o repositório no ciclo de revisão.

**Matriz serviço × desafio**

| Serviço | D1 | D2 | D3 | D4 | D5 |
| --- | --- | --- | --- | --- | --- |
| S1 Diagnóstico | ● | ● | | | ● |
| S2 Visão integrada | ● | | ● | | |
| S3 Regras versionadas | | ● | | | ● |
| S4 Painel | | | ● | ● | |
| S5 Simulação | | | ● | ● | |
| S6 Piloto | ● | ● | ● | ● | ● |

## Avaliação do grupo (a preencher)

- [ ] Todo desafio tem ao menos um serviço? (sim, pela matriz)
- [ ] Os serviços seguem o formato dos exemplos?
- [ ] Algum serviço é amplo demais para ser precificado na S3?
- Decisão: aceito / aceito com ajustes / refazer — por quem, em que data.

Nota: a comparação com o zero shot entra na apresentação da entrega 2. Os exemplos fizeram o modelo manter a mesma estrutura em todos os serviços, o que facilita a precificação.
