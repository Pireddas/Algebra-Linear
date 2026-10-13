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

$$E^2 = (\beta^T X^T X\vec{\beta}) - (\beta^T X^T \vec{y}) - (y^T X\vec{\beta}) + (y^T \vec{y})$$

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

## ***Aplicação Prática***

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

## ***Transposição da matriz*** $X$

Primeiramente, calculamos a transposta de $X$, que transforma suas linhas em colunas:

$$X^T= \begin{bmatrix} 
5 & 13 & 20 & 28 & \cdots & 2\\ 
120 & 90 & 120 & 60 & \cdots & 90 
\end{bmatrix}$$
  
<br>

## ***Cálculo de*** $X^TX$

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

<br>

## ***Cálculo de*** $X^T\vec{y}$

De forma semelhante, calculamos o produto entre $X^T$ e o vetor de valores observados $\vec{y}$:

$$
X^T\vec{y}=\begin{bmatrix} 
5 & 13 & 20 & 28 & \cdots & 2\\ 
120 & 90 & 120 & 60 & \cdots & 90 
\end{bmatrix}
\begin{bmatrix}
8.1\\
6.8\\
7.0\\
\vdots\\
6.1
\end{bmatrix}
$$

$$\downarrow$$

$$X^T\vec{y}=\begin{bmatrix} 
\sum x_0y\\ 
\sum x_1y 
\end{bmatrix}$$

$$\downarrow$$

$$
\boxed{
\begin{aligned}
\sum x_0y
&=(5)(8.1)+(13)(6.8)+(20)(7.0)+\cdots+(2)(6.1)\\
\sum x_1y
&=(120)(8.1)+(90)(6.8)+(120)(7.0)+\cdots+(90)(6.1)
\end{aligned}}
$$

$$\downarrow$$

$$X^T\vec{y}=\begin{bmatrix} 
2305.9\\ 
24726 
\end{bmatrix}$$
  
<br>

Dessa forma, a expressão

$$(X^TX)^{-1}X^T\vec{y}$$
  
<br>

pode ser escrita, neste caso, como:

$$\vec{\beta}=\begin{bmatrix} 
4669 & 34950\\ 
34950 & 441900 
\end{bmatrix}^{-1} 
\begin{bmatrix} 
2305.9\\ 
24726 
\end{bmatrix}$$
  
<br>

## ***Cálculo da matriz inversa*** $(X^TX)^{-1}$

Para uma matriz $2\times2$ da forma

$$
A=\begin{bmatrix}
a & b\\
c & d
\end{bmatrix},
$$
  
<br>

Desde que $ad-bc\neq0$, sua inversa é dada por:

$$
A^{-1}=\frac{1}{ad-bc}
\begin{bmatrix}
d & -b\\
-c & a
\end{bmatrix},
$$

<br>
Sabendo que:

* $a = 4669$;
* $b = 34950$;
* $c = 34950$;
* $d = 441900$.
  
O determinante de $X^TX$ é:

$$
(X^TX)^{-1}=\frac{1}{\det(X^TX)}
\begin{bmatrix}
441900 & -34950\\
-34950 & 4669
\end{bmatrix},
$$

$$\downarrow$$

$$
\det(X^TX)=(4669 \times 441900)-(-34950)^2=841.728.600
$$
  
$$\downarrow$$

$$
(X^TX)^{-1}=\frac{1}{841.728.600}
\begin{bmatrix}
441900 & -34950\\
-34950 & 4669
\end{bmatrix}
\approx
\begin{bmatrix}
0.0005250 & -0.00004152\\
-0.00004152 & 0.000005546
\end{bmatrix}
$$

<br>

## ***Obtenção de*** $\beta_1$ ***e*** $\beta_2$

Finalmente, realizamos a multiplicação de $(X^TX)^{-1}$ por $X^T\vec{y}$:

$$
\vec{\beta}=(X^TX)^{-1}X^T\vec{y}
$$

$$
\vec{\beta}=\begin{bmatrix}
0.0005250 & -0.00004152\\
-0.00004152 & 0.000005546
\end{bmatrix}
\begin{bmatrix}
2305.9\\
24726
\end{bmatrix}
$$
  
$$\downarrow$$

$$
\vec{\beta}\approx\begin{bmatrix}
0.1839\\
0.0414
\end{bmatrix}
$$
  
<br>

Portanto, os coeficientes estimados pelo Método dos Mínimos Quadrados são:

$$\boxed{\beta_1\approx0.1839}$$

$$\boxed{\beta_2\approx0.0414}$$
  
<br>

Assim, para a Matriz de Observações $X$, a equação estimada pelo modelo é:

$$
X=\begin{bmatrix}
5 & 120\\
13 & 90\\
20 & 120\\
\vdots & \vdots\\
2 & 90
\end{bmatrix}
$$

$$\boxed{\hat y_i=0.1839x_{i0}+0.0414x_{i1}}$$

<br>

Esse procedimento mostra como a solução matricial transforma o conjunto de dados em dois coeficientes que definem o modelo de regressão.

<br>

## ***Resultado***  

<div align=center>

|       | <div align="center" style="width: 90px;">$x1$</div> | <div align="center" style="width: 90px;">$x2$</div> | <div align="center" style="width: 90px;">$y$</div> | <div align="center" style="width: 90px;">Previsão ($\hat y$)</div> | <div align="center" style="width: 180px;">Resíduo ($y - \hat y$)</div> | <div align="center" style="width: 95px;">Erro Absoluto</div> |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 5&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;120&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8.1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5.888545&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.21145525&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.211455&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|   1   |13|90|6.8|6.117589 |0.68241071|0.682411|
|   2   |20|120|7.0|8.647216 |-1.6472162|1.647216|
|   3   |28|60|7.4|7.634014 |-0.23401384|0.234014|
|   4   |20|150|9.3|9.889463 |-0.5894631|0.589463|
|   5   |24|150|7.5|10.625109|-3.12510882|3.125109|
|   6   |18|60|7.6|5.794900 |1.80510046|1.805100|
|   7   |8 |120|8.0|6.440279 |1.55972096|1.559721|
|   8   |2 |240|7.0|10.305798|-3.30579806|3.305798|
|   9   |12|90|7.3|5.933678 |1.36632214|1.366322|
|  10   |15|90|8.6|6.485412 |2.11458785|2.114588|
|  11   |9 |120|8.3|6.624190 |1.67580953|1.675810|
|  12   |6 |180|7.9|8.556950 |-0.65694998|0.656950|
|  13   |4 |90|6.4|4.462386 |1.93761358|1.937614|
|  14   |8 |150|7.8|7.682526 |0.11747406|0.117474|
|  15   |12|120|9.4|7.175925 |2.22407524|2.224075|
|  16   |10|180|8.8|9.292596 |-0.4925957|0.492596|
|  17   |3 |90|6.9|4.278475 |2.62152501|2.621525|
|  18   |15|180|7.7|10.212153|-2.51215285|2.512153|
|  19   |9 |90|8.2|5.381944 |2.81805643|2.818056|
|  20   |24|120|8.6|9.382862 |-0.78286192|0.782862|
|  21   |5 |150|8.1|7.130792 |0.96920835|0.969208|
|  22   |7 |120|7.2|6.256368 |0.94363239|0.943632|
|  23   |12|180|8.5|9.660419 |-1.16041856|1.160419|
|  24   |2 |90|6.1|4.094564 |2.00543644|2.005436|

