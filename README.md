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
plt.plot( [11,3,2,5,7,9] ) #Se você fornece apenas uma lista ou arranjo para o plot, o matplotlib assume que é uma sequência de valores de y e automaticamente gera valores de x 
plt.title("inicial")
plt.show()
```

*imagem1*

``plot`` é um método versátil, ele aceita vários números arbitrários como argumento, por exemplo o usuário quiser plotar x por y:
```
plt.plot([2, 4, 6, 8], [2, 6, 9, 16])
```
*imagem2*

<h6>Formatando o estilo do seu plot</h6>
Para todo par de argumento, x e y, tem um terceiro argumento opcional do tipo string que indica o tipo e a cor da linha do plot. As letras e os símbolos da string são do MATLAB e você liga uma string de cor com uma string do tipo da linha. Como visto acima o formato de string default é ```b-``` que é uma linha azul sólida.
Exemplo: o mesmo plot com círculos amarelos
```
plt.plot([2, 4, 6, 8], [2, 6, 9, 16], 'yo')
```

*imagem3*


Como listas são muito limitantes, geralmente é usado [`numpy`](https://numpy.org/) arrays. Na verdade todas as sequências são convertidas para ``numpy`` internamente. O exemplo a seguir mostra várias linhas com diferentes estilos um uma chamada de função usando arrays 
```
import numpy as np

# tempo de intervalo iguais de 300 ms
t = np.arange(0., 7., 0.3)

# linha amarela, tracejado azul e quadrados cianos
plt.plot(t, t, 'y-', t, t**2, 'b--', t, t**3, 'cs')
plt.show()
```

*imagem4*

#### Plotando com strings de palavra-chave
Existem circunstâncias em que o formato do data possibilita o acesso a determinadas variáveis com strings. Por exemplo com [`numpy.recarray`](https://numpy.org/doc/stable/reference/generated/numpy.recarray.html#numpy.recarray) ou [`pandas.DataFrame`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html#pandas.DataFrame)

O ``matplotlib`` permite que você forneça o objeto com ``data`` como argumento key. Uma vez fornecido, é possível gerar plots com as strings correspondentes às variáveis.
```
data = {'a': np.arange(60),
        'c': np.random.randint(0, 60, 60),
        'd': np.random.randn(60)}
data['b'] = data['a'] + 15 * np.random.randn(60)
data['d'] = np.abs(data['d']) * 110

plt.scatter('a', 'b', c='c', s='d', data=data)
plt.xlabel('entrada a')
plt.ylabel('entrada b')
plt.show()
```

*imagem5*

#### Plotando com variáveis categóricas
Também podemos criar um plot com variáveis categóricas, o ``matplotlib`` possibilita você passá-las diretamente para várias funções de plotagem.
```
nomes = ['amostra1', 'amostra2', 'amostra3']
valores = [35, 50, 200]

plt.figure(figsize=(9, 3), facecolor='c')

plt.subplot(131)
plt.bar(nomes, valores)
plt.subplot(132)
plt.scatter(nomes, valores, c='r', edgecolors='r')
plt.subplot(133)
plt.plot(nomes, valores)
plt.suptitle('Conhecendo PyPlot')
plt.show()
```

*imagem6*

### Controlando propriedades de linha
É possível atribuir várias características para uma linha como: largura da linha, estilo do traço, suavização, etc. Existem vários modos de definir essas propriedades, sendo eles:
  - Argumentos de keywords
  
          
          plt.plot(x, y, linewidth=2.0)
          
  - Usar os métodos de definição de uma ``Line2D``. O ``plot`` retorna uma lista de ``Line2D`` objetos. 
  
          
          line, = plt.plot(x, y, '-')
          line.set_antialiased(False) # turn off antialiasing
          
  - Usar [`setp`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.setp.html#matplotlib.pyplot.setp). O exemplo a seguir usa uma função estilo MATLAB que define várias           propriedades em uma lista de linhas. O ``setp`` funciona ou com uma lista de objetos ou com um objeto único e você pode usar pares tanto de argumentos keywords do python         como strings e valores do MATLAB
  
          
          lines = plt.plot(x1, y1, x2, y2)
          # usar os argumentos keywords
          plt.setp(lines, color='r', linewidth=2.0)
          # ou string e valores do MATLAB
          plt.setp(lines, 'color', 'r', 'linewidth', 2.0)
          
Todas as propriedades estão disponíveis no [`matplotlib.lines.Line2D`](https://matplotlib.org/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D)

#### Trabalhando com várias figuras e eixos
O MATLAB e o ``pyplot``, possuem o conceito da figura atual e dos e dos eixos atuais, todas as suas funções de plotagem se aplicam aos eixos atuais. Com isso, abaixo está um script para a criação de dois subplots:
```
def f(t):
    return np.exp(-t) * np.cos(2*np.pi*t)

