
# Unidade 4 — Preparação dos Dados em Python (Pandas)

## Tecnologia
Python (Pandas, NumPy, Matplotlib) — notebook Jupyter

## Objetivo
Diferente das unidades anteriores (que já analisam), a Unidade 4 é a etapa de **engenharia de dados**: pegar a base bruta da PRF e transformá-la em duas bases prontas para uso — uma para exploração/dashboards, outra para modelagem preditiva — resolvendo de forma sistemática e documentada os problemas clássicos de dados públicos (encoding, tipos, nulos, texto sujo). No fluxo CRISP-DM, essa é a fase de *Data Preparation*, revisitando *Data Understanding*.

## Estrutura de pastas
```
Unidade 4/
├── dados_brutos/acidentes2025.csv          # base original da PRF
├── dados_tratados/
│   ├── base_analitica_prf_2025.csv         # para EDA e Power BI
│   ├── base_modelavel_prf_2025.csv         # para modelagem, sem data leakage
│   └── dicionario_variaveis_modulo4.csv    # dicionário das variáveis criadas
├── logs/decisoes_tratamento_modulo4.md     # registro das decisões de limpeza
├── notebooks/Modulo4_Python_Preparacao_Dados.ipynb
└── README.md
```

## O que o notebook faz, passo a passo
1. **Leitura robusta do CSV** — função com fallback de encoding (`latin1` → `utf-8` → `utf-8-sig`), porque dados abertos de governo frequentemente vêm com encoding inconsistente.
2. **Padronização de nomes de colunas** — minúsculas, sem acento, com underline, via `unicodedata.normalize`.
3. **Diagnóstico de qualidade** — tipos de dados, % de nulos por coluna, duplicidade exata, cardinalidade das categóricas.
4. **Conversões de tipo** — colunas numéricas com `errors="coerce"`, incluindo um detalhe sutil: o campo `km` chega com vírgula decimal (`"546,2"`), então é normalizado para ponto antes da conversão — um erro comum que quebraria silenciosamente os cálculos se não fosse tratado.
5. **Variáveis temporais derivadas** — `ano`, `mes`, `trimestre`, `dia_semana_num`, `fim_de_semana`, `hora`, `turno` e `faixa_horaria` (blocos de 3h), todas a partir de `data_inversa` e `horario`.
6. **Padronização de texto** — todas as colunas categóricas viram maiúsculas, strip, e valores tipo `"NAN"/"NULL"/""` viram nulo de verdade (não string).
7. **Tratamento de nulos** — categóricas relevantes preenchidas como `IGNORADO` (preserva o registro sem inventar categoria); contagens de vítimas nulas viram `0`.
8. **Variável-alvo `acidente_fatal`** — criada como `1` se `mortos >= 1`, com uma etapa própria só para **validar a regra** (assert de que não existe violação lógica) antes de seguir.
9. **Indicadores de gravidade** — `total_vitimas`, `acidente_grave`, `indice_gravidade` (peso 3 para morto, 2 para ferido grave, 1 para ferido leve — uma métrica de severidade contínua, não binária).
10. **`br_formatada` e `chave_localidade`** — chaves padronizadas (`BR-116`, `UF_MUNICIPIO_BR-000`) para facilitar joins e agrupamentos em ferramentas de BI depois.
11. **Duas bases finais**:
    - **Base analítica**: mantém tudo, incluindo `mortos`/`feridos` — serve para EDA e Power BI.
    - **Base modelável**: remove explicitamente variáveis que vazam o resultado (`mortos`, `feridos`, `indice_gravidade`, `classificacao_acidente` etc.) — só entra o que seria conhecido *antes* do desfecho do acidente. Essa etapa tem uma função dedicada, `verificar_data_leakage`, que lança erro se qualquer variável proibida sobrar na base. É a diferença entre um projeto de análise ingênuo e um preparado de verdade para treinar um modelo.
12. **Reabertura e validação** — depois de exportar os CSVs, o notebook lê os arquivos de volta e confere se o número de linhas bate, garantindo que a exportação não corrompeu nada.
13. **Documentação automática** — o próprio notebook gera o `README.md` da unidade, o dicionário de variáveis e o log de decisões — ou seja, a documentação não foi escrita à parte, é reprodutível junto com o código.

## Resultado desta execução
- **72.529 acidentes** processados, **7,18% classificados como fatais** (`acidente_fatal = 1`).
- Zero violações lógicas na variável-alvo (validado via assert).
- Zero data leakage confirmado na base modelável.

## Por que essa unidade é o "elo" do projeto
As Unidades 1–3 já tinham chegado a conclusões (UF, tipo de pista e tipo de acidente como fatores mais discriminantes). A Unidade 4 pega exatamente essa mesma regra de negócio (`acidente_fatal`) e a mesma seleção de variáveis relevantes, e as prepara de forma **auditável e sem vazamento de dados** para virarem, na prática, insumo de um modelo preditivo — o que é o passo natural depois de uma análise exploratória sólida.
