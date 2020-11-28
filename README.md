# MatPlotLib
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
 Para usar o ``matplotlib`` é recomendado o uso da <a href="https://www.anaconda.com/">Anaconda</a> e do <a href="https://www.activestate.com/products/python/downloads/">ActiveState</a> que funcionam para Windows, macOS e plataformas Linux. Ambos são distribuidores que incluem o ``matplotlib`` e várias outras ferramentas.

### Pacote PyPlot
O pacote ```matplotlib.pyplot``` tem um conjunto de funções que permite que você crie uma figura, desenhe linhas na área do gráfico, decore o gráfico com rótulos, entre outros. Cada função do ```pyplot``` algo na figura 
