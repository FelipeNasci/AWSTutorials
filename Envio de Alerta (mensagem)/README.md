# Envio de Alerta (mensagem)


Uma regra do Amazon SNS permite o envio de mensagens via email, sms, ou json a partir de uma ['thing'](https://github.com/FelipeNasci/AWSTutorials/tree/master/Registro%20do%20Device%20(Thing)#registro-do-device-thing).

Para criar uma regra com uma ação do SNS vá em:

```

Serviços -> Iot Core -> Agir -> criar uma regra

```

Nesta janela, você irá definir:

- Nome: `MySNSRule`

- Descrição: `A more complex SNS rule`

- Instrução da consulta da regra: `SELECT *, topic(3) as thing FROM '$aws/things/+/shadow/update/accepted'`

Sua tela deverá estar semelhante com a imagem a seguir:

![]()


Vamos definir uma ação que será executada quando a regra corresponder a uma mensagem de entrada. Estas ações podem ser por exemplo, um armazenamento em um banco de dados, execução de funções em nuvem etc.

- Click em: `Adicionar ação`

- Selecione: `Enviar uma mensagem como uma notificação por push SNS`

- Crie um destino do SNS: `MySNSTopic`

- Formato de mensagens: `RAW`

- Crie uma função: `MySNSRole`

Pronto! Nossa regra SNS está criada.

### Testes

#### Cadastro do endpoint

Nesta sessão vamos realizar um teste de envio de mensagens para uma conta de email. Siga os passos:

Primeiro iremos vincular um assinante ao nosso TópicoSNS:

```

Serviços -> Digite SNS no campo de pesquisa -> Simple Notification Service

```

No Amazon SNS:

```

Tópicos -> MySNSTopic

```


```

 Assinaturas -> Criar assinatura

```


Escolha o protocolo através do qual a mensagem será enviada e o endpoint (em nosso caso, o email que receberá as mensagens).

- Protocolo: `Email`

- Endpoint: `email@mail.com`


Caso tenha escolhido uma conta de email, você deverá receber uma confirmação em sua caixa de entrada.


#### Envio da mensagem

Agora podemos ir na opção `Publicar Mensagem` que está contida no submenu `Tópicos` , escrever o assunto e a mensagem e pronto"

Verifique em sua caixa de entrada.





