# Unidade 1 — Primeira Exploração dos Dados (Excel)

## Tecnologia
Excel

## Objetivo
Primeiro contato com a base bruta de acidentes da PRF (72.529 ocorrências, ano de 2025). O foco aqui não é chegar a conclusões definitivas, e sim organizar a base, entender as colunas disponíveis e montar as primeiras estruturas de consulta (resumo estatístico, painel de filtros e tabelas auxiliares) que servem de ponto de partida para as unidades seguintes.

## Arquivo
`atividade 1 (Eliton Gabriel - Julio César).xlsx`

## Estrutura da planilha
| Aba | Conteúdo |
|---|---|
| `Dados` | Base completa, 72.529 linhas × 34 colunas — dados originais da PRF mais 4 colunas calculadas (`Vitimas Feridas`, `Status Fatalidade`, `Taxa de feridos Graves`, `Pontuação de Risco`). |
| `Resumo Estátistico` | Estatísticas descritivas (média, mediana, quartil) e um painel de consulta rápida por ID/causa/condição. |
| `Tabelas Auxiliares` | Tabelas de apoio: distribuição por fase do dia, ranking de causas, top-5 estados por acidentes e evolução mensal. |
| `Análise Visual` | Espaço reservado para os gráficos derivados das tabelas auxiliares. |

## O que foi feito
- Importação e organização da base bruta da PRF em uma aba única e limpa.
- Criação de 4 colunas derivadas direto na aba `Dados`, antecipando o que depois vira `acidente_fatal`, `total_vitimas` e `indice_gravidade` nas unidades de SQL e Python — ou seja, o raciocínio da variável-alvo já nasce aqui, só que manualmente no Excel.
- Construção de tabelas auxiliares agregando por fase do dia, causa e mês, usando fórmulas e tabelas de apoio (não tabela dinâmica ainda — isso vem na Unidade 2).

## Leitura dos dados (o que já dá pra perceber)
Mesmo sendo a etapa mais exploratória, alguns padrões já aparecem nas tabelas auxiliares:
- **Concentração por fase do dia**: `Pleno dia` (40.375) e `Plena Noite` (24.781) concentram a esmagadora maioria dos acidentes, contra bem menos em `Anoitecer` e `Amanhecer` — o que já é uma pista de que volume não é o mesmo que risco (as unidades seguintes mostram que a *noite* tem taxa de fatalidade proporcionalmente pior, apesar do menor volume absoluto).
- **Sazonalidade discreta**: a evolução mensal (jan: 5.528 → dez: 6.788) mostra uma curva relativamente estável ao longo do ano, com leve alta no fim de ano — não há um mês "anômalo" que explique um pico isolado.
- **Causas mais frequentes** aparecem concentradas em fatores comportamentais e de infraestrutura (falhas de pista, condução), o que já antecipa o tipo de causa que a Unidade 3 (SQL) vai quantificar em termos de letalidade, e não só de volume.

## Limitação desta etapa
Nesta unidade ainda não há cálculo de **taxa de fatalidade** propriamente dita (fatais ÷ total) — as tabelas mostram contagens absolutas. É justamente essa lacuna que a Unidade 2 (tabelas dinâmicas) e a Unidade 3 (SQL) resolvem, transformando volume em proporção.
