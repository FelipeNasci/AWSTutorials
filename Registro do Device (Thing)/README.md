# Registro do Device (Thing)

**Coisa** é uma representação de um dispositivo específico ou entidade lógica. Ela pode ser um dispositivo físico ou sensor (por exemplo, uma lâmpada ou um interruptor em uma parede). Ela também pode ser uma entidade lógica, como uma instância de um aplicativo, ou uma entidade física que não se conecte à AWS IoT, mas esteja relacionada a outros dispositivos que se conectam (por exemplo, um carro que tenha sensores do motor ou um painel de controle).

Neste tutorial vamos criar e configurar uma **'thing'** (coisa)

Na Aba Serviços procure por **IOT CORE**

![serviços](https://github.com/FelipeNasci/AWSTutorials/blob/master/Registro%20do%20Device%20(Thing)/img/servicos.jpg?raw=true)

Entre no menu **Gerenciar** e escolha a opção **Coisas** em seguida _**Registre uma nova coisa**_

![iotCore](https://github.com/FelipeNasci/AWSTutorials/blob/master/Registro%20do%20Device%20(Thing)/img/iotCore.jpg?raw=true)

Siga os passos:

* Selecione Criar uma única coisa
* Insira o nome da coisa e avance
* Criar Certificado


![certificadoDownload](https://github.com/FelipeNasci/AWSTutorials/blob/master/Registro%20do%20Device%20(Thing)/img/certificados.jpg?raw=true)

Realize o download dos 03 arquivos e em seguida click em anexar uma política.

Note que no momento não há políticas a serem anexadas, então apenas registre a 'coisa'.

No menu **Proteger** selecione a opção **Políticas** e crie uma nova com as configurações a seguir:

![menuProteger](https://github.com/FelipeNasci/AWSTutorials/blob/master/Registro%20do%20Device%20(Thing)/img/proteger.jpg?raw=true)

```
Nome: Nome da Política
Ações: iot:*
Recurso ARN: *
Efeito: Permitir
Criar
```

![politicas](https://github.com/FelipeNasci/AWSTutorials/blob/master/Registro%20do%20Device%20(Thing)/img/criarPolitica.jpg?raw=true)

Ainda no menu **Proteger** selecione a opção **Certificados**.

Selecione o certificado criado e no menu Ações (ou botão direito do mouse) selecione Anexar Política

![anexar politica](https://github.com/FelipeNasci/AWSTutorials/blob/master/Registro%20do%20Device%20(Thing)/img/anexarPolitica.jpg?raw=true)

Pronto! O dispositivo já está criado

## Referências

Este tutorial está baseado no [AWS IoT Guia do desenvolvedor](https://docs.aws.amazon.com/pt_br/iot/latest/developerguide/register-device.html)