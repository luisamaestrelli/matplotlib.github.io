# MatPlotLib
<h6>Introdução ao PyPlot</h6>

### O que é? 
É uma biblioteca com recursos para a geração de gráficos 2D a partir de um arranjo. São gráficos comuns que podem ser criados com comandos simples, inpirados nos comandos gráficos do <a href="https://www.mathworks.com/products/matlab.html">MATLAB</a>
  
### Como funciona
O funcionamento do ```matplotlib``` pode ser explicado em 3 partes
1. **pylab**: Conjunto de funções disponível em ```matplotlib.pylab``` que permite a geração de código similar ao MATLAB
2. **frontend** ou **API**: conjunto de classes que realizam o trabalho de criar
    - figuras;
    - textos;
    - linhas.
3. **backends**: É um conjunto de funções que dependem do dispositivo de saída (display) como
    - ```PS```: Para gráficos em PostScript;
    - ```SVG```: Gera gráficos em Scalable Vector Graphics;
    - ````Agg````: Cria figuras no formato PNG;
    - ````GTK````: Permite que os gráficos sejam incluídos em aplicações ``GTK+``, e assim para ``PDF``, ``WxWidgets``, ``Tkinter``, etc.  
    
### Instalação
 Para usar o ``matplotlib`` é recomendado o uso da <a href="https://www.anaconda.com/">Anaconda</a> e do <a href="https://www.activestate.com/products/python/downloads/">ActiveState</a> que funcionam para Windows, macOS e plataformas Linux. Ambos são distribuidores que incluem o ``matplotlib`` e várias outras ferramentas. Para mais informações e um passo a passo mais detalhados visitar o <a href="https://matplotlib.org/users/installing.html">Installation Guide</a>

### Pacote PyPlot
As funções disponíveis no pacote ```matplotlib.pyplot``` fazem com que o ``matplotlib`` funcione como o MATLAB, sua principal função é tornar visível um determinado conjunto de dados. Cada função do ``pyplot`` muda algo na figura como
   - Plotando com strings de palavra-chave;
   - Plotando com variáveis categóricas;
   - Controlando propriedades de linha;
   - Trabalhando com várias figuras e eixos;
   - Trabalhando com texto;
   - Usando expressões matemáticas em texto;
   - Anotando texto;
   - Eixos logarítmicos e outros eixos não lineares.
    
O ``pyplot`` já tem uma figura e uma área de desenho padrão, ou seja, que não precisa de uma definição prévia. Assim o código para gerar um gráfico pode ser apenas:
```
import matplotlib.pyplot as plt
plt.plot( [10,5,3,4,6,8] ) #Se você fornece apenas uma lista ou arranjo para o plot, o matplotlib assume que é uma sequência de valores de y e automaticamente gera valores de x 
plt.title("Muito Fácil")
plt.show()
```

<img src="grafico q.png" alt="grafico 1" title="Avatar " />


``plot`` é um método versátil, ele aceita vários números arbitrários como argumento, por exemplo o usuário quiser plotar x por y:
```
plt.plot([2, 4, 6, 8], [2, 6, 9, 16])
```
*imagem*

<h5>Formatando o estilo do seu plot</h5>
Para todo par de argumento, x e y, tem um terceiro argumento opcional do tipo string que indica o tipo e a cor da linha do plot. As letras e os símbolos da string são do MATLAB e você liga uma string de cor com uma string do tipo da linha. Como visto acima o formato de string default é ```b-``` que é uma linha azul sólida.
Exemplo: o mesmo plot com círculos amarelos
```
plt.plot([2, 4, 6, 8], [2, 6, 9, 16], 'yo')
```

*imagem*


Como listas são muito limitantes, geralmente é usado ``<a href="https://numpy.org/">numpy</a>`` arrays. Na verdade todas as sequências são convertidas para ``numpy`` internamente. No exemplo abaixo


