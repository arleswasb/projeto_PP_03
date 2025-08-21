Claro. Aqui está o código completo do arquivo `README.md` que está no Canvas.

````markdown
# Disciplina: Programação Paralela
**Professor:** Samuel Xavier de Souza
**Projeto PP 03**

## Descrição da Tarefa

Implemente um programa em C que calcule uma aproximação de π usando uma série matemática, variando o número de iterações e medindo o tempo de execução. Compare os valores obtidos com o valor real de π e analise como a acurácia melhora com mais processamento. Reflita sobre como esse comportamento se repete em aplicações reais que demandam resultados cada vez mais precisos.

## Objetivo do Teste

O objetivo deste estudo é demonstrar empiricamente um dos princípios mais importantes da computação de alto desempenho: a relação direta entre **custo computacional (tempo) e a precisão do resultado**. Muitos problemas complexos não podem ser resolvidos de forma exata e instantânea, exigindo métodos iterativos que convergem para a solução correta. Este experimento utiliza o cálculo de π para visualizar esse trade-off fundamental.

## O Experimento: A Série de Leibniz para π

Para este experimento, foi utilizada a **série de Leibniz**, uma das séries infinitas mais simples para aproximar o valor de π. A fórmula é:

$$
\frac{\pi}{4} = \sum_{n=0}^{\infty} \frac{(-1)^n}{2n+1} = 1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + \frac{1}{9} - \cdots
$$

Apesar de sua simplicidade, a série de Leibniz converge muito lentamente, o que a torna um excelente exemplo didático: para obter uma precisão razoável, é necessário um número muito grande de iterações, tornando o custo computacional evidente.

## Procedimentos de Execução

1. **Compilação:** O código `pi_accuracy.c` deve ser compilado com a biblioteca matemática (`-lm`) para ter acesso ao valor de referência `M_PI`.

   ```bash
   gcc pi_accuracy.c -o pi_accuracy -lm
````

2.  **Execução:** O programa não requer argumentos e executará uma série de testes com um número crescente de iterações.

    ```bash
    ./pi_accuracy
    ```

## Resultados Esperados

A execução do programa produzirá uma tabela que mostra, para cada número de iterações, o valor de π calculado, o erro absoluto em relação ao valor real e o tempo de execução.

| Iterações | Pi Calculado | Erro Absoluto | Tempo (segundos) |
| :--- | :--- | :--- | :--- |
| 10 | 3.041839618929403240 | 0.099753034660390140 | 0.000000000 |
| 100 | 3.131592903558553730 | 0.009999749931239650 | 0.000000000 |
| 1,000 | 3.140592653839794020 | 0.000999999749999360 | 0.000000000 |
| 1,000,000 | 3.141591653589774300 | 0.000001000000018990 | 0.003000000 |
| 100,000,000 | 3.141592643589326000 | 0.000000010000467290 | 0.280000000 |
| 1,000,000,000 | 3.141592652588050400 | 0.000000001001742890 | 2.850000000 |

*(Nota: Os tempos de execução podem variar significativamente dependendo do hardware.)*

## Análise e Reflexão: O Trade-off no Mundo Real

A tabela de resultados ilustra perfeitamente o conceito:

  * **Aumento da Acurácia:** A cada ordem de magnitude no número de iterações, o erro absoluto diminui, e o valor calculado de π se aproxima cada vez mais do valor real.

  * **Aumento do Custo:** Ao mesmo tempo, o tempo de execução cresce de forma aproximadamente linear com o número de iterações. Para obter um dígito a mais de precisão, pagamos um preço computacional significativamente maior.

Este comportamento não é exclusivo do cálculo de π. Ele é um padrão universal em computação de alto desempenho, com paralelos diretos em áreas críticas:

### 1\. Simulações Físicas e de Engenharia

Em domínios como **previsão do tempo, dinâmica de fluidos computacional (CFD) ou simulações de elementos finitos**, a precisão do resultado depende da "resolução" da simulação (o tamanho da malha ou o passo de tempo).

  * **Baixo Custo / Baixa Precisão:** Uma simulação com uma malha grosseira é rápida, mas pode não capturar turbulências importantes ou pontos de estresse num material, levando a conclusões erradas.

  * **Alto Custo / Alta Precisão:** Refinar a malha aumenta drasticamente a precisão, mas o custo computacional pode crescer de forma cúbica ou pior. Simulações de alta fidelidade exigem supercomputadores e semanas de processamento.

### 2\. Inteligência Artificial e Machine Learning

O treino de modelos de **Deep Learning** é um processo iterativo onde o modelo ajusta seus pesos para minimizar uma função de erro (loss).

  * **Baixo Custo / Baixa Precisão:** Treinar por poucas épocas é rápido, mas resulta num modelo "sub-treinado" (*underfit*), que não aprendeu os padrões nos dados e terá um desempenho pobre.

  * **Alto Custo / Alta Precisão:** Treinar por muitas épocas reduz o erro, mas exige dias ou semanas de processamento em hardware especializado (GPUs/TPUs) e consome uma quantidade massiva de energia. O desafio é encontrar o ponto ótimo antes que o modelo comece a "decorar" os dados (*overfitting*).

### 3\. Renderização Gráfica e Ray Tracing

Na geração de imagens fotorrealistas, a qualidade da imagem (ausência de ruído, reflexos precisos) depende do número de raios de luz simulados por pixel.

  * **Baixo Custo / Baixa Qualidade:** Poucos raios por pixel resultam numa imagem "granulada" e com artefatos.

  * **Alto Custo / Alta Qualidade:** Aumentar o número de raios produz uma imagem limpa e realista, mas o tempo de renderização pode passar de segundos para horas por frame.

### Conclusão do Especialista em Programação Paralela

O problema do cálculo de π, assim como os exemplos citados, é um problema **"compute-bound"** (limitado pelo processamento). A boa notícia é que muitas dessas tarefas são também **"embaraçosamente paralelas"**. O cálculo de cada termo da série, a atualização de cada célula numa simulação, ou o processamento de diferentes lotes de dados em IA podem ser feitos de forma independente.

É aqui que a **programação paralela** se torna a solução. Ao dividir o trabalho (as iterações) entre múltiplos núcleos de CPU ou unidades de GPU, podemos alcançar a precisão desejada num tempo de execução muito menor. O desafio, portanto, não é apenas encontrar um algoritmo que convirja, mas também estruturá-lo de forma que ele possa ser eficientemente paralelizado para gerir o inevitável trade-off entre custo e precisão.

```
```