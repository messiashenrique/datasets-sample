# Datasets didáticos — Comparação entre grupos e medidas pareadas

Sete bases para praticar comparação de variáveis quantitativas no **Jamovi**: teste t de Student, ANOVA e alternativas baseadas em postos. O propósito é aprender a escolher e interpretar a análise a partir do delineamento e dos dados.

> Os arquivos não documentam sua origem ou o processo de coleta. As perguntas abaixo são propostas didáticas; os resultados não devem ser tomados como evidência de causalidade ou extrapolados sem informações sobre amostragem e delineamento. As unidades são indicadas apenas quando estão explícitas no nome da variável ou podem ser identificadas com segurança; nos demais casos, devem ser confirmadas.

## Arquivos e objetivos

| Arquivo | Variável quantitativa | Comparação | N | Análise principal proposta |
|---|---|---|---:|---|
| [`ne_hs_3g.csv`](ne_hs_3g.csv) | `Horas_Sono` | Três níveis de estresse | 105 | Kruskal–Wallis |
| [`glicemia_a_d.csv`](glicemia_a_d.csv) | `glicemia_antes` e `glicemia_depois` | Antes e depois, mesmas pessoas | 60 pares | t pareado |
| [`filtro_vitd.csv`](filtro_vitd.csv) | `vitamina_d_ng_ml` | Dois grupos independentes | 60 | t independente |
| [`app_sono.csv`](app_sono.csv) | `tempo_sono_horas` | Dois grupos independentes | 60 | t independente |
| [`af_ps.csv`](af_ps.csv) | `pressao_sistolica` | Dois grupos independentes | 60 | t independente |
| [`af_imc_3g.csv`](af_imc_3g.csv) | `IMC` | Três grupos independentes | 90 | ANOVA de um fator |
| [`af_col_3g.csv`](af_col_3g.csv) | `colesterol_total` | Três grupos independentes | 60 | ANOVA de um fator |

Os CSVs têm cabeçalho, vírgula como separador e ponto decimal. Cada linha é uma observação; `id` ou `Participante` é um identificador. As análises de grupos independentes pressupõem que cada linha corresponda a uma pessoa independente; os arquivos, por si só, não comprovam essa condição.

## Escolha do teste e pressupostos

1. **Duas medidas da mesma pessoa:** examine a distribuição das diferenças e use t pareado para comparar a diferença média. Wilcoxon pareado é uma alternativa baseada nos postos das diferenças, com pressuposto de simetria para a interpretação usual como deslocamento de localização.
2. **Dois grupos independentes:** o t de Student compara médias com variâncias populacionais iguais. O t de Welch permite variâncias diferentes. Mann–Whitney compara postos/distribuições e pode ser útil diante de assimetria acentuada ou valores extremos.
3. **Três ou mais grupos independentes:** a ANOVA clássica compara médias sob homogeneidade de variâncias; a ANOVA de Welch relaxa essa exigência. Kruskal–Wallis compara postos/distribuições e é uma alternativa quando a análise de médias não é adequada.

Mann–Whitney e Kruskal–Wallis **não são automaticamente testes de igualdade de médias ou medianas**. Uma interpretação como diferença de localização ou de medianas exige condições adicionais, como distribuições de formatos semelhantes. Todos esses testes também dependem de independência entre unidades de análise.

Para os testes paramétricos, inspecione distribuições por grupo ou resíduos do modelo, gráficos Q–Q e valores extremos. No t pareado, examine as **diferenças**, não apenas cada momento separadamente. Shapiro–Wilk e Levene complementam os gráficos, mas um valor de p acima de 0,05 não prova um pressuposto; um valor abaixo de 0,05 tampouco obriga, isoladamente, a trocar de teste. Avalie tamanho amostral, assimetria, extremos e objetivo da análise. Valores extremos devem ser investigados, não excluídos automaticamente.

## 1. Estresse e horas de sono — três grupos

