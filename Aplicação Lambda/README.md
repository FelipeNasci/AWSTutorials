# Aplicação Lambda

Este tutorial pressupõe que há um [tópico SNS](https://github.com/FelipeNasci/AWSTutorials/tree/master/Envio%20de%20Alerta%20(mensagem)#envio-de-alerta-mensagem) já criado.

Criaremos uma função Lambda que publica uma mensagem no tópico do Amazon SNS. Também criaremos uma regra Lambda que solicita a função do Lambda, transmitindo alguns dados da mensagem MQTT que acionou a regra.

Começamos por:

```

Serviços -> Pesquise por "Lambda" -> AWS Lambda

```

* No console do AWS Lambda, escolha Criar função.

 - selecione `Usar um esquema`. 
 
 - No campo de Esquemas.

 - Insira `hello-world` e pressione Enter

 - Escolha o esquema `hello-world-python` e, depois, escolha a opção `Configurar`.


![esquema](https://github.com/FelipeNasci/AWSTutorials/blob/master/Aplica%C3%A7%C3%A3o%20Lambda/img/Slide1.PNG?raw=true)


A seguir, iremos inserir

 - Nome da função Lambda: `myLambdaFunction`

 - Função de execução: `Criar uma função a partir da política da AWS templates`

 - Nome da nova função: `myIotLambdaFunction`

 - Modelos de Política: `Política de publicação do Amazon SNS`

 - Criar função

![funcao](https://github.com/FelipeNasci/AWSTutorials/blob/master/Aplica%C3%A7%C3%A3o%20Lambda/img/Slide2.PNG?raw=true)

Substitua o código existente por este

```python

from __future__ import print_function
  
import json
import boto3
  
print('Loading function')
  
def lambda_handler(event, context):
  
    # Parse the JSON message 
    eventText = json.dumps(event)
  
    # Print the parsed JSON message to the console; you can view this text in the Monitoring tab in the Lambda console or in the CloudWatch Logs console
    print('Received event: ', eventText)
  
    # Create an SNS client
    sns = boto3.client('sns')
  
    # Publish a message to the specified topic
    response = sns.publish (
      TopicArn = 'arn:aws:iam::123456789012:role/service-role/myLambdaFunctionRole',
      Message = eventText
    )
  
    print(response)

```

![code](https://github.com/FelipeNasci/AWSTutorials/blob/master/Aplica%C3%A7%C3%A3o%20Lambda/img/Slide4.PNG?raw=true)

#### Importante


**_A variável TopicArn deve ter seu valor substituído pelo arn do tópico SNS já criado_.**


Siga os passos:

```

Serviços -> SNS

```

![console](https://github.com/FelipeNasci/AWSTutorials/blob/master/Aplica%C3%A7%C3%A3o%20Lambda/img/Slide5.PNG?raw=true)


```

Tópicos -> MySNSTopic

```

copie o `arn` e substitua o valor da variável `TopicArn`

![arn](https://github.com/FelipeNasci/AWSTutorials/blob/master/Aplica%C3%A7%C3%A3o%20Lambda/img/Slide8.PNG?raw=true)

![tocpicArn](https://github.com/FelipeNasci/AWSTutorials/blob/master/Aplica%C3%A7%C3%A3o%20Lambda/img/Slide8.PNG?raw=true)


Salve o código. A seguir iremos configurar um evento de teste.

![EventTest](https://github.com/FelipeNasci/AWSTutorials/blob/master/Aplica%C3%A7%C3%A3o%20Lambda/img/Slide9.PNG?raw=true)

 - Configurar Evento de teste
 - Criar novo Evento de teste
 - Event name: `myEventTest`
 - Insira o código a seguir

```python
{ 
  "message" : "Hello, world"
}
```

![evento](https://github.com/FelipeNasci/AWSTutorials/blob/master/Aplica%C3%A7%C3%A3o%20Lambda/img/Slide10.PNG?raw=true)

	- Criar

Em seguida teste a aplicação, o estado deve ser semelhante a imagem abaixo.

![ok](https://github.com/FelipeNasci/AWSTutorials/blob/master/Aplica%C3%A7%C3%A3o%20Lambda/img/Slide11.PNG?raw=true)

#### Criando uma regra

No AWS Iot

![awsiot](https://github.com/FelipeNasci/AWSTutorials/blob/master/Aplica%C3%A7%C3%A3o%20Lambda/img/Slide12.PNG?raw=true)

```

Agir -> Criar

```

 - Nome: `myLambdaRule`

 - Instrução de consulta da regra: `SELECT * FROM "my/lambda/topic"`

 - Adicione uma ação: `Enviar uma mensagem para uma aplicação Lambda`

 - Adicione uma ação de erro: `Publicar novamente mensagens em um tópico do AWS Iot`


![acao](https://github.com/FelipeNasci/AWSTutorials/blob/master/Aplica%C3%A7%C3%A3o%20Lambda/img/Slide14.PNG?raw=true)

#### Testes

No cliente do MQTT, em Tópico de inscrição, insira `lambda/error` e, depois, selecione Inscrever-se no tópico.

![lambdaerro](https://github.com/FelipeNasci/AWSTutorials/blob/master/Aplica%C3%A7%C3%A3o%20Lambda/img/Slide15.PNG?raw=true)

Em Publicar, insira `my/lambda/topic` e, depois, escolha Publicar em um tópico para publicar a mensagem JSON padrão.


![mylambdatopic](https://github.com/FelipeNasci/AWSTutorials/blob/master/Aplica%C3%A7%C3%A3o%20Lambda/img/Slide16.PNG?raw=true)

A mensagem deverá ir para um email previamente cadastrado como assinante.


## Referências

Este tutorial está baseado no [AWS IoT Guia do desenvolvedor](https://docs.aws.amazon.com/pt_br/iot/latest/developerguide/register-device.html)