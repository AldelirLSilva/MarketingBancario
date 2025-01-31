# O que influencia no sucesso da conversão de uma campanha?

### É isso que irei descobrir e apresentar aqui neste artigo!

![](https://cdn-images-1.medium.com/max/800/1*cbZu5IQKnVJgF3V19u1MOQ.jpeg)

Apresentarei uma análise detalhada onde o objetivo é encontrar quais variáveis influenciam a conversão de clientes em uma campanha bancária.

### Vem comigo e acompanha o raciocínio!

Para essa análise utilizei dados do Kaggle, onde o dataset possui dados de uma campanha de marketing telefônico de uma instituição bancária portuguesa onde o objetivo foi oferecer o **depósito a prazo**.

_“O depósito a prazo é um produto financeiro no qual você empresta dinheiro para uma instituição financeira, como o Sicredi, e no fim de um prazo previamente acordado você recebe o pagamento desse valor com juros. Essa é a ideia básica de muitos produtos oferecidos por bancos, corretoras e instituições de crédito.  
_**_Depósitos a prazo são uma importante fonte de renda para um banco._**_  
As campanhas de marketing telefônico ainda são uma das formas mais eficazes de alcançar as pessoas._

_No entanto, elas exigem um grande investimento, pois grandes call centers são contratados para realmente executar essas campanhas. Portanto, é crucial identificar os clientes com maior probabilidade de conversão com antecedência para que eles possam ser especificamente direcionados por meio de chamada.”_

[https://www.kaggle.com/datasets/prakharrathi25/banking-dataset-marketing-targets?select=train.csv](https://www.kaggle.com/datasets/prakharrathi25/banking-dataset-marketing-targets?select=train.csv)


## Análise Exploratória dos Dados

Aqui está uma breve descrição dos dados que o kaggle disponibilizou:

### Dados pessoais
`age`: (*numérico*)  
`job`: tipo de emprego (categórico: *“admin”, ”unknown”, ”unemployed”, ”management”, ”housemaid”, ”entrepreneur”, ”student”, “blue-collar”, ”self-employed”, ”retired”, ”technician”, ”services”*)  
`marital`: estado civil (_categórico: “married”, ”divorced”, ”single”; nota: “divorced” significa divorciado ou viúvo_)  
`education` (_categórico: “unknown”,”secondary”,”primary”,”tertiary”_)  
`default`: tem crédito em inadimplência? (_binário: “yes”, “no”_)  
`balance`: saldo médio anual, em euros (_numérico_)  
`housing`: tem empréstimo imobiliário? (_binário: “yes”, “no”_)  
`loan`: tem empréstimo pessoal? (_binário: “yes”, “no”_)  
`contact`: tipo de comunicação de contato (_categórico: “unknown”,”telephone”,”cellular”_)

### Campanha Atual
`day`: último dia de contato do mês (_numérico_)  
`month`: último mês de contato do ano (_categórico: “jan”, “feb”, “mar”, …, “nov”, “dec”)_  
`duration`: duração do último contato, em segundos (_numérico_)  
`campaign`: número de contatos realizados durante esta campanha e para este cliente (_numérico, inclui o último contato_)  
`y`: o cliente subscreveu um depósito a prazo? (_binário: “yes”, “no”_)

### Campanha Anterior
`pdays`: número de dias que se passaram após o cliente ter sido contatado pela última vez de uma campanha anterior (_numérico, -1 significa que o cliente não foi contatado anteriormente_)  
`previous`: número de contatos realizados antes desta campanha e para este cliente (_numérico_)  
`poutcome`: resultado da campanha de marketing anterior (_categórico: “unknown”,”other”,”failure”,”success”_)

Temos quase total entendimento dos dados, falta só **visualizá-los**!

![](https://cdn-images-1.medium.com/max/1200/1*utsd0IWsuZbo1UqhPGYeVg.png)

Para facilitar vou traduzir todas as colunas e verificar os tipos de dados:

![](https://cdn-images-1.medium.com/max/800/1*EBj1WdqVJKaOK2KQNiAV0w.png)

**Não há valores nulos!** Agora como meu objetivo aqui é descobrir quais variáveis possuem maior relação com o sucesso da campanha, irei verificar a correlação de todas as variáveis com a variável alvo (`Conversão`):

![](https://cdn-images-1.medium.com/max/800/1*PhjSSLV40Q2tE38CyH88cw.png)

Claramente entre as variáveis quantitativas a `Duracao`é a que tem maior correlação com a conversão, indicando que quanto maior a duração da chamada maior a chance de conversão, porém não é uma correlação forte.

Agora vamos correlacionar as variáveis **qualitativas**:

![](https://cdn-images-1.medium.com/max/800/1*eARxq-ngg7dYEvqkHHy8Vw.png)
![](https://cdn-images-1.medium.com/max/800/1*L3UBzs2EM4sAddj1C9B85A.png)
![](https://cdn-images-1.medium.com/max/800/1*RwXYtrVTXMvB17vqmCOLBA.png)
![](https://cdn-images-1.medium.com/max/800/1*_kjhZr4v9LVmqdfgGFd-0w.png)
![](https://cdn-images-1.medium.com/max/800/1*QPi4LriBjMyYieZmRAvYmg.png)
![](https://cdn-images-1.medium.com/max/800/1*h4Ped4v3oMAvADLeRlJMuw.png)
![](https://cdn-images-1.medium.com/max/800/1*sYKCjy6uB8LVON5cM_p24g.png)
![](https://cdn-images-1.medium.com/max/800/1*mofiliCC1Sd1Mmw76DF9QQ.png)

Com toda certeza posso dizer que o **sucesso da campanha anterior** tem relação com o **sucesso da campanha atual**, quase que chega a uma correlação forte, diferente das demais.

Só que ainda faltam 2 variáveis para verificar: `Dia`e  `Mes`

![](https://cdn-images-1.medium.com/max/800/1*pH-5IXEh6tOeFlPQXC2SHg.png)
![](https://cdn-images-1.medium.com/max/800/1*_tF4i3h_YLlH9bEBLNLX0A.png)

Mais subcategorias que se destacam com seu alto nível de correlação! Em específico: _março, dezembro, setembro_ e _outubro_.

### **Inicialmente posso concluir que essas 3 variáveis possuem certa influência no sucesso da campanha:**

`Resuldado_camp_ant`= success;  
`Mes`= _mar, dec, sep e oct;  
`Duracao.`

### Porém…

Para poder afirmar com exatidão terei que executar um teste estatístico!  
E para saber qual teste usar irei explorar essas 3 variáveis mais a fundo.

Primeiro a variável `Duracao`:

![](https://cdn-images-1.medium.com/max/800/1*QaVX5aUkAA9l0vQV_9N7Rw.png)

Temos 2 pontos a destacar sobre essa variável! Ela possui muitos outliers e consequentemente sua distribuição é assimétrica, isso pode resultar em um problema a depender do teste estatístico que será usado.

Agora a variável `Resuldado_camp_ant`:

![](https://cdn-images-1.medium.com/max/800/1*rwZTV645uC_gPPTCvpCxBQ.png)

Podemos notar que a categoria _unknown_ possui extrema quantidade provocando o desbalanceamento da variavel e no teste de correlação ela foi a de menor taxa, então utilizarei ela como nível de referência para o modelo estatístico e a _success_ teve mais convertidos do que não convertidos, então podemos considerá-la valiosa.

Agora a variável `Mes`:

![](https://cdn-images-1.medium.com/max/800/1*9C3ZHWCt2aEkTUXAUYUSBA.png)

Podemos notar o mesmo padrão da variável anterior, o mês com menor correlação é _may_,  e contem  muitos não convertidos e pouquíssimos convertidos e os meses _mar, dec, sep e oct_ vemos que estão praticamente balanceados comparando entre convertidos e não convertidos.

Para finalizar vamos ver como está a distribuição da variável `Conversao`:

![](https://cdn-images-1.medium.com/max/800/1*KZ7mkMFWOtgJZRQ4X0gL5g.png)

A variável está desbalanceada, será necessário balancear para usá-la no modelo.


## **Agora é hora da verdade! Será que essas variáveis realmente influenciam na conversão de um cliente?**

Nessa ultima etapa da análise eu trouxe o melhor teste estatístico! O teste que resultou em um modelo de `92%` de acurácia.

### **Árvore de decisão**!

`A árvore de decisão apresenta diversas vantagens!`

_“Mais robusta contra outliers, além de ser flexível para modelar relações não lineares e detectar interações automaticamente. Outro ponto forte é a facilidade em trabalhar diretamente com variáveis categóricas e contínuas, sem necessidade de transformações como na regressão logística._

_Além disso, as árvores de decisão não dependem de pressupostos estatísticos rígidos, como linearidade ou normalidade, tornando-as mais versáteis em diferentes cenários. A interpretabilidade também é um destaque, já que o modelo pode ser visualizado de forma intuitiva em diagramas.”_

Para validar o modelo, os testes que precisarei fazer é o de taxa de **Overfitting** e o de validação cruzada **K-fold**!

#### Vamos iniciar!

Primeiro o treinamento do modelo com a biblioteca **sklearn.tree** e o comando **DecisionTreeClassifier().**

![](https://cdn-images-1.medium.com/max/800/1*hFnKa7FJ_sAX-EejFz-L5A.png)

E agora vamos ao resultado das métricas de classificação:

#### Teste de Overfitting

O teste de overfitting foca especificamente na diferença de desempenho entre treino e teste para determinar se o modelo está superajustado.

![](https://cdn-images-1.medium.com/max/800/1*Dt0D-2cRE3N06nRGGaMd7g.png)

-   O Overfitting de 5% é muito baixo, demonstrando que não teremos uma influência negativa no modelo.

#### Validação cruzada k-fold

A validação cruzada k-fold é um método abrangente para verificar a robustez e a generalização do modelo.

![](https://cdn-images-1.medium.com/max/800/1*e2vaQLRkBROBN6vkgKgOWA.png)

-   O teste trouxe um valor de desvio extremamente baixo, demonstrando novamente que o modelo é estável, entregando resultados semelhantes em diferentes divisões dos dados.

A árvore de decisão apresenta um ótimo desempenho geral, com métricas altas de acurácia, precisão, recall e F1-Score (todas em torno de **92%**).

## Conclusão

- As 3 variáveis usadas influenciam positivamente no sucesso da conversão!
- O teste estatistico demonstrou que podemos confiar no resultado da análise exploratória.

### Minhas recomendações para o banco!

-   `Aumentar o tempo médio de interação com clientes`: os vendedores devem estar preparados para conduzir o cliente até o sucesso da conversão.
-   `Focar as campanhas nos meses com alta conversão`: _março, dezembro, setembro_ e _outubro_.
-   `Criar estratégias de retenção para clientes que tiveram campanhas anteriores bem-sucedidas.`

### Isso por si só aumentaria consideravelmente os futuros resultados na execução dessa campanha.

Se as variáveis `Duracao` e `Mes` não fossem geradas pela campanha atual, eu poderia usar esse modelo para prever quais clientes do banco têm potencial de conversão com uma taxa de assertividade de `92%`.

Como não é possível agora, em um futuro artigo, pretendo utilizar uma abordagem diferente para identificar quais outras variáveis influenciam a conversão, podendo assim prever os clientes que irão converter.

## Fim
