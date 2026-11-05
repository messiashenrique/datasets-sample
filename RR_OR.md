# Datasets didáticos — Estudos caso-controle e de coorte

Conjunto de quatro bases de dados **inteiramente sintéticas** para aulas práticas de Epidemiologia e Bioestatística, especialmente no **Jamovi**. O objetivo é calcular e interpretar medidas de associação em tabelas 2 × 2: **Odds Ratio (OR)** em estudos caso-controle e **Risco Relativo (RR)** em estudos de coorte.

> **Aviso:** os valores foram definidos artificialmente para fins pedagógicos. As associações aqui apresentadas não constituem evidência empírica sobre tabagismo, fibras, sedentarismo ou atividade física. Resultados observacionais não demonstram causalidade por si só.

## Arquivos e objetivos

| Arquivo CSV | Delineamento | Exposição | Desfecho | N | Medida esperada |
|---|---|---|---|---:|---:|
| [`1-cc_or.csv`](1-cc_or.csv) | Caso-controle | Tabagismo prévio | Doença respiratória crônica | 160 | OR = 3,45 |
| [`2-cc_or.csv`](2-cc_or.csv) | Caso-controle | Consumo regular de fibras | Doença cardiovascular | 160 | OR = 0,74; IC95% inclui 1 |
| [`3-coorte_rr.csv`](3-coorte_rr.csv) | Coorte | Sedentarismo | Hipertensão incidente | 200 | RR = 2,50 |
| [`4-coorte_rr.csv`](4-coorte_rr.csv) | Coorte | Atividade física regular | Hipertensão incidente | 200 | RR = 0,375; IC95% não inclui 1 |

Todos os arquivos CSV usam **vírgula como separador**, **ponto de partida em uma linha de cabeçalho** e valores categóricos `Sim`/`Nao`, sem acentos, para simplificar a importação. Cada linha representa uma pessoa; o campo `id` é apenas um identificador.

## 1. Caso-controle: tabagismo e doença respiratória crônica

**Pergunta:** existe associação entre histórico de tabagismo e doença respiratória crônica?

O estudo fictício selecionou **80 casos** (com a doença) e **80 controles** (sem a doença). A exposição investigada foi o histórico de tabagismo. Para a análise, utilize `tabagismo_previo` × `doenca_respiratoria` (ou `grupo`).

| Tabagismo prévio | Casos | Controles |
|---|---:|---:|
| Sim | 52 | 28 |
| Não | 28 | 52 |
| **Total** | **80** | **80** |

Para uma tabela 2 × 2, com `a` = expostos doentes, `b` = expostos não doentes, `c` = não expostos doentes e `d` = não expostos não doentes:

$$
OR=\frac{a\times d}{b\times c}=\frac{52\times52}{28\times28}=\mathbf{3{,}45}
$$

- **IC95% aproximado do OR:** **1,80 a 6,60**.
- **Interpretação:** indivíduos com tabagismo prévio apresentam aproximadamente **3,45 vezes as odds** de doença, quando comparados aos não expostos.
- **Significância:** o IC95% está totalmente acima de 1, indicando associação estatisticamente significativa ao nível de 5%.
- **Cuidado:** não interpretar OR = 3,45 como “3,45 vezes o risco”; em um caso-controle tradicional não se estima diretamente a incidência populacional a partir das proporções de casos e controles selecionados.

## 2. Caso-controle: fibras e doença cardiovascular

**Pergunta:** existe associação entre consumo regular de fibras e doença cardiovascular?

O estudo fictício selecionou **80 casos** e **80 controles**. Use `consumo_regular_fibras` × `doenca_cardiovascular` (ou `grupo`).

| Consumo regular de fibras | Casos | Controles |
|---|---:|---:|
| Sim | 34 | 40 |
| Não | 46 | 40 |
| **Total** | **80** | **80** |

