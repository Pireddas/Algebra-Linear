## ***Introdução***

<div align=justify>
   A modelagem preditiva e a análise de risco dependem diretamente da capacidade de estruturar e manipular grandes volumes de dados de forma eficiente. Por trás dos algoritmos e frameworks computacionais, a Álgebra Linear atua como a linguagem fundamental para a representação de informações, permitindo calcular métricas cruciais no mercado financeiro e na gestão de carteiras de crédito, como Probabilidade de Inadimplência (PD), Perda Dada a Inadimplência (LGD) e Valor em Risco (VaR).
<br><br>
   Contudo, para construir uma intuição sólida sobre a modelagem matemática, é preciso ir além da simples aplicação de métodos, funções e bibliotecas. Este artigo tem como objetivo guiar o estudo por essa base conceitual, partindo das estruturas fundamentais de vetores, matrizes e tensores até a dedução matemática e matricial dos métodos apresentados, permitindo compreender os cálculos que sustentam as bibliotecas de programação.
<br><br>


## ***Álgebra Linear para Modelagem de Risco de Crédito***

A **Álgebra Linear** é a base matemática que fornece estruturas e operações fundamentais para representar, organizar e transformar dados por meio de vetores, matrizes e tensores. Essas estruturas permitem otimizar algoritmos de aprendizado de máquina e realizar operações matemáticas de forma eficiente em grandes volumes de informação.

Ao final desta leitura, deveremos ser capazes de compreender as técnicas utilizadas e a intuição que fundamenta a aplicação dos métodos e ferramentas no processo de modelagem de risco de crédito. Além dos fundamentos práticos e teóricos sobre PD, EAD, LGD, ***Application Score, Behavior Score e Recovery Score***, também serão apresentados conceitos relacionados à segmentação e ao monitoramento de carteiras de crédito, classificação de operações em diferentes estágios de risco (***Stages***), modelagem de capital em risco (VaR) e RAROC (***Risk-Adjusted Return on Capital***), utilizados na gestão e avaliação do risco de crédito.

### ***Vetores***

Um vetor é uma estrutura unidimensional de números dispostos em uma única linha ou coluna. Na **Ciência de Dados**, vetores são frequentemente utilizados para representar uma única amostra, observação ou lista de características (*features*).  

Matematicamente, um vetor coluna em $\mathbb{R}^n$ é representado por uma **matriz coluna** de dimensão $n \times 1$ (com $n$ linhas e $1$ coluna), conforme representação abaixo:  

$$
\vec{v} = \begin{bmatrix} v_1 \\ 
v_2 \\ 
\vdots \\ 
v_n 
\end{bmatrix}
$$ 

Cada elemento $v_i$ representa o valor daquela dimensão específica. Por exemplo, no contexto de machine learning, um vetor pode armazenar as características de um determinado registro (como idade, renda e escolaridade).  

### ***Matrizes***

Uma matriz é uma estrutura bidimensional disposta em linhas e colunas, formando uma tabela de elementos. Na **Ciência de Dados**, uma matriz pode ser utilizada para representar um conjunto completo de dados, em que cada linha representa uma observação e cada coluna representa uma variável ou *feature*.  

Uma matriz $X$ de dimensão $m \times n$ (com $m$ linhas e $n$ colunas) é representada como:  

$$
X = \begin{bmatrix} 
x_{11} & x_{12} & \cdots & x_{1n} \\ 
x_{21} & x_{22} & \cdots & x_{2n} \\ 
\vdots & \vdots & \ddots & \vdots \\ 
x_{m1} & x_{m2} & \cdots & x_{mn} 
\end{bmatrix}
$$

Na regressão linear, a matriz de dados, frequentemente chamada de **matriz de projeto** (*Design Matrix*), é utilizada em operações de álgebra linear para estimar os coeficientes do modelo. Uma formulação clássica da solução por mínimos quadrados é:

$$\vec{\beta} = (X^T X)^{-1} X^T \vec{y}$$

desde que $X^T X$ seja invertível. Na prática, métodos como decomposição QR ou SVD podem ser utilizados para obter a solução de forma numericamente mais estável, evitando a necessidade de calcular explicitamente a matriz inversa.

### ***Tensores***

