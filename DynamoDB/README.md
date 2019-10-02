# Armazenamento de dados no DynamoDB

As regras DynamoDB permitem que você obtenha informações de uma mensagem MQTT recebida e anote-a em uma tabela do DynamoDB.

Neste tutorial vamos criar e configurar uma **Regra do DynamoDB** 

Na Aba Serviços procure por **IOT CORE**

![serviços](https://github.com/FelipeNasci/AWSTutorials/blob/master/Registro%20do%20Device%20(Thing)/img/servicos.jpg?raw=true)

Entre no menu **Gerenciar** e escolha a opção **Agir** em seguida _**Criar uma regra**_

Aqui criaremos uma regra para avaliar mensagens enviadas por suas coisas, e determinar o que fazer quando uma mensagem é recebida (por exemplo, gravar os dados em uma tabela do DynamoDB ou invocar uma função Lambda).


* Nome: `GreenHouseRule`

* Descrição: `A DynamoDB rule for a GreenHouse`

* Instrução da consulta da regra: `SELECT * FROM 'my/greenhouse'`

* Adicionar Ação

* 4 - Ecolha `Inserir uma mensagem em uma tabela do DynamoDB` e em seguida `configurar`.

![acao](https://github.com/FelipeNasci/AWSTutorials/blob/master/DynamoDB/img/inserirMenssagem.JPG?raw=true)

Ao clicar em 'configurar' criaremos nossa primeira tabela.

* 5 Criar tabela

![inicioCriarTabela](https://github.com/FelipeNasci/AWSTutorials/blob/master/DynamoDB/img/criarTabela.JPG?raw=true)

* 6 - Nome da tabela

```

GreenHouseTable

```

* 7 - Chave primária

```

Chave de partição: Row
Chave de classificação: PositionRow

```
![defTabela](https://github.com/FelipeNasci/AWSTutorials/blob/master/DynamoDB/img/DefinicaoTabela.JPG?raw=true)

Ao término, será exibida a janela a seguir

![tabela](https://github.com/FelipeNasci/AWSTutorials/blob/master/DynamoDB/img/TabelaCriada.JPG?raw=true)

Continuando, em nossa regra:

 - escolheremos a tabela criada
 - Definiremos a variável para a partição `${row}`
 - Definiremos a variável para a classificação `${pos}`
 - Criaremos a ação, criando uma função

![table](https://github.com/FelipeNasci/AWSTutorials/blob/master/DynamoDB/img/aposCriarTabela.JPG?raw=true)

Para finalizar, selecione a opção `adicionar ação`

![ok](https://github.com/FelipeNasci/AWSTutorials/blob/master/DynamoDB/img/ok.JPG?raw=true)

A regra deve estar semelhante a imagem a seguir:

![]()