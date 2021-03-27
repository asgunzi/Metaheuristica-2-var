# Metaheuristica-2-var
Exemplo de metaheurística de otimização com 2 variáveis - VBA


Essa versão é um pouquinho mais elaborada que a ![versão com uma variável](https://ferramentasexcelvba.wordpress.com/2021/03/27/exemplo-de-metaheuristica-uma-variavel/)

Serve para resolver o problema linear:

Max 10*x +5*y

Sujeito a:

2*x+4*y <= 50

1*x -6*y <= 15



É semelhante ao anterior, mas agora as variáveis são matrizes.

‘Inicializando coeficientes FO

coefFO(1) = 10

coefFO(2) = 5

‘Inicializando coeficientes Matriz

coefMatriz(1, 1) = 2

coefMatriz(1, 2) = 4

coefMatriz(2, 1) = 1

coefMatriz(2, 2) = -6

‘Inicializando rhs

RHS(1) = 50

RHS(2) = 15


Um parâmetro adicional, restringindo as variáveis a assumir valor máximo 50 e mínimo 0.

For i = 1 To nvar

    varmin(i) = 0 ‘Range Mínimo

    varmax(i) = 50 ‘Range Máximo

Next i



Em linhas gerais:

– Escolhe valores aleatórios no range das variáveis

– Pondera o valor aleatório com a melhor solução até agora

– Lambda controla o mix valor aleatório x melhor solução até agora. No início lambda é pequeno, depois vai aumentando

– Verifica se cumpre todas as restrições

 – função objetivo que avalia a solução

– salva o histórico





‘Algoritmo evolutivo

For iter = 1 To Niteracoes ‘Numero de iteracoes

    lambda = iter / Niteracoes

    ‘Sorteia um valor

    sorteia var, varmin, varmax, varbest, lambda

    ‘Verifica restricoes

    isOk = verificaRestricoes(var, coefMatriz, RHS)

    If isOk Then

        ‘Avalia a função atual

        FOatual = FO(var, coefFO)

        ‘Salva a melhor (maximizando)

        If FOatual > FOBest Then

            FOBest = FOatual

            copiaUni var, varbest

        End If

    End If

    FOhist(iter, 1) = FOBest

Next iter



	
Usando o solver, as variáveis ótimas são 22,5 e 1,25.
![](https://ferramentasexcelvba.files.wordpress.com/2021/03/metah_01.png)

A metaheurística chega a valores próximos ao ótimo, o que mostra que funciona para uma solução suficientemente boa.
![](https://ferramentasexcelvba.files.wordpress.com/2021/03/metah_02.png)


Provavelmente, com muitas variáveis e muitas restrições, vai ficar bem mais difícil convergir para uma solução boa.

Uma coisa ruim é todas as equações serem hard coded, mas quem domina código consegue fazer isso fácil.

É possível “tunar” esse algoritmo básico com pré processamento, ou algum chute guiado ao invés de ser basicamente aleatório, mas aí vai depender do problema.

Planilha para download aqui no Github.


Texto original: ![aqui](https://ferramentasexcelvba.wordpress.com/2021/03/27/metaheuristica-com-2-variaveis/)
