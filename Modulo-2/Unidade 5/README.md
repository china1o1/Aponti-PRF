# Unidade 5 — Consolidação Final e KPIs (Excel)

## Tecnologia
Excel (Tabelas Dinâmicas + Painel de Indicadores)

## Objetivo
Fechar o projeto reunindo, num único arquivo, os principais indicadores e cruzamentos já validados nas unidades anteriores (SQL e Python), agora apresentados em formato de **painel de conclusões** — cada aba já vem com a interpretação escrita ao lado da tabela, fechando o ciclo: dado → análise → conclusão de negócio.

## Arquivos
- `Atividade_Td_f.xlsx` — planilha principal
- `Atividade_TD.png` — captura de tela/print de apoio (provavelmente do painel final ou de um gráfico)

## Estrutura da planilha
| Aba | Conteúdo |
|---|---|
| `dados_abertos_prf-datatran2025` | Base bruta usada como fonte. |
| `5 BRs Mais Letais` | Ranking das 5 rodovias com maior taxa de letalidade. |
| `TD - Tipos de Acidentes x Gravidade` | Tabela dinâmica cruzando tipo de acidente com gravidade, + interpretação escrita. |
| `TD - Fase do Dia x Condições Climáticas` | Cruzamento fase do dia × clima, + interpretação escrita. |
| `TD - Causa x Gravidade` | Causas ordenadas por letalidade vs. por volume, lado a lado. |
| `TD - UF x BR` | Análise espacial: onde se concentra o volume e onde está a maior letalidade. |
| `KPIs` | Painel-resumo com os 5 indicadores-chave do projeto inteiro. |

## Os KPIs finais do projeto
| Indicador | Valor |
|---|---|
| Total de acidentes | 72.529 |
| Total de mortos | 6.043 |
| Total de feridos | 83.550 |
| % de acidentes fatais | 7,18% |
| Taxa de letalidade | 6,74% |

*(Nota: "% de acidentes fatais" mede quantas ocorrências tiveram ao menos 1 morto; "taxa de letalidade" mede mortos em relação ao total de vítimas — são leituras complementares, uma pela ocorrência, outra pela pessoa.)*

## Leitura consolidada (o fechamento da análise)

**Tipo de acidente × gravidade**: confirma o que já vinha desde a Unidade 2/3 — *Atropelamento de Pedestre* tem a maior taxa de letalidade entre os tipos com volume relevante (24,4%), seguido de *Colisão Frontal* (19,7%). Ao mesmo tempo, os tipos de **maior volume** (Colisão traseira, Saída de leito carroçável) têm letalidade bem mais baixa (~4-6%) — ou seja, o que mais acontece não é o que mais mata, e um painel que priorizasse só por frequência erraria o alvo da prevenção.

**Fase do dia × clima**: o pior cenário combinado é Amanhecer + Céu Claro (11,99% de fatalidade) entre as combinações com volume relevante — reforçando, mais uma vez, que a luminosidade baixa pesa mais que o clima em si (nevoeiro tem taxa alta, mas baixíssimo volume, então não é representativo).

**Causa × gravidade**: quando se olha causa por letalidade, ocupa o topo *Suicídio (presumido)* (53%) e *Pedestre andava na pista* (35%) — mas quando se olha por volume, o topo é *Ausência de reação do condutor* e *Reação tardia ou ineficiente do condutor*, com letalidade bem mais baixa (~4-6%). É a mesma lição de novo, em outra dimensão: a causa mais comum não é a mais mortal, e um plano de fiscalização baseado só em "causa mais frequente" ignoraria os cenários de maior risco por ocorrência.

**5 BRs mais letais**: BR-403 (60%), BR-30 (40%), BR-416 (35,29%), BR-402 (25%) e BR-447 (22,22%) lideram em % — mas a própria interpretação registrada na planilha faz a ressalva correta: são rodovias com **poucos registros** (a BR-403 tem só 6 acidentes no total), então a taxa alta é estatisticamente instável. Em contraste, a combinação de maior **volume absoluto** é SC × BR-101, com 4.222 acidentes — mostrando que "mais letal em %" e "mais crítico na prática" são recortes diferentes, e o painel tem o cuidado de não confundir os dois.

## Conclusão do projeto como um todo
Juntando as 5 unidades, o padrão que se repete em todas as tecnologias (Excel, SQL e Python) é o mesmo: **volume e gravidade não caminham juntos**. Os fatores com maior poder de explicar fatalidade são, nesta ordem de evidência: **tipo de acidente** (atropelamento e colisão frontal), **tipo de pista** (simples é ~2x mais letal que dupla) e **UF/localização** (Norte/Nordeste com menos acidentes, porém mais graves) — enquanto o **clima**, apesar de intuitivamente parecer um fator óbvio, se mostrou consistentemente secundário em todas as etapas da análise.
