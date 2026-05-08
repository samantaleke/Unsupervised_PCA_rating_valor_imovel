# PCA / Análise Fatorial — Indicador Sintético para Imóveis

## Objetivo do projeto

Este projeto tem como objetivo criar um **indicador sintético para critério de preço de imóveis**, utilizando **PCA** / **Análise Fatorial**.

A ideia principal é consolidar várias características dos imóveis em uma única métrica, permitindo criar um **ranking de imóveis** com base em fatores extraídos das variáveis originais.

---

## Sobre o problema

A avaliação de imóveis normalmente envolve diversas variáveis, como:

- área do imóvel;
- quantidade de quartos;
- quantidade de banheiros;
- vagas de garagem;
- andar;
- distância até o metrô;
- idade do imóvel;
- condomínio;
- IPTU.

Analisar essas variáveis separadamente pode dificultar a criação de um critério único de comparação. Por isso, foi aplicada a técnica de **PCA**, com o objetivo de reduzir a dimensionalidade dos dados e gerar um indicador consolidado.

---

## Variáveis utilizadas na PCA

As seguintes variáveis foram utilizadas na análise:

| Variável | Descrição |
|---|---|
| `area_m2` | Área do imóvel em metros quadrados |
| `quartos` | Quantidade de quartos |
| `banheiros` | Quantidade de banheiros |
| `vagas_garagem` | Quantidade de vagas de garagem |
| `andar` | Andar do imóvel |
| `dist_metro_m` | Distância até o metrô em metros |
| `idade_imovel_anos` | Idade do imóvel em anos |
| `condominio_rs` | Valor do condomínio |
| `iptu_anual_rs` | Valor anual do IPTU |

---

## Variáveis removidas da PCA

Algumas colunas foram removidas da análise para evitar interferência direta no indicador:

| Variável | Motivo da remoção |
|---|---|
| `id_imovel` | Apenas identificador do imóvel |
| `preco_venda_rs` | Valor real do imóvel, usado apenas para validação final |
| `preco_m2_rs` | Valor por metro quadrado, também relacionado diretamente ao preço |
| `bairro` | Variável categórica |
| `tipo` | Variável categórica |

---

## Etapas da análise

A análise foi organizada na seguinte ordem:

1. Verificação das variáveis métricas;
2. Identificação de possíveis outliers;
3. Cálculo da matriz de correlação de Pearson;
4. Teste de esfericidade de Bartlett;
5. Extração dos autovalores;
6. Aplicação do critério de Kaiser;
7. Análise dos autovetores;
8. Interpretação das cargas fatoriais;
9. Avaliação das comunalidades;
10. Extração dos fatores;
11. Cálculo dos scores fatoriais;
12. Criação do ranking final dos imóveis.

---

## Lógica do indicador

O indicador foi criado por meio da ponderação dos fatores extraídos pela respectiva variância explicada.

A lógica é dar **maior peso aos fatores que concentram maior quantidade de informação** dos dados originais.

```math
Indicador_i =
F_{1i} \cdot Var(F_1)
+
F_{2i} \cdot Var(F_2)
+
\cdots
+
F_{ki} \cdot Var(F_k)
