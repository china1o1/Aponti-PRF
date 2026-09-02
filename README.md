# Aponti-PRF

Repositório com as atividades práticas do curso de Análise de Dados da **Aponti Academy**, usando como base de estudo os dados abertos de acidentes de trânsito em rodovias federais da PRF (2025).

Cada módulo representa uma etapa do curso, praticando uma ferramenta diferente (Excel, SQL, Python) sobre a mesma base de dados — sempre voltando à mesma pergunta: **o que mais influencia a ocorrência de acidentes com vítimas fatais?**

## Sobre a base
Dados abertos da PRF — 72.529 registros de acidentes em rodovias federais em 2025. Cada linha é uma ocorrência (não um veículo ou uma pessoa envolvida).

**Variável-alvo, usada de forma idêntica em todo o projeto:**
`acidente_fatal = 1` quando `mortos >= 1`; caso contrário, `acidente_fatal = 0`.

## Módulos

| Módulo | O que é praticado | README |
|---|---|---|
| [Modulo-1-Aponti-PRF](./Modulo-1-Aponti-PRF) | Excel, Tabelas Dinâmicas, SQL e Python — da primeira exploração da base até a preparação dos dados para modelagem. | [ver](./Modulo-1-Aponti-PRF/README.md) |
| [Modulo-2](./Modulo-2) | Consolidação em Excel (KPIs, rankings) e relatório analítico final em PDF. | [ver](./Modulo-2/Unidade%205/README.md) |

Os achados e conclusões de cada etapa estão detalhados no README de cada módulo.

## Tecnologias
Excel · SQL (SQLite) · Python (Pandas) · Word/PDF

## Autor
Eliton Gabriel Silva Cordeiro