Um tensor é uma estrutura matemática que generaliza escalares, vetores e matrizes para diferentes ordens ou dimensões.  
-  Um escalar é um tensor de ordem 0 (apenas um número).  
-  Um vetor é um tensor de ordem 1 (uma dimensão).  
-  Uma matriz é um tensor de ordem 2 (duas dimensões).  
-  Um arranjo com 3 ou mais dimensões é um tensor de ordem superior.  

Um exemplo clássico na **Ciência de Dados** é o processamento de imagens coloridas, que consiste na representação da imagem por um tensor de ordem 3 $(\text{altura} \times \text{largura} \times \text{canais de cor})$, em que os canais correspondem às camadas RGB (Red, Green, Blue).  
<br>
Em problemas financeiros, tensores podem representar informações organizadas em múltiplas dimensões, como clientes, safras de originação, períodos de acompanhamento (aging) e variáveis comportamentais. Essa estrutura preserva relações temporais e comportamentais dos dados, possibilitando a aplicação de técnicas estatísticas de análise multivariada para monitoramento de carteiras, otimização das estratégias de cobrança, identificação de padrões de inadimplência e avaliação dos processos de recuperação de crédito.

<br>

## ***Regressão Linear***

A regressão linear é um dos pilares da estatística e da aprendizagem de máquina, servindo como ponto de partida para a modelagem preditiva. Em sua forma simples, o objetivo é encontrar a melhor reta que descreve a relação entre uma única variável independente ($x$) e uma variável resposta ($y$).  

Embora frameworks permitam ajustar esse modelo com apenas uma linha de código, entender os cálculos por trás da minimização dos erros é um grande diferencial na aplicação das técnicas na modelagem estatística.  

Neste artigo, vou explorar passo a passo a dedução matemática do **Método dos Mínimos Quadrados Ordinários (MQO)** e realizar todos os cálculos manualmente para construir uma intuição sólida sobre como o modelo aprende a partir dos dados.

<img width="450" height="300" alt="image" src="https://github.com/user-attachments/assets/871cae46-3a59-42fa-9837-17afb74a2e0c" />  

