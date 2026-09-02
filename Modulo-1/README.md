# Modulo-1-Aponti-PRF

Análise de acidentes de trânsito em rodovias federais (dados abertos da PRF, 2025), com foco em entender **o que mais influencia a ocorrência de vítimas fatais**. O mesmo problema é atacado 4 vezes, cada uma com uma ferramenta diferente (Excel e Python), para construir a mesma análise em profundidade crescente — da exploração inicial até uma base pronta para modelagem preditiva. A consolidação final do projeto (Unidade 5) está no [Modulo-2](../Modulo-2).

## Sobre a base
Dados abertos da PRF — 72.529 registros de acidentes em rodovias federais em 2025. Cada linha é uma ocorrência (não um veículo ou uma pessoa envolvida).

**Variável-alvo, usada de forma idêntica em todas as unidades:**
`acidente_fatal = 1` quando `mortos >= 1`; caso contrário, `acidente_fatal = 0`.

## Estrutura do módulo

| Unidade | Tecnologia | O que faz | README |
|---|---|---|---|
| [Unidade 1](./Unidade%201) | Excel | Primeira organização da base bruta: resumo estatístico, painel de consulta e tabelas auxiliares. | [ver](./Unidade%201/README.md) |
| [Unidade 2](./Unidade%202) | Excel (Tabelas Dinâmicas) | Cruzamentos entre variáveis (dia×turno, causa×rodovia, tipo de pista×UF) e primeiras conclusões registradas. | [ver](./Unidade%202/README.md) |
| [Unidade 3](./Unidade%203) | SQL (SQLite) | Views e agregações formais: % de fatalidade por UF, BR, causa, clima e tipo de pista, mais o cálculo de **lift** (risco relativo à média nacional). | [ver](./Unidade%203/README.md) |
| [Unidade 4](./Unidade%204) | Python (Pandas) | Limpeza e preparação completa dos dados, com validação de regras e checagem de *data leakage*, gerando uma base analítica e uma base modelável. | [ver](./Unidade%204/README.md) |

## Objetivo
Entender quais fatores estão mais associados a acidentes com vítimas fatais, testando a mesma pergunta com a mesma base em ferramentas diferentes — e usando cada tecnologia para checar (e não só repetir) o que a anterior encontrou.

## Conclusão consolidada deste módulo

Passando pelas 4 unidades, um padrão se repete de forma consistente, independente da ferramenta usada: **volume de acidentes e gravidade não andam juntos.**

- **Tipo de acidente**: os tipos mais *frequentes* (colisão traseira, saída de pista) têm letalidade relativamente baixa (~4–6%). Os mais *letais* — atropelamento de pedestre (~24–30%) e colisão frontal (~20–29%) — não são os mais comuns, mas concentram a maior parte do risco.
- **Tipo de pista**: pista simples tem quase o dobro da taxa de fatalidade da pista dupla (9,86% vs. 4,88%) — um dos achados mais "acionáveis" do projeto, porque aponta diretamente para investimento em infraestrutura.
- **Localização (UF)**: estados com menor volume de acidentes (MA, PA) aparecem com as maiores taxas de fatalidade — sugerindo pior infraestrutura viária e/ou tempo de resposta mais lento, não necessariamente mais acidentes.
- **Fase do dia**: acidentes à noite e ao amanhecer são desproporcionalmente mais graves que os do período diurno, mesmo com menos ocorrências.
- **Clima**: ao contrário do que se poderia supor, condição climática se mostrou um fator **secundário** em todas as unidades — a maioria dos acidentes graves acontece a céu aberto. O risco está mais ligado a via, horário e tipo de colisão do que ao tempo.

Esses achados são validados de forma cruzada (3 tecnologias diferentes chegando à mesma conclusão) e depois consolidados, com KPIs finais e relatório completo, no [Modulo-2](../Modulo-2).

## Tecnologias
Excel · SQL (SQLite) · Python (Pandas)

## Autor
Eliton Gabriel Silva Cordeiro