**Pergunta:** a distribuição de `Horas_Sono` difere entre os níveis de `Nível_Estresse`?

| Nível de estresse | n | Média ± DP (horas) | Mediana (Q1–Q3) |
|---|---:|---:|---:|
| Baixo | 35 | 7,02 ± 3,48 | 5,89 (5,03–8,40) |
| Moderado | 35 | 6,54 ± 3,49 | 5,65 (4,11–7,03) |
| Alto | 35 | 4,64 ± 2,98 | 3,53 (2,96–5,53) |

- **Diagnóstico:** Shapiro–Wilk por grupo apresenta p < 0,001 nos três grupos. Há assimetria à direita e valores extremos, como **22,75 horas** no grupo baixo, **19,45** no moderado e **18,12** no alto. Levene, centrado na mediana, p = 0,727. Os valores elevados merecem verificação contextual; foram mantidos no cálculo.
- **Análise proposta:** Kruskal–Wallis, H(2) = **19,11**, p < 0,001. Há evidência de diferença entre as distribuições dos grupos.
- **Comparações exploratórias:** Mann–Whitney bilateral em cada par, com correção de Holm: baixo × alto, p ajustado < 0,001; moderado × alto, p ajustado = 0,0026; baixo × moderado, p ajustado = 0,335. Foram usados postos médios para empates e aproximação assintótica com correção de continuidade.
- **Interpretação:** o grupo de estresse alto apresenta mediana e postos de sono menores na amostra. As diferenças de formato e os extremos recomendam cautela ao interpretar o teste como comparação exclusiva de medianas.

## 2. Glicemia antes e depois — medidas pareadas

**Pergunta:** qual é a diferença média entre `glicemia_antes` e `glicemia_depois` nas mesmas 60 pessoas? A unidade da glicemia não está informada no arquivo.

| Medida | n | Média ± DP |
|---|---:|---:|
| Antes | 60 | 124,90 ± 6,32 |
| Depois | 60 | 115,87 ± 6,50 |
| Diferença: antes − depois | 60 | 9,03 ± 2,05 |

- **Diagnóstico:** Shapiro–Wilk das diferenças, p = 0,124; complemente com Q–Q e inspeção de extremos.
- **Teste t pareado:** t(59) = **34,13**, p < 0,001; diferença média antes − depois = **9,03**, IC95% **8,50 a 9,56**.
- **Interpretação:** a glicemia depois foi, em média, 9,03 unidades menor nesta amostra. Não há informação suficiente para atribuir a mudança a uma intervenção específica.
- **Alternativa:** Wilcoxon pareado, quando adequado às diferenças; o teste não equivale a comparar duas amostras independentes.

## 3. Uso de filtro e vitamina D — dois grupos

**Pergunta:** a média de `vitamina_d_ng_ml` difere entre os grupos de `grupo`?

| Grupo | n | Média ± DP (ng/mL) |
|---|---:|---:|
| Usa filtro | 30 | 31,09 ± 2,11 |
| Não usa filtro | 30 | 31,12 ± 2,17 |

- **Diagnóstico:** Shapiro–Wilk p = 0,557 e 0,452; Levene p = 0,878.
- **Teste t independente de Student:** t(58) = **−0,05**, p = **0,962**; diferença usa − não usa = **−0,03 ng/mL**, IC95% **−1,13 a 1,08**.
- **Interpretação:** não há evidência de diferença de médias nesta amostra. O intervalo descreve diferenças compatíveis com os dados; um resultado não significativo não demonstra igualdade.

## 4. Aplicativo e tempo de sono — dois grupos

**Pergunta:** a média de `tempo_sono_horas` difere entre os grupos de `grupo`?

| Grupo | n | Média ± DP (horas) |
|---|---:|---:|
| Usa App | 30 | 6,92 ± 0,25 |
| Não usa App | 30 | 6,91 ± 0,24 |