*Photo by [OPUS Pesquisa](https://www.opuspesquisa.com/) on 
[https://www.opuspesquisa.com/](https://www.opuspesquisa.com/)*

<br>

## ***Estimativa dos mínimos quadrados***

A **Estimativa de Mínimos Quadrados Ordinários (MQO)** — ou *Ordinary Least Squares (OLS)* — é o método matemático utilizado para determinar os parâmetros da reta de regressão, buscando o melhor ajuste possível aos dados observados. O objetivo central é minimizar a soma das distâncias verticais elevadas ao quadrado entre os pontos reais e a reta estimada (os chamados resíduos $e_i$).

<img width="450" height="300" alt="image" src="https://github.com/user-attachments/assets/e8304e60-564a-4a9a-a178-156e869630be" />
 
*Photo by [Sociedade Brasileira de Física](https://www.sbfisica.org.br/) on 
[https://www.sbfisica.org.br/](https://www.sbfisica.org.br/)*

<br>

## ***Equação linear em forma matricial***

Toda equação linear pode ser escrita em forma de matriz, e isso
facilita muito o desenvolvimento de códigos computacionais.

Para uma matriz $X$ quadrada e invertível:  

$$\boxed{X\vec{\beta} = \vec{y}}$$ 

$$\downarrow$$

$$\boxed{\vec{\beta} = X^{-1} \vec{y}}$$

Exemplo:

Dado um Conjunto de dados (Observações) com 3 variáveis independente ($x1$, $x2$ e $x3$) e uma variável dependentes $(y):$

$$
\begin{cases}
2x_1 + x_2 - x_3 = 8 \\  
3x_1 - x_2 + 2x_3 = 11 \\  
-x_1 + 2x_2 + x_3 = 3
\end{cases}
\quad\longrightarrow\quad
\underbrace{\begin{bmatrix}
2 & 1 & -1 \\
3 & -1 & 2 \\
-1 & 2 & 1
\end{bmatrix}}_{\text{Coeficientes}}
\underbrace{
\begin{bmatrix}
x_1 \\ 
x_2 \\ 
x_3
\end{bmatrix}}_{\text{Incógnitas}}=
\underbrace{
\begin{bmatrix}
8 \\ 
11 \\ 
3
\end{bmatrix}
}_{\text{Constantes}}
$$

<br>

## ***Solução Matricial por Mínimos Quadrados***

Quando lidamos com um sistema linear sobredeterminado $X\vec{\beta} \approx \vec{y}$ (com mais equações do que incógnitas), em geral não existe uma solução exata em que a diferença seja nula. Nesses casos, o objetivo é encontrar o vetor de incógnitas $\vec{\beta}$ que minimiza a norma do vetor de resíduos $\vec{e}.$

<br>

## ***Formulação do Erro Residual***

A relação entre os valores estimados e observados é dada por:

$$\boxed{X\vec{\beta} - \vec{y} = \vec{e}}$$

Sendo:  
&nbsp;&nbsp;&nbsp;&nbsp;
$\vec y\ \longrightarrow\ \text{valor observado}$  
&nbsp;&nbsp;&nbsp;
$X\vec\beta\ \longrightarrow\ \text{valor estimado}$  
&nbsp;&nbsp;&nbsp;
$\vec e=X\vec\beta-\vec y\ \longrightarrow\ \text{resíduo}$

Se o sistema tiver solução exata, então $\vec{e} = \mathbf{0}$. Caso contrário, para obter a solução aproximada de menor erro, minimiza-se a soma dos quadrados dos erros $E^2$:

$$
\boxed{
E^2 = (X\vec{\beta} - \vec{y})^T (X\vec{\beta} - \vec{y})
}
$$

Expansão da expressão matricial utilizando as propriedades da transposta $(X\vec{\beta})^T = \beta^T X^T$:

$$\boxed{E^2 = (\beta^T X^T - y^T)(X\vec{\beta} - \vec{y})}$$

$$\downarrow$$

$$\boxed{E^2 = \beta^T X^T X \vec{\beta} - 2\beta^T X^T \vec{y} + y^T\vec{y}}$$

(Nota: o termo $-2\beta^T X^T y$ surge pois $\beta^T X^T \vec{y}$ é um escalar, sendo igual à sua transposta $y^T X \vec{\beta}$).

<br>

## ***Minimização e Obtenção da Equação Normal***

O valor mínimo de $E^2$ ocorre no ponto em que a derivada em relação ao vetor de incógnitas $\vec{\beta}$ é igual a zero:

$$\boxed{\frac{dE^2}{d\vec{\beta}} = 2 X^T X \vec{\beta} - 2 X^T \vec{y} = \mathbf{0}}$$
$$\downarrow$$
$$\boxed{2 X^T X \vec{\beta} = 2 X^T \vec{y}}$$

Isolando o vetor $\vec{\beta}$ através da multiplicação pela matriz inversa $(X^T X)^{-1}$ (desde que $X^TX$ seja invertível), chega-se à **Estimativa dos Mínimos Quadrados**:

$$\boxed{\vec{\beta} = (X^T X)^{-1} X^T \vec{y}}$$

Essa abordagem puramente algébrica permite obter a solução de mínimos quadrados para o sistema sobredeterminado diretamente em formato matricial, servindo de base computacional antes de introduzirmos modelos probabilísticos e estatísticos.

<br>

## ***Aplicação, Avaliação e Evolução do Modelo***

Dado o seguinte conjunto de dados, em que $x_1$ e $x_2$ representam as variáveis explicativas e $y$ representa a variável resposta:

<br>
<div align=center>

**Conjunto de dados (Observações)**

|       | <div align="center" style="width: 150px;">$x1$</div> | <div align="center" style="width: 150px;">$x2$</div> | <div align="center" style="width: 150px;">$y$</div> |
| :---: | :--------------------------------------------------: | :--------------------------------------------------: | :-------------------------------------------------: |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;120&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8.1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|   1   |13|90|6.8|
|   2   |20|120|7.0|
|   3   |28|60|7.4|
|   4   |20|150|9.3|
|   5   |24|150|7.5|
|   6   |18|60|7.6|
|   7   |8 |120|8.0|
|   8   |2 |240|7.0|
|   9   |12|90|7.3|
|  10   |15|90|8.6|
|  11   |9 |120|8.3|
|  12   |6 |180|7.9|
|  13   |4 |90|6.4|
|  14   |8 |150|7.8|
|  15   |12|120|9.4|
|  16   |10|180|8.8|
|  17   |3 |90|6.9|
|  18   |15|180|7.7|
|  19   |9 |90|8.2|
|  20   |24|120|8.6|
|  21   |5 |150|8.1|
|  22   |7 |120|7.2|
|  23   |12|180|8.5|
|  24   |2 |90|6.1|

</div>
<br>

Nesse caso, temos 25 observações e duas variáveis explicativas. Portanto, o sistema possui 25 equações, 2 incógnitas ($\beta_1$ e $\beta_2$) e um vetor de constantes $\vec{y}_{25X1}$:

Representação matricial pela Origem (sem intercepto):

$$
\begin{bmatrix}
5 & 120\\
13 & 90\\
20 & 120\\
\vdots & \vdots\\
2 & 90
\end{bmatrix}
\begin{bmatrix}
\beta_1\\
\beta_2
\end{bmatrix}
\approx
\begin{bmatrix}
8.1\\
6.8\\
7.0\\
\vdots\\
6.1
\end{bmatrix}
$$

<br>

Ou, de forma explícita:

$$
\boxed{
X_{25\times2}\,
\vec{\beta}_{2\times1}
\approx
\vec y_{25\times1}
}
$$
  
<br>

Em que:

* o produto $X\vec{\beta}$ resulta em um vetor $25\times1$.
* $X$ é uma matriz $25\times2$;
* $\vec{\beta}$ é um vetor $2\times1$, contendo as duas incógnitas;
* $\vec y$ é um vetor $25\times1$, contendo as 25 constantes/valores observados;
  
<br>

Como temos mais equações do que incógnitas, não buscamos uma solução exata para cada equação. Utilizamos o **Método dos Mínimos Quadrados** para encontrar os valores de $\beta_1$ e $\beta_2$ que produzem o melhor ajuste aos dados.

Para isso, aplicamos a solução matricial:

$$\boxed{ \vec{\beta}=(X^TX)^{-1}X^T\vec{y} }$$
  
<br>

### Transposição da matriz $X$

Primeiramente, calculamos a transposta de $X$, que transforma suas linhas em colunas:

$$X^T= \begin{bmatrix} 
5 & 13 & 20 & 28 & \cdots & 2\\ 
120 & 90 & 120 & 60 & \cdots & 90 
\end{bmatrix}$$
  
<br>

### Cálculo de $X^TX$

A multiplicação de $X^T$ por $X$ resulta em uma matriz $2\times2$:

$$
X^TX=\begin{bmatrix} 
5 & 13 & 20 & 28 & \cdots & 2\\ 
120 & 90 & 120 & 60 & \cdots & 90 
\end{bmatrix}
\begin{bmatrix}
5 & 120 \\
13 & 90\\
20 & 120\\
\vdots & \vdots\\
2 & 90
\end{bmatrix}
$$

$$\downarrow$$

$$X^TX= \begin{bmatrix} 
\sum x_0^2 & \sum x_0x_1\\ 
\sum x_1x_0 & \sum x_1^2 
\end{bmatrix}$$ 

$$\downarrow$$

$$
\boxed{
\begin{aligned}
\sum x_0^2
&=5^2+13^2+20^2+\cdots+2^2\\
\sum x_0x_1
&=(5)(120)+(13)(90)+(20)(120)+\cdots+(2)(90)\\
\sum x_1x_0
&=(120)(5)+(90)(13)+(120)(20)+\cdots+(90)(2)\\
\sum x_1^2
&=120^2+90^2+120^2+\cdots+90^2
\end{aligned}}
$$

$$\downarrow$$

$$X^TX= \begin{bmatrix} 
4669 & 34950\\ 
34950 & 441900 
\end{bmatrix}$$












## ***Bloco de Código***

<details>
  <summary>Python</summary>
  <p>
     
    ...
  </p>
</details>
<details>
  <summary>VBA</summary>
  <p>
     
    ...
  </p>
</details>
<details>
  <summary>Rust</summary>
  <p>
     
    ...
  </p>
</details>