$$
OR=\frac{34\times40}{40\times46}=\mathbf{0{,}74}
$$

- **IC95% aproximado do OR:** **0,40 a 1,38**.
- **Interpretação:** o OR sugere odds aproximadamente **26% menores** de doença entre consumidores regulares de fibras.
- **Significância:** o IC95% **inclui 1**. Portanto, não há evidência estatística suficiente, ao nível de 5%, para afirmar que exista associação nesta amostra simulada.
- **Cuidado:** ausência de significância não equivale a prova de ausência de efeito. O intervalo é compatível tanto com associação protetora quanto com aumento discreto das odds.

## 3. Coorte: sedentarismo e hipertensão arterial

**Pergunta:** o sedentarismo está associado a maior incidência de hipertensão?

A coorte fictícia acompanhou **200 adultos**, todos **sem hipertensão no início**, durante **12 meses completos**, sem perdas de acompanhamento: 100 sedentários e 100 não sedentários. Use `exposicao_sedentarismo` × `caso_incidente`.

| Sedentarismo | Hipertensão incidente: Sim | Não | Total |
|---|---:|---:|---:|
| Sim (expostos) | 30 | 70 | 100 |
| Não (não expostos) | 12 | 88 | 100 |
| **Total** | **42** | **158** | **200** |

**Incidência acumulada em 12 meses:**

$$
I_E=\frac{30}{100}=30\% \qquad I_{NE}=\frac{12}{100}=12\%
$$

**Risco Relativo:**

$$
RR=\frac{I_E}{I_{NE}}=\frac{0{,}30}{0{,}12}=\mathbf{2{,}50}
$$

- **IC95% aproximado do RR:** **1,36 a 4,60**.
- **Diferença absoluta de riscos:** 30% − 12% = **18 pontos percentuais**.
- **Interpretação:** a incidência acumulada entre sedentários foi **2,5 vezes** a incidência entre não sedentários durante os 12 meses de acompanhamento.
- **Significância:** o IC95% está totalmente acima de 1, indicando associação estatisticamente significativa ao nível de 5%.

## 4. Coorte: atividade física e hipertensão arterial

**Pergunta:** a atividade física regular está associada a menor incidência de hipertensão?

Outra coorte fictícia acompanhou **200 adultos sem hipertensão inicial**, durante **12 meses completos**, sem perdas: 100 praticantes regulares de atividade física e 100 sem atividade física regular. Use `atividade_fisica_regular` × `caso_incidente`.

| Atividade física regular | Hipertensão incidente: Sim | Não | Total |
|---|---:|---:|---:|
| Sim (expostos) | 12 | 88 | 100 |
| Não (não expostos) | 32 | 68 | 100 |
| **Total** | **44** | **156** | **200** |

**Incidência acumulada em 12 meses:**

$$
I_E=\frac{12}{100}=12\% \qquad I_{NE}=\frac{32}{100}=32\%
$$

**Risco Relativo:**

$$
RR=\frac{0{,}12}{0{,}32}=\mathbf{0{,}375}
$$

- **IC95% aproximado do RR:** **0,205 a 0,685**.
- **Redução relativa de risco observada:** (1 − 0,375) × 100 = **62,5%**.
- **Diferença absoluta de riscos:** 12% − 32% = **−20 pontos percentuais**.
- **Interpretação:** a incidência entre indivíduos fisicamente ativos foi aproximadamente **62,5% menor** que entre os não ativos.
- **Significância:** o IC95% está totalmente abaixo de 1, indicando associação estatisticamente significativa ao nível de 5%. O delineamento observacional, isoladamente, não demonstra que a exposição cause a redução do risco.

## Como analisar no Jamovi

