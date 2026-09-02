# Unidade 2 — Tabelas Dinâmicas e Primeiras Conclusões (Excel)

## Tecnologia
Excel (Tabelas Dinâmicas)

## Objetivo
Aprofundar a análise da Unidade 1 usando **tabelas dinâmicas**, cruzando variáveis (dia da semana × turno, causa × rodovia, tipo de pista × UF, tipo de acidente × gravidade) para começar a enxergar relações, não só contagens isoladas. É a primeira unidade em que o projeto sai de "quantos acidentes existem" para "onde e quando os acidentes são mais graves".

## Arquivo
`modulo_02_excel_prf_Eliton_Gabriel.xlsx`

## Estrutura da planilha
| Aba | Conteúdo |
|---|---|
| `dados` | Base de 72.529 linhas, já com a coluna `acidente_fatal` calculada. |
| `tabelas_dinamicas` | 5 tabelas dinâmicas cruzando diferentes dimensões. |
| `graficos` | Visualizações derivadas das tabelas dinâmicas. |
| `observações` | Registro estruturado de observação → evidência → interpretação → limitação (metodologia de análise aplicada de forma explícita). |

## As 5 tabelas dinâmicas construídas
1. **Pessoas envolvidas por dia da semana e turno** — volume de pessoas por combinação de dia/turno.
2. **Total de mortos por rodovia (BR)** — ranking de rodovias por número absoluto de mortos, com filtro por causa.
3. **Mortalidade por UF e tipo de pista** — mortos cruzados por estado e tipo de pista (simples/dupla/múltipla).
4. **Feridos graves e acidentes fatais por tipo de acidente** — qual tipo de colisão gera mais vítimas graves.
5. **Vítimas e envolvidos por período do dia** — soma de feridos graves, pessoas, mortos e feridos leves por fase do dia.

## Leitura dos dados (raciocínio sobre os cruzamentos)
- **Plena Noite concentra o maior volume de mortos** entre as fases do dia: 2.892 mortos, contra 2.391 em Pleno dia — mesmo o dia tendo *muito* mais acidentes no total. Isso reforça a hipótese: dirigir à noite é desproporcionalmente mais arriscado, provavelmente por visibilidade reduzida e maior velocidade média com menos fiscalização.
- **Colisão frontal é o tipo de acidente mais letal em termos absolutos**: 1.396 acidentes fatais sobre 3.148 ocorrências — quase 1 em cada 2. Isso é coerente com a física do evento (duas massas se chocando de frente é o pior cenário possível de energia de impacto).
- **Atropelamento de pedestre também aparece muito grave**: 902 fatais em 1.321 ocorrências, o que já sinaliza (e será confirmado com números na Unidade 3, via "lift") que atropelamento tem taxa de fatalidade desproporcional ao seu volume.
- Na aba de observações, a autoria já registra um insight importante: em Pernambuco, a maioria dos acidentes acontece **a céu aberto**, não em condição climática adversa — ou seja, o clima **não é o principal vilão**; o foco de investigação deveria migrar para condição da via, sinalização e comportamento do condutor. Essa é uma conclusão de negócio genuína, não só um resumo de tabela, e ela orienta o que a Unidade 3 vai testar formalmente com SQL.

## Limitação registrada pela própria autoria
Faltam dados mais detalhados sobre condição da via/sinalização e testes de embriaguez — sem isso, a análise de causa fica limitada ao que a PRF já classifica como "causa_acidente" (uma variável categórica de julgamento do agente, não uma medição objetiva).
