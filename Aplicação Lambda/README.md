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

A seguir, iremos inserir

 - Nome da função Lambda: `myLambdaFunction`

 - Função de execução: `Criar uma função a partir da política da AWS templates`

 - Nome da nova função: `myIotLambdaFunction`

 - Modelos de Política: `Política de publicação do Amazon SNS`

 - Criar função

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

#### Importante
```

A variável TopicArn deve ter seu valor substituído pelo arn do tópico SNS já criado.

```

Salve o código, a seguir iremos configurar um evento de teste.

 - Configurar Evento de teste
 - Criar novo Evento de teste
 - Event name: `myEventTest`
 - Insira o código a seguir

```python
{ 
  "message" : "Hello, world"
}
```

	- Criar

Em seguida teste a aplicação, o estado deve ser semelhante a imagem abaixo.


#### Criando uma regra

Ainda no AWS Iot

```

Agir -> Criar

```

 - Nome: `myLambdaRule`

 - Instrução de consulta da regra: `SELECT * FROM "my/lambda/topic"`

 - Adicione uma ação: `Enviar uma mensagem para uma aplicação Lambda`

 - Adicione uma ação de erro: `Publicar novamente mensagens em um tópico do AWS Iot`


#### Testes

No cliente do MQTT, em Tópico de inscrição, insira `lambda/error` e, depois, selecione Inscrever-se no tópico.

Em Publicar, insira `my/lambda/topic` e, depois, escolha Publicar em um tópico para publicar a mensagem JSON padrão.

A mensagem deverá ir para um email previamente cadastrado como assinante.


## Referências

Este tutorial está baseado no [AWS IoT Guia do desenvolvedor](https://docs.aws.amazon.com/pt_br/iot/latest/developerguide/register-device.html)