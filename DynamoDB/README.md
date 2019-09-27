# Armazenamento de dados no DynamoDB

As regras DynamoDB permitem que você obtenha informações de uma mensagem MQTT recebida e anote-a em uma tabela do DynamoDB.

Neste tutorial vamos criar e configurar uma **Regra do DynamoDB** 

Na Aba Serviços procure por **IOT CORE**

![serviços](https://github.com/FelipeNasci/AWSTutorials/blob/master/Registro%20do%20Device%20(Thing)/img/servicos.jpg?raw=true)

Entre no menu **Gerenciar** e escolha a opção **Agir** em seguida _**Criar uma regra**_

Aqui criaremos uma regra para avaliar mensagens enviadas por suas coisas, e determinar o que fazer quando uma mensagem é recebida (por exemplo, gravar os dados em uma tabela do DynamoDB ou invocar uma função Lambda).


* 1 - Insira um nome para sua regra: 

```
GreenHouseRule
```

* 2 - Descreva a ação desta nova regra: 

```
A DynamoDB rule for a GreenHouse
````

Em Rule query statement (Instrução da consulta da regra), escolha a versão mais recente da lista Using SQL version (Versão do SQL a ser usada). Para Rule query statement (Instrução de consulta da regra), insira:

```
SELECT * FROM 'my/greenhouse'
```

* 3 - Adicionar Ação

* 4 - Ecolha `Inserir uma mensagem em uma tabela do DynamoDB` e em seguida `configurar`.

Ao clicar em 'configurar' criaremo nossa primeira tabela.

* 5 Criar tabela

* 6 - Nome da tabela

```
GreenHouseTable
```

* 7 - Chave primária

```
Chave de partição: Row
Chave de classificação: PositionRow
```

Ao término, será exibida a janela a seguir


Continuando, em nossa regra:

 - escolheremos a tabela criada
 - Definiremos a variável para a partição `${row}`
 - Definiremos a variável para a classificação `${pos}`
 - Criaremos a ação, criando uma função

 A imagem a seguir demonstra qual deveria ser o estado até o momento.


 porém em minha conta AWS não tenho permissões para continuar, sendo esta a notificação que me aparece.

 





## Referências

Este tutorial está baseado no [AWS IoT Guia do desenvolvedor](https://docs.aws.amazon.com/pt_br/iot/latest/developerguide/register-device.html)