- **Diagnóstico:** Shapiro–Wilk p = 0,383 e 0,108; Levene p = 0,924.
- **Teste t independente de Student:** t(58) = **0,26**, p = **0,796**; diferença usa − não usa = **0,017 hora**, IC95% **−0,112 a 0,145 hora**.
- **Interpretação:** a diferença média observada é pequena e o intervalo inclui zero. O resultado não comprova equivalência nem efeito do aplicativo.

## 5. Atividade física e pressão sistólica — dois grupos

**Pergunta:** a média de `pressao_sistolica` difere entre as categorias de `atividade_fisica`? A unidade da pressão não está informada no arquivo.

| Grupo | n | Média ± DP |
|---|---:|---:|
| Sedentario | 30 | 144,37 ± 5,30 |
| Ativo | 30 | 127,13 ± 3,92 |

- **Diagnóstico:** Shapiro–Wilk p = 0,643 e 0,562; Levene p = 0,072. A dispersão difere numericamente; Welch é uma análise útil de sensibilidade.
- **Teste t independente de Student:** t(58) = **14,32**, p < 0,001; diferença sedentário − ativo = **17,23**, IC95% **14,82 a 19,64**.
- **Interpretação:** a média observada foi maior entre sedentários. O resultado não estabelece que a atividade física tenha causado a diferença.

## 6. Atividade física e IMC — três grupos

**Pergunta:** o IMC médio difere entre as categorias de `Nível_Atividade`?

| Grupo | n | Média ± DP de IMC |
|---|---:|---:|
| Sedentário | 30 | 28,43 ± 2,69 |
| Moderadamente Ativo | 30 | 25,64 ± 2,80 |
| Ativo | 30 | 23,04 ± 2,98 |

- **Diagnóstico:** Shapiro–Wilk por grupo: p = 0,651; 0,917; 0,350, respectivamente. Levene p = 0,849. Examine também os gráficos e a observação de IMC 15,1 no grupo ativo.
- **ANOVA clássica:** F(2, 87) = **27,31**, p < 0,001. Há evidência de que pelo menos uma média difere das demais.
- **Tukey:** sedentário − moderadamente ativo = **2,79** (p ajustado = 0,001); sedentário − ativo = **5,39** (p ajustado < 0,001); moderadamente ativo − ativo = **2,60** (p ajustado = 0,002).
- **Interpretação:** na amostra, o IMC médio diminui na sequência apresentada. O teste global não identifica sozinho quais pares diferem.

## 7. Atividade física e colesterol — três grupos

**Pergunta:** o `colesterol_total` médio difere entre as categorias de `grupo`? A unidade do colesterol não está informada no arquivo.

| Grupo | n | Média ± DP |
|---|---:|---:|
| Sedentário | 20 | 246,05 ± 5,48 |
| Moderadamente Ativo | 20 | 221,50 ± 5,11 |
| Ativo | 20 | 196,65 ± 5,08 |

- **Diagnóstico:** Shapiro–Wilk por grupo: p = 0,687; 0,735; 0,764, respectivamente. Levene p = 0,899.
- **ANOVA clássica:** F(2, 57) = **446,27**, p < 0,001.
- **Tukey:** sedentário − moderadamente ativo = **24,55**; sedentário − ativo = **49,40**; moderadamente ativo − ativo = **24,85**. Para os três pares, p ajustado < 0,001.
- **Interpretação:** os três grupos apresentam médias distintas na amostra, com médias menores nas categorias mais ativas. Não se pode inferir causalidade a partir dessa comparação.

## Como analisar no Jamovi

Os nomes dos menus podem variar conforme a versão e o idioma.

