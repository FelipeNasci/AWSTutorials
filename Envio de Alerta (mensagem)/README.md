# Envio de Alerta (mensagem)


Uma regra do Amazon SNS permite o envio de mensagens via email, sms, ou json a partir de uma ['thing'](https://github.com/FelipeNasci/AWSTutorials/tree/master/Registro%20do%20Device%20(Thing)#registro-do-device-thing).

Para criar uma regra com uma ação do SNS vá em:

```

Serviços -> Iot Core -> Agir -> criar uma regra

```

![criarRegra](https://github.com/FelipeNasci/AWSTutorials/blob/master/Envio%20de%20Alerta%20(mensagem)/img/Slide1.JPG?raw=true)

Nesta janela, você irá definir:

- Nome: `MySNSRule`

- Descrição: `A more complex SNS rule`

- Instrução da consulta da regra: `SELECT *, topic(3) as thing FROM '$aws/things/+/shadow/update/accepted'`

Sua tela deverá estar semelhante com a imagem a seguir:

![regra](https://github.com/FelipeNasci/AWSTutorials/blob/master/Envio%20de%20Alerta%20(mensagem)/img/Slide2.JPG?raw=true)

Vamos definir uma ação que será executada quando a regra corresponder a uma mensagem de entrada. Estas ações podem ser por exemplo, um armazenamento em um banco de dados, execução de funções em nuvem etc.

- Click em: `Adicionar ação`

![addAcao](https://github.com/FelipeNasci/AWSTutorials/blob/master/Envio%20de%20Alerta%20(mensagem)/img/Slide3.JPG?raw=true)

- Selecione: `Enviar uma mensagem como uma notificação por push SNS`

![acao](https://github.com/FelipeNasci/AWSTutorials/blob/master/Envio%20de%20Alerta%20(mensagem)/img/Slide4.JPG?raw=true)

- Crie um destino do SNS: `MySNSTopic`

- Formato de mensagens: `RAW`

- Crie uma função: `MySNSRole`

![configAcao](https://github.com/FelipeNasci/AWSTutorials/blob/master/Envio%20de%20Alerta%20(mensagem)/img/Slide5.JPG?raw=true)

Pronto! Nossa regra SNS está criada.

![ok](https://github.com/FelipeNasci/AWSTutorials/blob/master/Envio%20de%20Alerta%20(mensagem)/img/Slide6.JPG?raw=true)

### Testes

#### Cadastro do endpoint

Nesta sessão vamos realizar um teste de envio de mensagens para uma conta de email. Siga os passos:

Primeiro iremos vincular um assinante ao nosso TópicoSNS:

```

Serviços -> Digite SNS no campo de pesquisa -> Simple Notification Service

```

![sns](https://github.com/FelipeNasci/AWSTutorials/blob/master/Envio%20de%20Alerta%20(mensagem)/img/Slide7.JPG?raw=true)

No Amazon SNS:

```

Tópicos -> MySNSTopic

```

![topicos](https://github.com/FelipeNasci/AWSTutorials/blob/master/Envio%20de%20Alerta%20(mensagem)/img/Slide8.JPG?raw=true)

```

 Assinaturas -> Criar assinatura

```
![criarAssinatura](https://github.com/FelipeNasci/AWSTutorials/blob/master/Envio%20de%20Alerta%20(mensagem)/img/Slide9.JPG?raw=true)

Escolha o protocolo através do qual a mensagem será enviada e o endpoint (em nosso caso, o email que receberá as mensagens).

- Protocolo: `Email`

- Endpoint: `email@mail.com`


![criado](https://github.com/FelipeNasci/AWSTutorials/blob/master/Envio%20de%20Alerta%20(mensagem)/img/Slide10.JPG?raw=true)

Caso tenha escolhido uma conta de email, você deverá receber uma confirmação em sua caixa de entrada.

![confirmacao](https://github.com/FelipeNasci/AWSTutorials/blob/master/Envio%20de%20Alerta%20(mensagem)/img/Slide12.JPG?raw=true)

#### Envio da mensagem

Agora podemos ir na opção `Publicar Mensagem` que está contida no submenu `Tópicos` , escrever o assunto e a mensagem e pronto"

![ok](https://github.com/FelipeNasci/AWSTutorials/blob/master/Envio%20de%20Alerta%20(mensagem)/img/Slide13.JPG?raw=true)

![](https://github.com/FelipeNasci/AWSTutorials/blob/master/Envio%20de%20Alerta%20(mensagem)/img/Slide14.JPG?raw=true)

Verifique em sua caixa de entrada.

![resultado](https://github.com/FelipeNasci/AWSTutorials/blob/master/Envio%20de%20Alerta%20(mensagem)/img/Slide16.JPG?raw=true)

# Referências

Estes tutoriais estão baseados no [AWS IoT Guia do desenvolvedor](https://docs.aws.amazon.com/pt_br/iot/latest/developerguide/register-device.html)