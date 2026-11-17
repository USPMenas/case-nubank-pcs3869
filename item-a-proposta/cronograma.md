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
