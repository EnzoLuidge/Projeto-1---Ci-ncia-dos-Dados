# Projeto-1---Cdados

***Introdução***

Um classificador Naive-Bayes é um algoritmo que é capaz de classificar informações em diferentes categorias baseada nas probabilidades dos parâmetros individuais de cada informação. Esse algoritmo tem aplicações famosas em classificações de palavras ou frases (admitindo-se que as palavras ocorrem de maneira independente na frase), mas suas aplicações podem abrangir outras áreas, como até a categorização de falhas ocorridas em robôs manipuladores (WANKE, 2014).

Este projeto visou criar um classificador Naive-Bayes para classificar tweets relacionados à série de RPG Ordem Paranormal: Calamidade, que ocorre na plataforma Twitch aos sábados. A classificação foi feita considerando como "relevante" tweets que contêm opiniões, reclamações e apontamentos sobre a série, e "irrelevante" para todo o restante.


***Construção do classificador***

Para iniciar a construção do classificador, foi adquirida uma base de dados com 600 tweets manualmente classificados, dividindo-a em uma planilha para o treinamento do classificador, com 400 tweets, e uma planilha para os testes de performance, contendo 200 tweets. Para facilitar o tratamento de dados, foi construída uma função para limpar os tweets, transformando emojis em palavras, deixando todas as letras em minúsculo, retirando sinais de pontuação, excluindo nomes de perfil, retirando links, desconsiderando stopwords etc.

Com os tweets limpos e considerando apenas os da base de treinamento, foram adquiridos três conjuntos de palavras: o conjunto contendo todas as palavras, o conjunto de todas as palavras apenas dos tweets manualmente classificados como relevantes e o conjunto de palavras dos tweets classificados como irrelevantes. Utilizando esses três conjuntos, foi possível adquirir a probabilidade de uma palavra ser relevante e a probabilidade de uma palavra ser irrelevante.

O próximo passo foi, então, fazer uma função para o classificador onde, para cada tweet, seria analisada o quão relevante e irrelevante cada palavra do tweet seria com base na sua frequência relativa no conjunto de palavras relevantes e irrelevantes, respectivamente, multiplicando essas probabilidades entre si para se obter a probabilidade de a frase aparecer entre os relevantes ou irrelevantes (admitindo-se independência entre as palavras). Para evitar zerar a probabilidade total do tweet no caso de uma palavra inédita, foi utilizada uma suavização Laplace em cada probabilidade relativa. 

Como última etapa do classificador, foi multiplicada a probabilidade da frase aparecer entre os relevantes com a probabilidade geral de uma palavra ser relevante e o mesmo processo para os irrelevantes, resultando na probabilidade do tweet ser relevante e na probabilidade do tweet ser irrelevante. São comparadas ambas as duas probabilidades e, dependendo de qual a maior, o classificador classifica o tweet como relevantes ou irrelevante.


***Resultados***

Testando, então, o classificador na base de testes, pode-se perceber uma acurácia (soma da porcentagem de verdadeiros positivos com verdadeiros negativos) de 75,5% para os tweets analisados para a distribuição utilizada. Porém, como a distribuição de tweets entre base de testes e treinamento pode impactar na acurácia do classificador, foram testadas 100 combinações diferentes de tweets com as mesmas proporções iniciais entre treinamento e base, salvando a acurácia de cada distribuição em uma lista. Analisando os resultados, o acerto em média do classificador foi de 69,75%, para as 100 distribuições.


***Conclusões***

Considerando que o classificador em média tem uma performance razoavelmente boa (próxima de 70%), pode-se afirmar que o categorizador poderia ser uma ferramenta útil para a filtragem de tweets com opiniões sobre a série, especialmente considerando o quão raro pode ser encontrar um tweet relevante em meio a muitos irrelevantes.

Para melhorar sua performance, uma possível medida a ser tomada seria de adquirir mais tweets manualmente classificados para a base de treinamento, aumentando o repertório do algoritmo para calcular as probabilidades. Uma ideia que pederia surgir para facilitar esse processo de aprimoração do projeto seria de deixar o próprio programa classificar os tweets adicionais, mas essa *NÃO* seria uma ideia válida para aprimorar sua performance, uma vez que o classificador apenas iria se alimentar com os próprios erros, ao invés de adquirir mais parâmetros para os cálculos das probabilidades. 