1. Em **Abrir → Este computador**, importe o CSV. Confira os acentos, os valores decimais e os tipos: identificador como ID, variável de grupo como nominal ou ordinal e medidas numéricas como contínuas.
2. Em **Exploração → Descritivas**, inclua a medida e divida por grupo. Solicite n, média, desvio-padrão, mediana, quartis, histogramas, boxplots e gráficos Q–Q. Para a glicemia, crie a variável calculada `glicemia_antes - glicemia_depois` e examine sua distribuição.
3. Para dois grupos, vá a **Testes T → Teste T para amostras independentes**. Coloque a medida em variáveis dependentes e o grupo em agrupamento. Selecione Student ou Welch; marque descritivas, intervalo de confiança e verificações de pressupostos. Mann–Whitney pode ser selecionado na mesma análise.
4. Para glicemia, use **Testes T → Teste T para amostras pareadas** e forme o par `glicemia_antes` / `glicemia_depois` nessa ordem. Selecione t pareado, IC e, se desejado, Wilcoxon. A ordem altera o sinal da diferença.
5. Para três grupos, acesse **ANOVA → ANOVA de um fator** ou **ANOVA**, conforme as opções disponíveis. Indique a medida como dependente e a categoria como fator; solicite homogeneidade, descritivas e pós-teste de Tukey. Considere Welch e pós-teste apropriado, como Games–Howell, quando houver heterogeneidade.
6. Para `ne_hs_3g.csv`, selecione **Kruskal–Wallis** na análise não paramétrica de um fator, quando disponível. Para reproduzir as comparações indicadas, faça Mann–Whitney para cada par e aplique Holm aos três valores de p, caso sua versão não ofereça esse ajuste diretamente.
7. Registre o teste, a ordem das comparações, estatística, graus de liberdade quando aplicáveis, p, estimativa e IC quando disponíveis. Um resultado exibido como `p = 0,000` deve ser relatado como **p < 0,001**.

## Resumo comparativo e gabarito

| Dataset | Análise principal | Resultado | Conclusão ao nível de 5% |
|---|---|---|---|
| Estresse e sono | Kruskal–Wallis | H(2) = 19,11; p < 0,001 | Distribuições diferem entre grupos |
| Glicemia | t pareado | t(59) = 34,13; p < 0,001 | Diferença média antes − depois positiva |
| Filtro e vitamina D | t independente | t(58) = −0,05; p = 0,962 | Evidência insuficiente de diferença média |
| App e sono | t independente | t(58) = 0,26; p = 0,796 | Evidência insuficiente de diferença média |
| Atividade e pressão | t independente | t(58) = 14,32; p < 0,001 | Média maior no grupo sedentário |
| Atividade e IMC | ANOVA | F(2, 87) = 27,31; p < 0,001 | Pelo menos uma média difere |
| Atividade e colesterol | ANOVA | F(2, 57) = 446,27; p < 0,001 | Pelo menos uma média difere |

### Questões sugeridas para os estudantes

1. Por que a glicemia exige um teste pareado? O que muda se a ordem antes − depois for invertida?
2. Que padrão nos dados de estresse e sono motivou a análise por postos? Como investigar os valores elevados?
3. Qual é a diferença entre Student e Welch? Quando a ANOVA de Welch é útil?
4. Por que o resultado global da ANOVA não diz, por si só, quais grupos diferem?
5. Por que ajustar os valores de p ao realizar várias comparações entre pares?
6. Um resultado não significativo demonstra que os grupos são equivalentes? Como o intervalo de confiança ajuda?
7. Sob quais condições uma diferença em postos pode ser interpretada como diferença de medianas?

---

**Nota metodológica:** resultados bilaterais, com nível de 5%, calculados a partir dos CSVs completos, sem exclusões. O desvio-padrão é amostral; Q1 e Q3 usam interpolação linear nas posições 25% e 75%. Shapiro–Wilk foi aplicado por grupo ou às diferenças pareadas; Levene foi centrado na mediana. Os ICs de diferenças usam a distribuição t e os testes de Student indicados assumem variâncias iguais. Tukey controla o erro familiar nos três pares; Holm foi aplicado aos três testes de Mann–Whitney do exemplo de sono. Arredondamento, definição de quartis, tratamento de empates e métodos do software podem causar pequenas diferenças. As análises dependem da independência das pessoas e não ajustam possíveis fatores de confusão.