<br>

Erro médio absoluto (MAE): **1.58236029**

</div>

---

<div>

### ***Representação Gráfica*** 

<div style="display: flex; gap: 10px;">

<img width="450" height="300" alt="image" src="https://github.com/user-attachments/assets/f5c15f09-405c-45fc-82c8-f5531785f8f1" />
<img width="450" height="300" alt="image" src="https://github.com/user-attachments/assets/b95b0032-9df8-45f9-94ad-05986fa95dce" />
 
*Photo by [Ralf Piredda](https://www.sbfisica.org.br/)*

</div>

<br>

## ***Conclusão***

Embora tenhamos obtido uma solução matemática para o sistema, o modelo $\hat{y} = 0.1839x_0 + 0.0414x_1$ apresenta uma limitação.

Num cenário em que as variáveis explicativas apresentem valor zero ($x_0 = 0$ e $x_1 = 0$), o modelo prevê um **valor zero** para a previsão.

$$\hat{y}=0.1839(0) + 0.0414(0)=0$$

Para corrigir esse viés e refletir a realidade, o próximo passo é evoluir o modelo para uma **Regressão Linear** com um termo constante independente $\beta_0$ - **intercepto**.

A nova equação estimada assume a seguinte forma:

$$\hat{y}=\beta_0 x_0+\beta_1 x_1+\beta_2 x_2$$

Ao introduzirmos o termo $\beta_0$, garantimos que, quando todas as variáveis explicativas forem nulas ($x_1=0$ e $x_2=0$), o resultado estimado não seja forçado a zero, mas sim ao valor da constante $\beta_0$:

$$\hat{y}=\beta_0(1)+\beta_1(0)+\beta_2(0)=\beta_0$$

Esse coeficiente $\beta_0$ atua como um "piso" ou "nota base" do modelo.

<br>

Além da ausência do intercepto ($\beta_0$), o modelo puramente determinístico ($\hat{y} = \beta_1x_0 + \beta_2x_1$) não leva em consideração as oscilações aleatórias inerentes aos dados reais. Na prática, a variável resposta $y$ é influenciada por fatores não observados, erros de medição e variações estocásticas.

Para proteger o sistema dos riscos ligados a essa exposição, a **Regressão Linear Múltipla** introduz duas modificações fundamentais:
1. A inclusão de uma coluna de uns ($1s$) na Matriz de Projeto $X$, permitindo estimar o termo constante $\beta_0$;

$$X_{25\times3}= \begin{bmatrix} 
1 & 5 & 120 \\ 
1 & 13 & 90 \\ 
1 & 20 & 120 \\ 
\vdots & \vdots & \vdots \\ 
1 & 2 & 90 
\end{bmatrix}, 
\quad\vec{\beta}_{3\times1}= \begin{bmatrix}
\beta_0 \\ 
\beta_1 \\ 
\beta_2 
\end{bmatrix}$$

2. A formalização do erro estocástico $\epsilon$, assumindo premissas estatísticas (como média zero, homocedasticidade e ausência de autocorrelação) que viabilizam a inferência estatística e testes de hipóteses.

<br>

Assim, a equação pode expressar o valor real em função da estimativa mais o resíduo:

$$\boxed{y=\underbrace{\beta_0 x_0+\beta_1 x_1+\beta_2 x_2}_{\text{Componente Determinístico}}+\cdots+\beta_n x_n+\underbrace{\epsilon}_{\text{Erro Estocástico}}}$$

<br>

## ***Regressão Linear Múltipla com Intercepto*** ($\beta_0$) 

Dado o seguinte conjunto de dados, em que adicionamos a coluna de uns $x_0$ para cálculo do intercepto:


<div align="center">  

**Conjunto de dados (Observações)**

|       | <div align="center" style="width: 100px;">$x0$</div> | <div align="center" style="width: 100px;">$x1$</div> | <div align="center" style="width: 100px;">$x2$</div> | <div align="center" style="width: 100px;">$y$</div> |
| :---: | :---: | :---: | :---: | :---: |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 0 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;120&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8.1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|   1   |1|13|90|6.8|
|   2   |1|20|120|7.0|
|   3   |1|28|60|7.4|
|   4   |1|20|150|9.3|
|   5   |1|24|150|7.5|
|   6   |1|18|60|7.6|
|   7   |1|8 |120|8.0|
|   8   |1|2 |240|7.0|
|   9   |1|12|90|7.3|
|  10   |1|15|90|8.6|
|  11   |1|9 |120|8.3|
|  12   |1|6 |180|7.9|
|  13   |1|4 |90|6.4|
|  14   |1|8 |150|7.8|
|  15   |1|12|120|9.4|
|  16   |1|10|180|8.8|
|  17   |1|3 |90|6.9|
|  18   |1|15|180|7.7|
|  19   |1|9 |90|8.2|
|  20   |1|24|120|8.6|
|  21   |1|5 |150|8.1|
|  22   |1|7 |120|7.2|
|  23   |1|12|180|8.5|
|  24   |1|2 |90|6.1|

</div>
<br>

Nesse caso, temos 25 observações e três variáveis explicativas  (incluindo o termo constante). Portanto, o sistema possui 25 equações, 3 incógnitas ($\beta_0$, $\beta_1$ e $\beta_2$) e um vetor de constantes $\vec{y}_{25\times1}$:

Representação matricial com intercepto:

$$
\begin{bmatrix}
1 & 5 & 120\\
1 & 13 & 90\\
1 & 20 & 120\\
\vdots & \vdots & \vdots\\
1 & 2 & 90
\end{bmatrix}
\begin{bmatrix}
\beta_0\\
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

Ou de forma explícita:

$$
\boxed{
X_{25\times3}\,
\vec{\beta}_{3\times1}\approx\vec{y}_{25\times1}
}
$$
  
<br>

Em que:
* $X$ é uma matriz $25\times3$;
* $\vec{\beta}$ é um vetor $3\times1$, contendo as três incógnitas;
* $\vec{y}$ é um vetor $25\times1$, contendo os 25 valores observados;
* O produto $X\vec{\beta}$ resulta em um vetor $25\times1$.
  
<br>

Utilizamos o **Método dos Mínimos Quadrados Ordinários (MQO)** para encontrar o vetor de estimadores $\vec{\hat{\beta}}$ aplicando a solução matricial:

$$\boxed{\vec{\beta}=(X^TX)^{-1}X^T\vec{y}}$$

<br>

## ***Transposição da matriz*** $X$

Primeiramente, calculamos a transposta de $X$, que transforma suas linhas em colunas:

$$X^T= \begin{bmatrix} 
1 & 1 & 1 & 1 & \cdots & 1\\
5 & 13 & 20 & 28 & \cdots & 2\\ 
120 & 90 & 120 & 60 & \cdots & 90 
\end{bmatrix}$$

<br>

## ***Cálculo de*** $X^TX$

A multiplicação de $X^T$ por $X$ resulta em uma matriz quadrada $3\times3$:

$$
X^TX=\begin{bmatrix} 
1 & 1 & 1 & 1 & \cdots & 1\\
5 & 13 & 20 & 28 & \cdots & 2\\ 
120 & 90 & 120 & 60 & \cdots & 90 
\end{bmatrix}
\begin{bmatrix}
1 & 5 & 120\\
1 & 13 & 90\\
1 & 20 & 120\\
\vdots & \vdots & \vdots\\
1 & 2 & 90
\end{bmatrix}
$$

$$\downarrow$$

$$X^TX= \begin{bmatrix} 
\sum x_0^2 & \sum x_0x_1 & \sum x_0x_2\\ 
\sum x_1x_0 & \sum x_1^2 & \sum x_1x_2\\
\sum x_2x_0 & \sum x_2x_1 & \sum x_2^2
\end{bmatrix}$$ 

$$\downarrow$$

$$
\boxed{
\begin{aligned}
&\sum x_0^2=1^2+1^2+1^2+\cdots+1^2=25\\
&\sum x_0x_1=(1)(5)+(1)(13)+(1)(20)+\cdots+(1)(2)=291\\
&\sum x_0x_2=(1)(120)+(1)(90)+(1)(120)+\cdots+(1)(90)=3150\\
&\space\\
&\space\\
&\space\\
&\sum x_1x_0=(5)(1)+(13)(1)+(20)(1)+\cdots+(2)(1)=291\\
&\sum x_1^2=5^2+13^2+20^2+\cdots+2^2=4669\\
&\sum x_1x_2=(5)(120)+(13)(90)+(20)(120)+\cdots+(2)(90)=34950\\
&\space\\
&\space\\
&\space\\
&\sum x_2x_0=(120)(1)+(90)(1)+(120)(1)+\cdots+(90)(1)=3150\\
&\sum x_2x_1=(120)(5)+(90)(13)+(120)(20)+\cdots+(90)(2)=34950\\
&\sum x_2^2=120^2+90^2+120^2+\cdots+90^2=441900
\end{aligned}
}
$$

$$\downarrow$$

$$X^TX= \begin{bmatrix} 
25 & 291 & 3150\\ 
291 & 4669 & 34950\\ 
3150 & 34950 & 441900 
\end{bmatrix}$$

<br>

## ***Cálculo de*** $X^T\vec{y}$

De forma semelhante, calculamos o produto entre $X^T$ e o vetor de valores observados $\vec{y}$:

$$
X^T\vec{y}=\begin{bmatrix} 
1 & 1 & 1 & 1 & \cdots & 1\\ 
5 & 13 & 20 & 28 & \cdots & 2\\ 
120 & 90 & 120 & 60 & \cdots & 90 
\end{bmatrix}
\begin{bmatrix}
8.1\\
6.8\\
7.0\\
\vdots\\
6.1
\end{bmatrix}
$$

$$\downarrow$$

$$X^T\vec{y}=\begin{bmatrix} 
\sum x_0y\\ 
\sum x_1y\\ 
\sum x_2y
\end{bmatrix}$$

$$\downarrow$$

$$
\boxed{
\begin{aligned}
&\sum x_0y=(1)(8.1)+(1)(6.8)+(1)(7.0)+\cdots+(1)(6.1)=194.5\\
&\sum x_1y=(5)(8.1)+(13)(6.8)+(20)(7.0)+\cdots+(2)(6.1)=2305.9\\
&\sum x_2y=(120)(8.1)+(90)(6.8)+(120)(7.0)+\cdots+(90)(6.1)=24726
\end{aligned}}
$$

$$\downarrow$$

$$X^T\vec{y}=\begin{bmatrix} 
194.5\\
2305.9\\ 
24726 
\end{bmatrix}$$
  
<br>

O sistema normal de equações assume a seguinte forma:

$$\vec{\hat{\beta}}=(X^TX)^{-1}X^T\vec{y}$$
  
$$\downarrow$$

$$\vec{\hat{\beta}}=\begin{bmatrix} 
25 & 291 & 3150\\ 
291 & 4669 & 34950\\ 
3150 & 34950 & 441900  
\end{bmatrix}^{-1} 
\begin{bmatrix} 
194.5\\
2305.9\\ 
24726 
\end{bmatrix}$$

<br>

## ***Cálculo da Matriz Inversa*** $(X^TX)^{-1}$

Para inverter uma matriz $3\times3$ de forma: 

$$
A=\begin{bmatrix}
a & b & c\\
d & e & f\\
g & h & i
\end{bmatrix},
$$

utilizamos a fórmula:

$$A^{-1}=\frac{1}{\det(A)} \text{adj}(A)$$

com o padrão de sinais dos cofatores dado por:

$$
\begin{pmatrix} 
\text{+} & \text{-} & \text{+} \\
\text{-} & \text{+} & \text{-} \\
\text{+} & \text{-} & \text{+} 
\end{pmatrix}
$$

<br>

Identificando os elementos de $X^TX$:
* $a = 25, \quad b = 291, \quad c = 3150$
* $d = 291, \quad e = 4669, \quad f = 34950$
* $g = 3150, \quad h = 34950, \quad i = 441900$

<br>

Matriz de Cofatores ($C_{ij}$) e Matriz Adjunta $\text{adj}(X^TX)$:

Em que:

$$
X^T X=\begin{bmatrix} 
25 & 291 & 3150\\ 
291 & 4669 & 34950\\ 
3150 & 34950 & 441900  
\end{bmatrix}
\longrightarrow\ 
\begin{pmatrix} 
\text{+} & \text{-} & \text{+} \\
\text{-} & \text{+} & \text{-} \\
\text{+} & \text{-} & \text{+}
\end{pmatrix}
$$

Para acharmos a primeira linha ($C_{00}$, $C_{01}$ e $C_{02}$) da Matriz de Cofatores ($C_{ij}$), eliminamos a 1ª coluna de $X^T X$ e as linhas conforme abaixo:

<br>

Eliminamos a 1ª linha de $X^T X$  

$$\begin{bmatrix} 
\emptyset & \emptyset & \emptyset \\
\emptyset & 4669 & 34950\\
\emptyset & 34950 & 441900  
\end{bmatrix}$$
$$\downarrow$$
$$\boxed{C_{00}: + (4669 \cdot 441900 - 34950 \cdot 34950) = 2063231.100 - 1221502500 = 841728600}$$

<br>

Eliminamos a 2ª linha de $X^T X$  

$$\begin{bmatrix} 
\emptyset & 291 & 3150 \\
\emptyset & \emptyset & \emptyset\\
\emptyset & 34950 & 441900  
\end{bmatrix}$$
$$\downarrow$$
$$\boxed{C_{01}: - (291 \cdot 441900 - 34950 \cdot 3150) = - (128592900 - 110092500) = -18500400}$$

<br>

Eliminamos a 3ª linha de $X^T X$   

$$\begin{bmatrix} 
\emptyset & 291 & 3150 \\
\emptyset & 4669 & 34950\\
\emptyset & \emptyset & \emptyset  
\end{bmatrix}$$
$$\downarrow$$
$$\boxed{C_{02}: + (291 \cdot 34950 - 4669 \cdot 3150) = 10170450 - 14707350 = -4536900}$$

<br>

Em seguida, para acharmos a segunda linha ($C_{10}$, $C_{11}$ e $C_{12}$) da Matriz de Cofatores ($C_{ij}$), eliminamos a 2ª coluna de $X^T X$ e as linhas conforme abaixo:

<br>

Eliminamos a 1ª linha de $X^T X$  

$$\begin{bmatrix} 
\emptyset & \emptyset & \emptyset\\ 
291 & \emptyset & 34950\\ 
3150 & \emptyset & 441900   
\end{bmatrix}$$
$$\downarrow$$
$$\boxed{C_{10}: - (291 \cdot 441900 - 3150 \cdot 34950) = 128592900 - 110092500 = -18500400}$$  

<br>

Eliminamos a 2ª linha de $X^T X$ 

$$\begin{bmatrix} 
25 & \emptyset & 3150\\ 
\emptyset & \emptyset & \emptyset\\ 
3150 & \emptyset & 441900  
\end{bmatrix}$$
$$\downarrow$$
$$\boxed{C_{11}: + (25 \cdot 441900 - 3150 \cdot 3150) = 11047500 - 9922500 = 1125000}$$  

<br>

Eliminamos a 3ª linha de $X^T X$  

$$\begin{bmatrix} 
25 & \emptyset & 3150\\ 
291 & \emptyset & 34950\\ 
\emptyset & \emptyset & \emptyset  
\end{bmatrix}$$
$$\downarrow$$
$$\boxed{C_{12}: - (25 \cdot 34950 - 291 \cdot 3150) = - (873750 - 916650) = 42900}$$

<br>

Finalmente, para acharmos a terceira linha ($C_{20}$, $C_{21}$ e $C_{22}$) da Matriz de Cofatores ($C_{ij}$), eliminamos 3ª coluna de $X^T X$ e as linhas conforme abaixo:

<br>

Eliminamos 1ª linha de $X^T X$  

$$\begin{bmatrix} 
\emptyset & \emptyset & \emptyset\\ 
291 & 4669 & \emptyset\\ 
3150 & 34950 & \emptyset   
\end{bmatrix}$$
$$\downarrow$$
$$\boxed{C_{20}: + (291 \cdot 34950 - 3150 \cdot 4669) = 10170450 - 14707350 = -4536900}$$

<br>

Eliminamos 2ª linha de $X^T X$  

$$\begin{bmatrix} 
25 & 291 & \emptyset\\ 
\emptyset & \emptyset & \emptyset\\ 
3150 & 34950 & \emptyset  
\end{bmatrix}$$

$$\boxed{C_{21}: - (25 \cdot 34950 - 3150 \cdot 291) = - (873750 - 916650) = 42900}$$

<br>

Eliminamos 3ª linha de $X^T X$  

$$
\begin{bmatrix}
25 & 291 & \emptyset \\
291 & 4669 & \emptyset \\
\emptyset & \emptyset & \emptyset
\end{bmatrix}
$$
$$\downarrow$$
$$\boxed{C_{22}: + (25 \cdot 4669 - 291 \cdot 291) = 116725 - 84681 = 32044}$$

<br>

Sendo $X^TX$ uma matriz simétrica, a Matriz de Cofatores é igual à sua transposta ($C = C^T$), logo:

$$\text{adj}(X^TX)=\begin{bmatrix} 
841728600 & -18500400 & -4536900 \\ 
-18500400 & 1125000 & 42900 \\ 
-4536900 & 42900 & 32044 
\end{bmatrix}$$

Cálculo do Determinante $\det(X^TX)$:

Sendo:

$$X^T X=\begin{bmatrix} 
25 & 291 & 3150\\ 
291 & 4669 & 34950\\ 
3150 & 34950 & 441900  
\end{bmatrix}
\longrightarrow
\begin{bmatrix}
a & b & c\\
d & e & f\\
g & h & i
\end{bmatrix}$$

Pela Regra de Sarrus:

$$det(X^T X)=(aei+bfg+cdh)−(ceg+bdi+afh)$$

<br>

Então:

$$
\boxed{
\begin{aligned}
&v_1 = aei+bfg+cdh\\
&aei = (25 \times 4669 \times 441900)=51580777500\\
&bfg = (291 \times 34950 \times 3150)=32036917500\\
&cdh = (3150 \times 291 \times 34950)=32036917500\\
&v_1 = 115654612500
\end{aligned}}
$$

$$
\boxed{
\begin{aligned}
&v_2 = ceg+bdi+afh\\
&ceg = (3150 \times 4669 \times 3150)=46328152500\\
&bdi = (291 \times 291 \times 441900)=37420533900\\
&afh = (25\times 34950 \times 34950)=30537562500\\
&v_2 = 114286248900
\end{aligned}}
$$

$$
\boxed{
\begin{aligned}
det(X^T X) &= v_1-v_2\\
det(X^T X) &= 115654612500-114286248900\\
det(X^T X) &= 1368363600
\end{aligned}}
$$

Obtenção da Inversa $(X^TX)^{-1}$:

$$
(X^TX)^{-1}=\frac{1}{\det(X^TX)}
\text{adj}(X^TX)
$$
$$\downarrow$$
$$
(X^TX)^{-1}=\frac{1}{1368363600}
\begin{bmatrix}
841728600 & -18500400 & -4536900 \\ 
-18500400 & 1125000 & 42900 \\ 
-4536900 & 42900 & 32044
\end{bmatrix}
$$
$$\downarrow$$
$$
(X^TX)^{-1}\approx\begin{bmatrix}
 0.615135188 &	-0.013520091 &	-0.003315566 \\
-0.013520091 &	 0.000822150 &	 0.000031351 \\
-0.003315566 &	 0.000031351 &	 0.000023418 
\end{bmatrix}
$$

<br>

Obtenção de $\beta_0$, $\beta_1$ e $\beta_2$

Finalmente, realizando a multiplicação matricial $(X^TX)^{-1} \cdot (X^T\vec{y})$:

$$
\vec{\hat{\beta}}=\begin{bmatrix}
 0.615135188 &	-0.013520091 &	-0.003315566 \\
-0.013520091 &	 0.000822150 &	 0.000031351 \\
-0.003315566 &	 0.000031351 &	 0.000023418 
\end{bmatrix}
\begin{bmatrix}
194.5\\
2305.9\\ 
24726 
\end{bmatrix}
$$

$$\downarrow$$

$$
\vec{\beta}\approx\begin{bmatrix}
 6.48712881576214 \\
 0.04133046216663 \\
 0.00644273495729 
\end{bmatrix}
$$
  
<br>

Portanto, os coeficientes estimados pelo Método dos Mínimos Quadrados são:

$$\boxed{\beta_0\approx 6.48712881576214}$$
$$\boxed{\beta_1\approx 0.04133046216663}$$
$$\boxed{\beta_2\approx 0.00644273495729}$$
  
<br>

Assim, para a Matriz de Observações $X$, a equação estimada pelo modelo é:

$$
X=\begin{bmatrix}
1 & 5 & 120\\
1 & 13 & 90\\
1 & 20 & 120\\
\vdots & \vdots & \vdots\\
1 & 2 & 90
\end{bmatrix}
$$

$$\boxed{ \hat y_i=6.4871x_{i0} + 0.04133x_{i1}+0.006442x_{i2} }$$

<br>

Esse procedimento mostra como a solução matricial transforma o conjunto de dados em dois coeficientes que definem o modelo de regressão.

<br>

## ***Resultado***  

<div align=center>
   
|       | <div align="center" style="width: 60px;">$x0$</div> | <div align="center" style="width: 60px;">$x1$</div> | <div align="center" style="width: 60px;">$x2$</div> | <div align="center" style="width: 60px;">$y$</div> | <div align="center" style="width: 85px;">Previsão ($\hat y$)</div> | <div align="center" style="width: 130px;">Resíduo ($y - \hat y$)</div> | <div align="center" style="width: 95px;">Erro Absoluto</div> |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;120&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8.1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;7.466909&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0.633090679&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0.633091&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|   1   | 1 |13|90|6.8|7.604271|-0.80427097|0.804271|
|   2   | 1 |20|120|7.0|8.086866|-1.086866254|1.086866|
|   3   | 1 |28|60|7.4|8.030946|-0.630945854|0.630946|
|   4   | 1 |20|150|9.3|8.280148|1.019851697|1.019852|
|   5   | 1 |24|150|7.5|8.445470|-0.945470151|0.945470|
|   6   | 1 |18|60|7.6|7.617641|-0.017641232|0.017641|
|   7   | 1 |8 |120|8.0|7.590901|0.409099292|0.409099|
|   8   | 1 |2 |240|7.0|8.116046|-1.11604613|1.116046|
|   9   | 1 |12|90|7.3|7.562941|-0.262940508|0.262941|
|  10   | 1 |15|90|8.6|7.686932|0.913068106|0.913068|
|  11   | 1 |9 |120|8.3|7.632231|0.66776883|0.667769|
|  12   | 1 |6 |180|7.9|7.894804|0.005196119|0.005196|
|  13   | 1 |4 |90|6.4|7.232297|-0.832296811|0.832297|
|  14   | 1 |8 |150|7.8|7.784183|0.015817243|0.015817|
|  15   | 1 |12|120|9.4|7.756223|1.643777443|1.643777|
|  16   | 1 |10|180|8.8|8.060126|0.73987427|0.739874|
|  17   | 1 |3 |90|6.9|7.190966|-0.290966348|0.290966|
|  18   | 1 |15|180|7.7|8.266778|-0.566778041|0.566778|
|  19   | 1 |9 |90|8.2|7.438949|0.761050879|0.761051|
|  20   | 1 |24|120|8.6|8.252188|0.347811897|0.347812|
|  21   | 1 |5 |150|8.1|7.660191|0.43980863|0.439809|
|  22   | 1 |7 |120|7.2|7.549570|-0.349570246|0.349570|
|  23   | 1 |12|180|8.5|8.142787|0.357213346|0.357213|
|  24   | 1 |2 |90|6.1|7.149636|-1.049635886|1.049636|

<br>

Erro médio absoluto (MAE): **0.6362742745**
</div>
<br>

## ***Representação Gráfica***

<br>

<img width="450" height="300" alt="image" src="https://github.com/user-attachments/assets/cacbac06-af09-4fc5-834c-63ada0889c3b" />
<img width="450" height="300" alt="image" src="https://github.com/user-attachments/assets/ba039795-0c17-4671-9dda-f47faa4e8675" />

*Photo by [Ralf Piredda]()*

<br>

## ***Conclusão***

Diferente do modelo que passa pela origem, a inclusão do intercepto ($\beta_0$) na equação estimada

$$\boxed{ \hat y_i = 6.4871 + 0.04133x_{i1} + 0.006442x_{i2} }$$

fornece flexibilidade para modelar fenômenos do mundo real.

O impacto dessa flexibilidade reflete-se diretamente na acurácia preditiva. Enquanto o modelo sem intercepto apresentou um Erro Médio Absoluto (MAE) elevado de 1.5823, a inclusão do intercepto reduziu esse erro para 0.6363. A dedução matricial de $\vec{\hat{\beta}} = (X^TX)^{-1}X^Ty$ com a inclusão da coluna de 1s na matriz de projeto $X$ garante que os resíduos (erros) tenham média zero e distribui de forma equilibrada as flutuações ao redor da reta de regressão, conferindo confiabilidade para a tomada de decisões.

Mesmo que o resultado tenha apresentado uma melhora com a inclusão do intercepto, podemos afirmar que a regressão linear foi o método mais adequado?  

Para respondermos a essa questão, antes precisaremos passar por alguns conceitos importantes para o estudo de regressões:  

- Testes de Normalidade
  - Teste Shapiro-Wilk
  - Teste Lilliefors (Kolmogorov-Smirnov)
- Homocedasticidade
  - Teste de Breusch-Pagan
- Outliers nos Resíduos
- Coeficientes de Correlação
  - Pearson (linear / dados normais)
  - Spearman (postos / não normal)
  - Kendall (postos / não normal e amostras menores)
- Estatística de teste t
- Coeficiente de Determinação ($R^2$)

<br>

## ***Testes de Normalidade***

Teste de normalidade é um procedimento estatístico usado para verificar se um conjunto de dados segue uma distribuição normal (curva em forma de sino).

<img width="450" height="300" alt="image" src="https://github.com/user-attachments/assets/b529aa1a-beeb-41f0-bb43-47f7bd027d88" />

*Photo by [andre.zibetti](https://www.inf.ufsc.br/~andre.zibetti/probabilidade/normal.html)*

<br>

Objetivo: Avaliar se a variável em estudo se comporta de forma paramétrica (normal).  

**Hipóteses:** 
- Hipótese nula (H₀):  
  Os dados seguem uma distribuição normal.

- Hipótese alternativa (H₁):  
  Os dados não seguem uma distribuição normal.

<br>

## ***Shapiro-Wilk***  

O teste de Shapiro-Wilk é um método para testar a normalidade de um conjunto de dados com até 5 mil observações.

A Fórmula do Teste ($W$)  A estatística do teste, denotada por $W$, é calculada pela seguinte razão:  

$$W = \frac{\left( \sum_{i=1}^{n} a_i x_{(i)} \right)^2}{\sum_{i=1}^{n} (x_i - \bar{x})^2}$$

Onde:  
- $n$: é o tamanho da amostra ($n = 25$).
- $x_{(i)}$: são os valores da amostra ordenados do menor para o maior ($x_{(1)} \le x_{(2)} \le \dots \le x_{(n)}$).  
- $\bar{x}$: é a média aritmética simples da amostra.
- $a_i$: são pesos estatísticos específicos obtidos a partir da covariância e dos valores esperados de estatísticas de ordem de uma normal padrão ( $N(0.1)$ ).  

<br>

## ***Passo a Passo***

Para calcular o $W$ à mão (ou entender o que o computador faz quando chamamos stats.shapiro), seguimos estas etapas:  

**Passo 1:** Organização e Ordenação dos Dados  

Pegamos os dados brutos da coluna (ex: RM ou MEDV) e os ordenamos em ordem crescente:

$$x_{(1)}, x_{(2)}, x_{(3)}, \dots, x_{(n)}$$

**Passo 2:** Cálculo do Denominador (Variabilidade Total)  

Calculamos a soma dos desvios quadráticos em relação à média (exatamente igual ao denominador da variância amostral):

$$\text{Denominador} = \sum_{i=1}^{n} (x_i - \bar{x})^2$$

**Passo 3:** Obtenção dos Coeficientes de Peso ($a_i$)  

Os coeficientes $a_i$ são simétricos (o peso do primeiro elemento espelha o do último, com sinal trocado). Eles vêm de tabelas polinomiais criadas por Shapiro e Wilk (ou calculadas via algoritmos complexos como a aproximação de Royston para $n$ grandes).

- Eles dão mais peso aos valores extremos (caudas da distribuição), pois é exatamente nas pontas que os dados não-normais costumam "fugir" da curva em sino.
  
**Passo 4:** Cálculo do Numerador (Soma Ponderada)  

Multiplicamos cada valor ordenado $x_{(i)}$ pelo seu respectivo peso $a_i$, somamos e elevamos o resultado ao quadrado:

$$\text{Numerador} = \left( \sum_{i=1}^{n} a_i x_{(i)} \right)^2$$

**Passo 5:** Obtenção do Estatístico $W$ e InterpretaçãoDividimos o numerador pelo denominador:

$$W = \frac{\text{Numerador}}{\text{Denominador}}$$

O que o valor de $W$ significa?  
- O coeficiente $W$ varia sempre entre 0 e 1.  
- Se $W$ for muito próximo de 1, significa que a distribuição dos seus dados se alinha à de uma curva normal.  
- Se $W$ for muito menor que 1 (próximo de 0), os dados apresentam forte assimetria ou desvio da normalidade.  

**Passo 6:** O Cálculo do P-valor ($p$-value)  

O algoritmo compara o $W$ obtido com a distribuição teórica de $W$ sob a hipótese nula para gerar o $p$-valor.  
- Se $p > 0.05$: Falhamos em rejeitar $H_0$. Consideramos que os dados seguem uma distribuição normal.  
- Se $p \le 0.05$: Rejeitamos $H_0$. Os dados não seguem uma distribuição normal.  

<br>

## ***Cálculo dos valores esperados da normal padrão***

Inicialmente, são determinados os quantis esperados da distribuição normal padrão. Para isso, define-se o vetor de índices:

$$
i=\begin{bmatrix}
1\\
2\\
3\\
\vdots\\
25
\end{bmatrix}
$$

<br>

Os valores esperados são obtidos por meio da transformação:

$$
m_i=\Phi^{-1} \left( \frac{i−\frac{3}{8}}{n+\frac{1}{4}}\right)
$$

em que $\Phi^{-1}$ representa a função quantil da inversa da distribuição normal padrão.

Para $n=25$, a expressão assume a forma:

$$
m_i=\Phi^{-1} \left( \frac{i−0,375}{25,25}\right)
$$
$$ \downarrow $$ 
$$
\vec{\hat{m_i}}=\begin{bmatrix}
-1,9642168419486300\\
-1,5191971786348200\\
-1,2593033267763100\\
\vdots\\
1,9642168419486300
\end{bmatrix}
$$

<br>

A aplicação dessa expressão aos 25 índices fornece o vetor de quantis esperados $\hat{\mathbf m}$, cujos valores extremos são aproximadamente $-1,96421684$ e $1,96421684$.

<br>

## ***Cálculo da soma dos quadrados dos quantis***

Na sequência, calcula-se a soma dos quadrados dos valores $m_i$, necessária para a determinação dos coeficientes de Royston:

$$
\sum^{n}_{i=1} m_i^2
$$

Em que:

$$
m_i^2 = m^Tm
$$

$$\downarrow$$ 

$$
m^Tm=\begin{bmatrix}
-1,9642168&
-1,5191971&
-1,2593033&
\dots&
1,9642168
\end{bmatrix}
\begin{bmatrix}
-1,9642168419486300\\
-1,5191971786348200\\
-1,2593033267763100\\
\vdots\\
1,9642168419486300
\end{bmatrix}
$$

$$ \downarrow $$ 

$$
m^2=\begin{bmatrix}
0,4417998157703870\\
0,3108412242151760\\
0,2544758389229410\\
\vdots\\
-0,4417998157703870
\end{bmatrix}
$$

<br>

Para os valores obtidos:

$$
\sum^{n}_i m_i^2=22,528896471497700
$$

<br>

## ***Determinação dos coeficientes extremos***

O primeiro coeficiente utilizado na aproximação de Royston é obtido a partir do maior quantil esperado:

$$
C_n=\frac{m_n}{\sqrt{\sum_{i=1}^{n}m_i^2}}.
$$

<br>

Assim, para $n=25$:

$$
C_{25}=\frac{1,9642168419486300}{\sqrt{22,528896471497700}}=0,413827617690387
$$

<br>

Analogamente, para o quantil imediatamente anterior:

$$
C_{n-1}=\frac{m_{n-1}}{\sqrt{\sum_{i=1}^{n}m_i^2}},
$$

resultando em:

$$
C_{24}=\frac{1,5191971786348200}{\sqrt{22,528896471497700}}=0,320069421975176.
$$

<br>

## ***Cálculo dos coeficientes*** $a_n$ ***e*** $a_{n-1}$

Para a aproximação dos coeficientes de Royston, define-se inicialmente:

$$
u=\frac{1}{\sqrt n}.
$$

<br>

Como $n=25$,

$$
u=\frac{1}{\sqrt{25}}=0,20.
$$

<br>

O coeficiente associado à maior ordem é calculado por

$$
\boxed{
  \begin{aligned}
    &a_n=C_{n}+0,221157u-0,147981u^2-2,07119u^3+4,434685u^4-2,706056u^5\\
    &\space\\
    &\space\\
    &\space\\
    &a_{25}=C_{25}+0,221157(0,20)-0,147981(0,20)^2-2,07119(0,20)^3+4,434685(0,20)^4-2,706056(0,20)^5\\
    &\space\\
    &\space\\
    &\space\\
    &a_{25}=0,413827617690387+0,0442314-0,00591924-0,01656952+0,007095496-0,00086593792
  \end{aligned}
}
$$

$$ \downarrow $$ 

$$
a_{25}=0,441799815770387
$$

<br>

Igualmente para $a_{n-1}$, utiliza-se:

$$
\boxed{
  \begin{aligned}
    &a_{n-1}=C_{n-1}+0,042981u-0,293762u^2-1,752461u^3+5,682633u^4-3,582633u^5\\
    &\space\\
    &\space\\
    &\space\\
    &a_{24}=C_{24}+0,042981(0,20)-0,293762(0,20)^2-1,752461(0,20)^3+5,682633(0,20)^4-3,582633(0,20)^5\\
    &\space\\
    &\space\\
    &\space\\
    &a_{24}=0,320069421975176+0,0085962-0,01175048-0,014019688+0,0090922128-0,001146442560
  \end{aligned}
}
$$

$$ \downarrow $$ 

$$
a_{24}=0,310841224215176
$$

<br>

## ***Determinação de*** $\eta$

Com os valores de $a_{25}$ e $a_{24}$, determina-se o fator de normalização $\eta$ por:

$$
\boxed{
  \begin{aligned}
    &η = \frac{ \sum^{n}_{i=1} m_i^2 - 2m_{n}^2 - 2m_{n-1}^2}{1-2a_{n}^2-2a_{n-1}^2}\\
    &\space\\
    &\space\\
    &\space\\
    &η = \frac{22,5288964714977 - 2 \times 1,96421684194863^2 - 2 \times 1,51919717863482^2}{1-2\times0,441799815770387^2-2\times0,310841224215176^2}\\
    &\space\\
    &\space\\
    &\space\\
    &η = \frac{22,5288964714977 - 7,716295604 - 4,615920135}{1-0,390374154-0,193244533}\\
    &\space\\
    &\space\\
    &\space\\
    &η = \frac{10,1966807319644}{0,416381312}
  \end{aligned}
}
$$

$$ \downarrow $$ 

$$
η = 24,4888049307975
$$

<br>

Os coeficientes são determinados por:

$$
\vec{\hat{a}}=a_{i=13}^{23} \cup a_{i=24}^{25}
$$

<br>

Sendo o vetor intermediário:

$$
a_{i=13}^{23}=\frac{m_{i}}{\sqrt{η}}
$$

$$\downarrow$$ 

$$
a_{i=13}^{23} =\frac{m_i}{\sqrt{24,4888049307975}}
$$

$$\downarrow$$ 

$$
a_{i=13}^{23}=\begin{bmatrix}
0,0000000000000000\\
0,0200937024567133\\
0,0403885744211470\\
0,0611002786348897\\
0,0824762869770886\\
0,1048199468783080\\
0,1285281947032720\\
0,1541570107663560\\
0,1825473174182830\\
0,2150988204776230\\
0,2544758389229410
\end{bmatrix}
$$

<br>

Que deve ser complementado pelos coeficientes extremos $a_{24}$ e $a_{25}$. 

Considerando a ordenação necessária para a aplicação do teste, obtém-se o vetor de coeficientes de Royston:

$$
\vec{\hat{a}}=a_{i=13}^{23} \cup a_{i=24}^{25}
$$

$$\downarrow$$ 

$$
\vec{\hat{a}}=\begin{bmatrix}
0,0000000000000000\\
0,0200937024567133\\
0,0403885744211470\\
0,0611002786348897\\
0,0824762869770886\\
0,1048199468783080\\
0,1285281947032720\\
0,1541570107663560\\
0,1825473174182830\\
0,2150988204776230\\
0,2544758389229410
\end{bmatrix}
\cup  
\begin{bmatrix}
0,310841224215176\\
0,441799815770387
\end{bmatrix}
$$

$$\downarrow$$ 

$$
\vec{\hat{a}}=\begin{bmatrix}
0,0000000000000000\\
0,0200937024567133\\
0,0403885744211470\\
0,0611002786348897\\
0,0824762869770886\\
0,1048199468783080\\
0,1285281947032720\\
0,1541570107663560\\
0,1825473174182830\\
0,2150988204776230\\
0,2544758389229410\\
0,310841224215176\\
0,441799815770387
\end{bmatrix}
$$

<br>


---
---

<br>

Dado os seguintes conjuntos de dados:

<br>
<div align=center>

**Conjunto de dados (Observações)**

|       | <div align="center" style="width: 80px;">$y$</div> | <div align="center" style="width: 80px;">Previsão ($\hat y$)</div> | <div align="center" style="width: 200px;">Resíduos ($y - \hat y$)</div> |
| :---: | :---: | :---: | :---: |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8.1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;7.466909&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0.633090679&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|   1   |6.8|7.604271|-0.80427097|
|   2   |7.0|8.086866|-1.086866254|
|   3   |7.4|8.030946|-0.630945854|
|   4   |9.3|8.280148|1.019851697|
|   5   |7.5|8.445470|-0.945470151|
|   6   |7.6|7.617641|-0.017641232|
|   7   |8.0|7.590901|0.409099292|
|   8   |7.0|8.116046|-1.11604613|
|   9   |7.3|7.562941|-0.262940508|
|  10   |8.6|7.686932|0.913068106|
|  11   |8.3|7.632231|0.66776883|
|  12   |7.9|7.894804|0.005196119|
|  13   |6.4|7.232297|-0.832296811|
|  14   |7.8|7.784183|0.015817243|
|  15   |9.4|7.756223|1.643777443|
|  16   |8.8|8.060126|0.73987427|
|  17   |6.9|7.190966|-0.290966348|
|  18   |7.7|8.266778|-0.566778041|
|  19   |8.2|7.438949|0.761050879|
|  20   |8.6|8.252188|0.347811897|
|  21   |8.1|7.660191|0.43980863|
|  22   |7.2|7.549570|-0.349570246|
|  23   |8.5|8.142787|0.357213346|
|  24   |6.1|7.149636|-1.049635886|

<br>

**Coeficientes Shapiro-Wilk (Royston)**

|<div align="center" style="width: 100px;">$i$</div> | <div align="center" style="width: 100px;">$a$</div> |
| :---: | :---: |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0.441802&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|2|0.310852  |
|3|0.254467  |
|4|0.215099  |
|5|0.182557  |
|6|0.154166  |
|7|0.128524  |
|8|0.104834  |
|9|0.082465  |
|10|0.061101 |
|11|0.040399 |
|12|0.020105 |
|13|0.000000 |
|14|-0.020105 |
|15|-0.040399 |
|16|-0.061101 |
|17|-0.082465 |
|18|-0.104834 |
|19|-0.128524 |
|20|-0.154166 |
|21|-0.182557 |
|22|-0.215099 |
|23|-0.254467 |
|24|-0.310852 |
|25|-0.441802 |

</div>
<br>

Considerando os valores observados, as previsões obtidas pelo modelo e os respectivos resíduos apresentados anteriormente, procede-se, nesta etapa, ao cálculo dos coeficientes utilizados no teste de normalidade de Shapiro–Wilk, conforme a formulação de Royston. Para o conjunto de dados considerado, tem-se $n=25$ observações.

<br>

## ***A estatística do teste*** $W$


Calculada pela razão:  

$$W = \frac{\left( \sum_{i=1}^{n} a_i x_{(i)} \right)^2}{\sum_{i=1}^{n} (x_i - \bar{x})^2}$$

<br>
Sendo: 

$$
\vec{\hat{ax}}=\begin{bmatrix}
0.441802\\
0.310852\\
0.254467\\
\vdots \\
-0.4418\\
\end{bmatrix}
\underbrace{
\begin{bmatrix}
-1.11604612984445\\
-1.08686625396935\\
-1.04963588625130\\
\vdots\\
1.64377744336372
\end{bmatrix}
}_\text{{Resíduos ($\hat{\epsilon} = y - \hat{y}) \textcolor{orange}{\downarrow^A_Z}$}}
$$

$$\downarrow$$

$$
\vec{\hat{ax}}=\begin{bmatrix}
-0.493071412\\
-0.337854548\\
-0.267097695\\
\vdots \\
-0.726224162
\end{bmatrix}
$$

<br>
Logo:

$$
\left( \sum_{i=1}^{n} a_i x_{(i)} \right)^2
=((-0.493071412)+(-0.337854548)+(-0.267097695)+\cdots+(-0.726224162) )^2
$$

$$\downarrow$$

$$
\left( \sum_{i=1}^{n} a_i x_{(i)} \right)^2= 13.323484559
$$

<br>

e a média de $x$:

$$
\bar{x}=\frac{1}{n}\sum_{i=1}^{n}y_i​−\hat{y_i}​
$$
$$\downarrow$$
$$
\bar{x}=\frac{(-1.116046)+(-1.086866)+(-1.049635)+\cdots+1.643777}{n} = -1.52E^{-14}
$$

<br>

Então:

$$
x-\bar{x}=\begin{bmatrix}
1.11604612984445\\
1.08686625396935\\
1.04963588625130\\
\vdots\\
1.64377744336372
\end{bmatrix}
-1.52E^{-14}\\
$$

$$\downarrow$$

$$
x-\bar{x}=\begin{bmatrix}
1.11604612984444\\
1.08686625396934\\
1.04963588625129\\
\vdots\\
1.64377744336371
\end{bmatrix}
$$

<br>

Sendo:

$$
(x-\bar{x})^2=(x-\bar{x})^T(x-\bar{x})\\
$$

$$\downarrow$$

$$
(x-\bar{x})^2=
\begin{bmatrix}
1.11604612984444&
1.08686625396934&
\cdots&
1.64377744336371
\end{bmatrix}
\begin{bmatrix}
1.11604612984444\\
1.08686625396934\\
1.04963588625129\\
\vdots\\
1.64377744336371
\end{bmatrix}
$$

$$\downarrow$$

$$(x-\bar{x})^2=\begin{bmatrix}
1.245558964\\
1.181278254\\
1.101735494\\
\vdots\\
2.702004283
\end{bmatrix}
$$

<br>

Então, a soma do quadro dos resíduos absolutos:

$$
\boxed{
  \begin{aligned}
&\sum(x-\bar{x})^2=1.245558964+1.181278254+1.101735494+\cdots+2.702004283
  \end{aligned}
}
$$

$$\downarrow$$

$$
\sum(x-\bar{x})^2= 13.91646807
$$

<br>

Portanto, substituimos os valores da equação:

$$
\boxed{
  \begin{aligned}
&W = \frac{\left( \sum_{i=1}^{n} a_i x_{(i)} \right)^2}{\sum_{i=1}^{n} (x_i - \bar{x})^2}\\
&W = \frac{13.323484559}{13.91646807}
  \end{aligned}
}
$$

$$\downarrow$$

$$W = 0.957389798$$

<br>

## ***Transformação logarítmica de*** $W$

<br>

$p-value$ ***por interpolação linear***

Considerando a Tabela de Quantis de $W$ para $n = 25$:

<br>

| $p-valor$ (Probabilidade) | Estatístico $W$ |
|:---:|:---:|
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0.01&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0.888&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|0.02| 0.901|
|0.05| 0.918|
|0.10| 0.931|
|0.50| 0.964|
|0.90| 0.981|
|0.95| 0.985|
|0.98| 0.988|
|0.99| 0.989|

<br>

De acordo com a tabela de Quantis e considerando os parâmetros a seguir:

 - $W=0.957389798;$
 - $n = 25.$

<br>

Temos:  

- $0.10 \le p \le 0.50;$
- $0.931 \le W \le 0.964.$

<br>

Então:

$$
p-valor = p_{min}+\left( \frac{W - W_{min}}{W_{max} - W_{min}} \right) \times (p_{max} - p_{min})
$$
$$\downarrow$$
$$
p-valor \approx 0.10 + \left( \frac{0.957389798 - 0.931}{0.964 - 0.931} \right) \times (0.50 - 0.10)
$$
$$\downarrow$$
$$
p-valor \approx 0.419876344
$$

<br><br>

***Aproximação do*** $p-value$ ***do teste de Shapiro-Wilk para*** $n>11$

<br>

Coeficientes dos polinômios $C_5$ e $C_6$

<br>

| Polinômio  | Coeficiente |  Valor |
| :--------- | :---------: | -----: |
| $C_5(x)$ | $c_{50}$ |   $-1.5861$ |
| $C_5(x)$ | $c_{51}$ |  $-0.31082$ |
| $C_5(x)$ | $c_{52}$ | $-0.083751$ |
| $C_5(x)$ | $c_{53}$ | $0.0038915$ |
| $C_6(x)$ | $c_{60}$ |   $-0.4803$ |
| $C_6(x)$ | $c_{61}$ | $-0.082676$ |
| $C_6(x)$ | $c_{62}$ | $0.0030302$ |

<br>

Sendo:
- $W=0.957364809687$
- $n=25$

<br>

Calculamos $y$:

$$ 
\boxed{
  \begin{aligned}
    y&=\ln(1-W) \\
    y&=\ln(1-0.957364809687) 
  \end{aligned}
}
$$ 
$$ \downarrow $$ 
$$ y=-3.155075303$$ 

<br>

Calculamos $x$:

$$ 
\boxed{
  \begin{aligned}
    x&=\ln(n)\\
    x&=\ln(25) 
  \end{aligned}
}
$$ 
$$ \downarrow $$ 
$$ x=3.218875825$$ 

<br>

Calculamos $m$:

$$ 
\boxed{
  \begin{aligned}
    m&=c_1+c_2x+c_3x^2+c_4x^3 \\
    m&=-1.5861-0.31082x-0.083751x^2+0.0038915x^3 \\
    m&=-1.5861-0.31082(3.218875825)-0.083751(3.218875825)^2+0.0038915(3.218875825)^3
  \end{aligned}
}
$$ 

$$ \downarrow $$ 
$$m=-3.324562072$$

<br>

Calculamos $s$:

$$
\boxed{
  \begin{aligned}
    s&=e^{c_5+c_6x+c_7x^2}\\
    s&=e^{-0.4803+-0.082676x+0.0030302x^2}\\
    s&=e^{-0.4803+-0.082676(3.218875825)+0.0030302(3.218875825)^2}
  \end{aligned}
}
$$ 
$$ \downarrow $$ 
$$s=0.489178715$$

<br>

Calculamos $z$:

$$
\boxed{
  \begin{aligned}  
    z&=\frac{y-m}{s}\\
    z&=\frac{-3.155075303-(-3.324562072)}{0.489178715}
  \end{aligned}
}
$$ 
$$ \downarrow $$ 
$$z=0.346472085$$

<br>

Finalmente $p$:

$$
\boxed{
  \begin{aligned} 
    p&=1-\Phi(z)\\
    p&=1-\Phi(0.346472085)
  \end{aligned}
}
$$

$$ \downarrow $$ 

$$p-valor = 0.364493979877$$

<br>

### ***Interpretação***

Como o p-valor obtido ($0.36449$) é superior a $0.05$, não há evidência estatística suficiente para rejeitar a hipótese nula ($H_0$), confirmando que os dados seguem uma distribuição normal.

![alt text](image-11.png)

</div>








































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