t1 = np.arange(0.0, 5.0, 0.1)
t2 = np.arange(0.0, 5.0, 0.02)

plt.figure()                                  # O comando figure é opcional porque o figure(1) seria criado por default
plt.subplot(211)                              # O comando subplot(111) também é criado por default se o usuário não especificar o número de eixos manualmente
plt.plot(t1, f(t1), 'bo', t2, f(t2), 'k')

plt.subplot(212)
plt.plot(t2, np.cos(2*np.pi*t2), 'r--')
plt.show()
```

*imagem7gráfico*

O comando ``subplot`` especifica ``numrows``, ``numcols``, ``plot_number`` (variando de 1 até numrowsxnumcols). As vírgulas são opcionais no caso de numrowsxnumcols menores que 10.  Portanto, ``subplot (211)`` é idêntico à ``subplot (2, 1, 1)``.
É possível que se crie um número arbitrário de subplot. Se você quiser posicionar os eixos manualmente, por exemplo uma grade não retangular, basta usar [`matplotlib.pyplot.axes`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.axes.html#matplotlib.pyplot.axes), eles permite que o usuário especifique a posição dos eixos em ``axes([left, bottom, width, height])`` onde todos os valores são coordenadas fracionárias, variando de 0 a 1. É possível encontrar mais exemplos e detalhes em <a href="https://matplotlib.org/gallery/subplots_axes_and_figures/axes_demo.html">Axes Demo</a>.

É possível criar múltiplas figuras usando vários comandos ``figures`` com número crescentes. Cada figura pode conter qualquer quantidade de eixos e subplots, no código a seguir temos 2 figuras, onde a figura 1 tem dois subplots e a segunda apenas um.
import matplotlib.pyplot as plt
```
plt.figure(1)                # primeira figura
plt.plot([4, 5, 6], 'r-')    # cria um subplot(111) por default

plt.figure(2)                # a segunda figura
plt.subplot(121)             # o primeiro subplot na segunda figura
plt.plot([1, 2, 3], 'g')
plt.subplot(122)             # o segundo subplot na segunda figura
plt.plot([4, 5, 6], 'g')

plt.figure(2)                   # figura 2 atual
plt.title('Subplots e Figuras') # título da segunda figura
```

#### Trabalhando com texto
``text`` pode ser usado para adicionar texto em um lugar arbitrário e ``xlabel``, ``ylabel`` e ``title`` adicionam texto em uma determinada posição (consultar <a href="https://matplotlib.org/tutorials/text/text_intro.html">Texto em MatPlotLib plots</a>).
```
beta, mu = 100, 15
x = beta + mu * np.random.randn(10000)

# the histogram of the data
n, bins, patches = plt.hist(x, 50, density=0.7, facecolor='c', alpha=0.75)


plt.xlabel('exemplo1')
plt.ylabel('exemplo2')
plt.title('Plotando')
plt.text(50, .022, r'$\beta=100,\ \mu=15$')
plt.axis([40, 160, 0, 0.03])
plt.grid(True)
plt.show()
```

*imagem8*

Todas as funções de ``text`` retornam uma intância de ``matplotlib.text.Text`` 



