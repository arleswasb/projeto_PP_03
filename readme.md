# Disciplina: Programação Paralela
**Professor:** Samuel Xavier de Souza
**Projeto PP 03**

## Descrição da Tarefa

Implemente e compare duas versões de um programa em C que calcule uma aproximação de π usando uma série matemática. A primeira versão deve ser puramente sequencial, enquanto a segunda deve ser otimizada explorando o paralelismo em nível de instrução (ILP). O objetivo é medir o tempo de execução de ambas, comparar os resultados e analisar o ganho de desempenho (speedup) obtido com a otimização.

## Objetivo do Teste

O objetivo deste estudo é demonstrar empiricamente um dos princípios mais importantes da computação de alto desempenho: a relação direta entre **custo computacional (tempo) e a precisão do resultado**, e como técnicas de **programação paralela** podem mitigar esse custo. Este experimento utiliza o cálculo de π para visualizar esse trade-off fundamental e a eficácia da otimização.

## O Experimento: A Série de Leibniz para π

Para este experimento, foi utilizada a **série de Leibniz**, uma das séries infinitas mais simples para aproximar o valor de π. A fórmula é:

$$
\frac{\pi}{4} = \sum_{n=0}^{\infty} \frac{(-1)^n}{2n+1} = 1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + \frac{1}{9} - \cdots
$$

Apesar de sua simplicidade, a série de Leibniz converge muito lentamente, o que a torna um excelente exemplo didático: para obter uma precisão razoável, é necessário um número muito grande de iterações, tornando o custo computacional evidente e a otimização, necessária.

## Procedimentos de Execução

O projeto consiste em dois códigos-fonte, que devem ser compilados separadamente com a biblioteca matemática (`-lm`).

1.  **Compilação:**
    * **Versão Sequencial:**
        ```bash
        gcc pi_sequencial.c -o pi_sequencial -lm
        ```
    * **Versão Otimizada (ILP):**
        ```bash
        gcc pi_ilp.c -o pi_ilp -lm
        ```

2.  **Execução:**
    Cada programa pode ser executado para gerar seus respectivos resultados de tempo e precisão.
    ```bash
    ./pi_sequencial
    ./pi_ilp
    ```

## Resultados Comparativos e Speedup

A execução e a coleta de dados de ambas as versões produziram os resultados consolidados na tabela abaixo. A coluna "Speedup" (calculada como Tempo Sequencial / Tempo ILP) demonstra o ganho de desempenho da versão otimizada.

| Iterações | Tempo Sequencial (s) | Tempo ILP (s) | Speedup |
| :--- | :--- | :--- | :--- |
| 10 | 0.0000005 | 0.0000001 | 5.00x |
| 100 | 0.0000003 | 0.0000001 | 3.00x |
| 1,000 | 0.0000026 | 0.0000010 | 2.60x |
| 10,000 | 0.0000261 | 0.0000098 | 2.66x |
| 100,000 | 0.0002666 | 0.0000979 | 2.72x |
| 1,000,000 | 0.0029831 | 0.0009832 | 3.03x |
| 10,000,000 | 0.0347278 | 0.0117944 | 2.94x |
| 100,000,000 | 0.2930814 | 0.1071978 | 2.73x |
| 1,000,000,000 | 2.5113620 | 1.4679070 | 1.71x |

*(Nota: Os tempos de execução podem variar dependendo do hardware.)*

## Análise e Reflexão: O Trade-off no Mundo Real

A tabela de resultados ilustra perfeitamente o conceito:

* **Aumento da Acurácia:** A cada ordem de magnitude no número de iterações, o erro absoluto diminui, e o valor calculado de π se aproxima cada vez mais do valor real.

* **Aumento do Custo:** Ao mesmo tempo, o tempo de execução cresce de forma aproximadamente linear com o número de iterações. Para obter um dígito a mais de precisão, pagamos um preço computacional significativamente maior.

Este comportamento não é exclusivo do cálculo de π. Ele é um padrão universal em computação de alto desempenho, com paralelos diretos em áreas críticas:

### 1. Simulações Físicas e de Engenharia

Em domínios como **previsão do tempo, dinâmica de fluidos computacional (CFD) ou simulações de elementos finitos**, a precisão do resultado depende da "resolução" da simulação (o tamanho da malha ou o passo de tempo).

* **Baixo Custo / Baixa Precisão:** Uma simulação com uma malha grosseira é rápida, mas pode não capturar turbulências importantes ou pontos de estresse num material, levando a conclusões erradas.

* **Alto Custo / Alta Precisão:** Refinar a malha aumenta drasticamente a precisão, mas o custo computacional pode crescer de forma cúbica ou pior. Simulações de alta fidelidade exigem supercomputadores e semanas de processamento.

### 2. Inteligência Artificial e Machine Learning

O treino de modelos de **Deep Learning** é um processo iterativo onde o modelo ajusta seus pesos para minimizar uma função de erro (loss).

* **Baixo Custo / Baixa Precisão:** Treinar por poucas épocas é rápido, mas resulta num modelo "sub-treinado" (*underfit*), que não aprendeu os padrões nos dados e terá um desempenho pobre.

* **Alto Custo / Alta Precisão:** Treinar por muitas épocas reduz o erro, mas exige dias ou semanas de processamento em hardware especializado (GPUs/TPUs) e consome uma quantidade massiva de energia. O desafio é encontrar o ponto ótimo antes que o modelo comece a "decorar" os dados (*overfitting*).

### 3. Renderização Gráfica e Ray Tracing

Na geração de imagens fotorrealistas, a qualidade da imagem (ausência de ruído, reflexos precisos) depende do número de raios de luz simulados por pixel.

* **Baixo Custo / Baixa Qualidade:** Poucos raios por pixel resultam numa imagem "granulada" e com artefatos.

* **Alto Custo / Alta Qualidade:** Aumentar o número de raios produz uma imagem limpa e realista, mas o tempo de renderização pode passar de segundos para horas por frame.

### Conclusão do Especialista em Programação Paralela

O problema do cálculo de π, assim como os exemplos citados, é um problema **"compute-bound"** (limitado pelo processamento). A boa notícia é que muitas dessas tarefas são também **"embaraçosamente paralelas"**. O cálculo de cada termo da série, a atualização de cada célula numa simulação, ou o processamento de diferentes lotes de dados em IA podem ser feitos de forma independente.

Os resultados deste experimento demonstram exatamente como a **programação paralela** se torna a solução. Ao dividir o trabalho (as iterações) entre múltiplas unidades de processamento — ou, neste caso, otimizando o fluxo de instruções para o pipeline do processador (ILP) —, podemos alcançar a precisão desejada num tempo de execução muito menor. O desafio, portanto, não é apenas encontrar um algoritmo que convirja, mas também estruturá-lo de forma que ele possa ser eficientemente paralelizado para gerir o inevitável trade-off entre custo e precisão.

# Gráficos #

![Gráfico Comparativo de de Desempenho](graficos.png)