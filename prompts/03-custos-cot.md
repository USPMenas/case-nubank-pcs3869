# Prompt 03 — Esforço e preços — chain of thought

| Campo | Valor |
| --- | --- |
| Atividade do cronograma | 3.2 — Estimar esforço e preços na planilha de custos |
| Técnica | Chain of thought (raciocínio passo a passo, explícito na saída) |
| Modelo usado (gerador) | Claude Opus 5.5, no claude.ai |
| Data da execução | 17/11/2026 |
| Operado por | Claude, a pedido do grupo (papéis: Analista financeiro — Rafael; Engenheiro de prompts — Ian) |
| Entrada | Serviços S1 a S6 (Prompt 02) e `cronograma.md` |
| Saída usada em | `item-a-proposta/planilha-custos.xlsx` e seção 7 da proposta |

## Prompt

**Objetivo:** Estimar o esforço em horas e o preço de cada serviço da consultoria, mostrando o raciocínio de cada passo.

**Domínio:** Precificação de projetos de consultoria em sistemas de informação.

**Contexto:** A consultoria tem seis serviços (S1 a S6) distribuídos em 16 semanas, conforme o cronograma de entrada. É uma consultoria fictícia, criada para um trabalho acadêmico; os valores/hora são premissas do grupo, não preços de mercado.

**Persona:** Você é um gerente financeiro de uma consultoria, acostumado a montar orçamentos que um cliente consegue auditar linha a linha.

**Atividades:** Pense passo a passo e mostre cada passo:
1. Para cada serviço, leia a duração em semanas no cronograma.
2. Escolha os perfis de cada serviço (dos listados no Prompt 02) e a dedicação de cada um (100%, 50%, 25% ou 20%), justificando em uma frase.
3. Calcule as horas: semanas × 40 h × dedicação.
4. Calcule o custo: horas × valor/hora do perfil.
5. Some por serviço e no total.
6. Aplique a contingência e os tributos das premissas, nessa ordem.
7. Confira se a soma das horas por serviço bate com a soma por perfil.

**Definições:**
- Semana = 40 horas de trabalho.
- Gerente de projeto com 20% de dedicação em todos os serviços técnicos, para coordenação.
- Contingência = 10% sobre o subtotal, para riscos de escopo.
- Tributos = 15% sobre o valor com contingência (premissa simplificada do grupo).
- Valores/hora (premissas do grupo, em R$): Gerente de projeto 250; Arquiteto de dados 230; Especialista de risco 240; Analista de negócios 180; Analista de dados 180; Analista de processos 170; Designer de produto 170.

**Formato de saída:** Primeiro, o raciocínio numerado por serviço. Depois, uma tabela com Serviço, Perfil, Semanas, Dedicação, Horas, Valor/hora e Custo. Por fim, um resumo com subtotal, contingência, tributos e total.

**Descrição de entrada:** Tabela do cronograma (serviços, semanas e duração) colada abaixo.

---

**Entrada:** S1 semanas 1–3 (3 sem.); S2 3–8 (6); S3 4–8 (5); S4 7–11 (5); S5 8–12 (5); S6 12–16 (5).

## Saída obtida

**Raciocínio passo a passo**

1. **S1 Diagnóstico (3 semanas).** É levantamento e entrevistas, então o analista de negócios e o analista de processos ficam em tempo integral; o gerente coordena a 20%. Horas: 3 × 40 × 1 = 120 h para cada analista; 3 × 40 × 0,2 = 24 h para o gerente. Custo: 120 × 180 + 120 × 170 + 24 × 250 = 21.600 + 20.400 + 6.000 = **R$ 48.000**.
2. **S2 Visão integrada (6 semanas).** O modelo de dados é o trabalho central, então o arquiteto de dados fica a 100%; o analista de negócios valida as regras de negócio a 50%. Horas: 240 h (arquiteto), 120 h (analista), 48 h (gerente). Custo: 55.200 + 21.600 + 12.000 = **R$ 88.800**.
3. **S3 Regras versionadas (5 semanas).** O analista de processos padroniza regras e desenha o fluxo de aprovação a 100%; o especialista de risco revisa as regras de taxa a 50%. Horas: 200 h, 100 h, 40 h (gerente). Custo: 34.000 + 24.000 + 10.000 = **R$ 68.000**.
4. **S4 Painel (5 semanas).** O analista de dados define indicadores e fontes a 100%; o designer prototipa a tela a 50%. Horas: 200 h, 100 h, 40 h (gerente). Custo: 36.000 + 17.000 + 10.000 = **R$ 63.000**.
5. **S5 Simulação de coerência (5 semanas).** O especialista de risco define as regras de coerência e os cenários a 100%; o analista de dados roda as simulações a 50%. Horas: 200 h, 100 h, 40 h (gerente). Custo: 48.000 + 18.000 + 10.000 = **R$ 76.000**.
6. **S6 Piloto (5 semanas).** O piloto é sobretudo acompanhamento e treinamento: analista de negócios a 100%, gerente a 50% (coordena o cliente) e designer a 25% para ajustes de uso. Horas: 200 h, 100 h, 50 h. Custo: 36.000 + 25.000 + 8.500 = **R$ 69.500**.
7. **Subtotal:** 48.000 + 88.800 + 68.000 + 63.000 + 76.000 + 69.500 = **R$ 413.300**, com 2.042 horas (S1 264 + S2 408 + S3 340 + S4 340 + S5 340 + S6 350).
8. **Contingência (10%):** R$ 41.330 → R$ 454.630.
9. **Tributos (15% sobre R$ 454.630):** R$ 68.194,50 → **total de R$ 522.824,50**.
10. **Conferência:** a soma das horas por perfil (gerente 292; arquiteto 240; especialista de risco 300; analista de negócios 440; analista de dados 300; analista de processos 320; designer 150) também dá 2.042 h. Bate com o passo 7.

**Tabela de custos** — reproduzida com fórmulas em `planilha-custos.xlsx`, aba Esforço.

## Avaliação do grupo (a preencher)

- [ ] O raciocínio de cada serviço justifica os perfis e as dedicações?
- [ ] A conferência do passo 10 bate com o passo 7? (a planilha recalcula tudo por fórmula)
- [ ] As premissas de valor/hora e tributos foram aprovadas pelo grupo?
- Decisão: aceito / aceito com ajustes / refazer — por quem, em que data.

O chain of thought deixa cada número rastreável até a premissa que o gerou; o passo de conferência existe para pegar erros de soma antes da auditoria.
