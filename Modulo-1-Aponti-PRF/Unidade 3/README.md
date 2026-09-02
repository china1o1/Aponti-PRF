# Unidade 3 — Análise de Letalidade em SQL

## Tecnologia
SQL (SQLite)

## Objetivo
Sair do Excel e formalizar a análise em SQL, criando **views reutilizáveis** e uma métrica que não tinha aparecido nas unidades anteriores: o **lift** — quanto uma categoria é mais (ou menos) perigosa que a média geral do Brasil. É a unidade em que o projeto deixa de comparar só volumes e passa a comparar *risco relativo*.

## Arquivo
`projeto_prf_analise.sql` (188 linhas, ~18 consultas numeradas e comentadas)

## Estrutura da análise
1. **Validação da importação** — versão do SQLite, schema da tabela, contagem de linhas.
2. **View base (`vw_acidentes_base`)** — recria a coluna `acidente_fatal` (1 quando `mortos >= 1`) direto no banco, igual à lógica usada no Excel e no Python — a mesma regra de negócio é replicada nas 3 tecnologias, o que garante consistência entre as unidades.
3. **Agregações univariadas** — % de fatais por UF, por BR, por mês, por tipo de acidente, por causa, por fase do dia, por condição meteorológica, por tipo de pista.
4. **Agregações bivariadas** — cruzamento tipo de pista × fase do dia, com coluna de cobertura (% do total que aquela combinação representa), pra não deixar tirar conclusão de combinações raras.
5. **Cálculo de lift** — `taxa do grupo ÷ taxa média do Brasil`. Lift > 1 = mais perigoso que a média; lift < 1 = mais seguro.
6. **Views consolidadas** (`vw_indicadores_mensais`, `vw_indicadores_uf_br`) — pensadas para alimentar dashboards depois.

## Resultados obtidos (com raciocínio)

**Fatalidade geral**: dos 72.529 acidentes, ~7,2% foram fatais — esse número é o "chão" contra o qual todo o resto é comparado.

**Por estado (UF)** — o achado mais forte da unidade: os estados com maior % de fatalidade não são os de maior volume.
- MA lidera com 18,7% de fatalidade, PA com 17,28% — mas em volume absoluto de acidentes esses estados estão longe do topo.
- Isso é uma inversão importante: estados do Norte/Nordeste, com malha rodoviária mais precária e provavelmente menor tempo de resgate, têm **menos acidentes, mas cada acidente é mais grave**. Um dashboard que olhasse só "total de acidentes por estado" esconderia esse risco.

**Por tipo de pista**: pista **Simples** tem 9,86% de fatalidade contra 4,88% da **Dupla** — praticamente o dobro. Isso é um dos sinais mais claros e "acionáveis" do projeto: duplicar pistas simples de alto tráfego é literalmente uma medida com efeito mensurável sobre mortes.

**Combinação pista × fase do dia**: pista Simples + Amanhecer chega a 14,64% de fatalidade — o pior cenário identificado nas combinações com volume relevante. Faz sentido: baixa luminosidade + via sem separação física de sentido é a pior combinação possível.

**Lift por tipo de acidente**: Atropelamento de Pedestre (lift 4,11) e Colisão Frontal (lift 4,10) são ambos **mais de 4x mais letais que a média geral**. O valor do lift aqui é justamente mostrar que dois tipos de acidente muito diferentes em natureza — um envolve pedestre, o outro só veículos — chegam a um risco relativo quase idêntico, o que não seria óbvio olhando só a % de fatalidade isolada de cada um.

**Causas mais letais**: "Suicídio (presumido)" tem 55,79% de fatalidade — mas é um caso à parte (intenção, não falha de trânsito). Excluindo esse outlier, "Pedestre andava na pista" (41,25%) é a causa comportamental mais letal, reforçando que atropelamento é uma das frentes mais críticas do projeto.

**Condição meteorológica**: nevoeiro/neblina tem a maior % de fatalidade (10,85%) entre as condições climáticas — mas está longe de ser a causa dominante em volume, o que confirma a observação já registrada na Unidade 2: o clima **não é o fator central**, é só um agravante pontual.

## Por que isso importa para o projeto como um todo
A Unidade 3 é o ponto em que a hipótese "quais fatores mais influenciam a fatalidade" (levantada no README raiz) começa a ganhar resposta quantitativa: **UF, tipo de pista e tipo de acidente** aparecem como os fatores com maior poder discriminante — muito mais do que o clima, por exemplo. Essa priorização é o que orienta as variáveis usadas depois na base modelável da Unidade 4.