1. Abra um dos arquivos CSV em **Abrir → Este computador** e confira se as variáveis `Sim`/`Nao` foram reconhecidas como **nominais**.
2. Acesse **Análises → Frequências → Tabelas de contingência → Amostras independentes** (a nomenclatura pode variar conforme a versão).
3. Coloque a **exposição** nas linhas e o **desfecho** nas colunas, organizando `Sim` antes de `Nao` para reproduzir as tabelas acima. A orientação das categorias é essencial: inverter linhas ou colunas pode produzir a medida recíproca.
4. Habilite frequências observadas, percentuais apropriados e, conforme o delineamento, **Odds Ratio** ou **Risco Relativo**, com **IC95%**.
5. Se desejado, habilite o teste **Qui-quadrado** de independência. Interprete separadamente **magnitude**, **direção**, **precisão** e **significância** da associação.
6. Nos estudos de coorte, calcule também as incidências acumuladas usando o número de **casos novos / participantes inicialmente sob risco** em cada grupo.

**Orientação das tabelas:** para a fórmula `a, b, c, d` usada neste README, o desfecho `Sim` fica na primeira coluna, o desfecho `Nao` na segunda, a exposição `Sim` na primeira linha e a exposição `Nao` na segunda.

## Como os intervalos de confiança foram calculados

Os valores apresentados são intervalos **aproximados de Wald, calculados na escala logarítmica**, com `z = 1,96`. Dependendo do software, da configuração de continuidade ou do método de intervalo de confiança empregado, podem ocorrer pequenas diferenças.

Para **OR**:

$$
\mathrm{IC}_{95\%}(\mathrm{OR}) = e^{\log(\mathrm{OR}) \pm 1.96\sqrt{\frac{1}{a}+\frac{1}{b}+\frac{1}{c}+\frac{1}{d}}}
$$

Para **RR**, com `a` e `b` no grupo exposto e `c` e `d` no não exposto (método logarítmico de Katz):

$$
\mathrm{IC}_{95\%}(RR)=\exp\left[\ln(RR)\pm1{,}96\sqrt{\frac{1}{a}-\frac{1}{a+b}+\frac{1}{c}-\frac{1}{c+d}}\right]
$$

Em ambos os casos, o valor **1** representa ausência de associação na escala relativa. Se um IC95% bilateral incluir 1, não se rejeita a hipótese de associação nula em um teste correspondente ao nível de 5%.

## Resumo comparativo e gabarito

| Estudo | Medida | IC95% aproximado | Inclui 1? | Interpretação didática |
|---|---:|---:|---|---|
| Caso-controle: tabagismo | OR = **3,45** | 1,80–6,60 | Não | Associação positiva e significativa |
| Caso-controle: fibras | OR = **0,74** | 0,40–1,38 | **Sim** | Associação protetora sugerida, sem significância estatística |
| Coorte: sedentarismo | RR = **2,50** | 1,36–4,60 | Não | Maior incidência entre expostos |
| Coorte: atividade física | RR = **0,375** | 0,205–0,685 | Não | Menor incidência entre expostos |

### Questões sugeridas para os estudantes

1. Qual delineamento permite estimar diretamente a incidência acumulada? Por quê?
2. Qual é a diferença conceitual entre **odds** e **risco**?
3. Como interpretar OR ou RR **maior que 1**, **igual a 1** e **menor que 1**?
4. Por que o segundo estudo não permite afirmar associação protetora estatisticamente significativa, embora OR < 1?
5. Qual é a diferença entre **redução relativa** e **diferença absoluta** de risco no quarto estudo?
6. Uma associação estatisticamente significativa é suficiente para concluir causalidade? Justifique.

---

**Nota metodológica:** as coortes representam situações simplificadas, sem censura ou perdas e com o mesmo período de observação para todos. Portanto, seus resultados representam **incidência acumulada**, não taxa de incidência por pessoa-tempo. As variáveis adicionais de idade e sexo foram simuladas para permitir exploração, mas as estimativas apresentadas são **brutas (não ajustadas)**. Os quatro arquivos são exemplos independentes: não devem ser combinados como se representassem os mesmos participantes.
