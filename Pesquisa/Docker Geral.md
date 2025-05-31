
# Pt/BR

Docker é uma ferramenta muito poderosa no meio do desenvolvimento. Ele permite “empacotar” uma aplicação com todas as suas dependências em um ambiente isolado, chamado de **container**. Esses containers garantem que o sistema rode da mesma forma em qualquer lugar, seja localmente ou na nuvem – independentemente do sistema operacional da máquina em questão.

A grande sacada do Docker é reunir todas as dependências do projeto, sejam elas quais forem, em um único arquivo chamado Dockerfile. Com isso, o Docker monta uma **imagem**, que basicamente é um “modelo” do ambiente onde os arquivos estão. Depois, você usa essa imagem para criar um container, que funciona como uma **mini-máquina** que roda exatamente do jeito que você definiu.

É parecido com uma máquina virtual, mas muito mais leve e rápida, já que o container compartilha o kernel do sistema operacional com o host, ao invés de rodar um sistema inteiro dentro de outro.

No dia a dia, o Docker é muito utilizado para desenvolvimento, testes e deploy. É possível subir APIs, banco de dados e até o frontend de uma aplicação – cada um em um container separado – e tudo se conecta como se estivesse no mesmo ambiente. E se algo der errado, é só parar o container e subir outro, o que facilita bastante a gestão e uso de cada aplicação.


# EN

Docker is a powerful tool widely used in the development world. It allows you to “package” an application along with all its dependencies into an isolated environment called a **container**. These containers ensure that the system runs the same way anywhere—locally or in the cloud—regardless of the machine’s operating system.

The key idea behind Docker is to gather all the project’s dependencies, whatever they may be, into a single file called a Dockerfile. From that, Docker builds an **image**, which is essentially a blueprint of the environment where your application runs. You then use this image to create a container, which behaves like a **mini-machine**, running exactly as you defined.

It’s similar to a virtual machine, but much lighter and faster since the container shares the host’s operating system kernel instead of running an entire OS inside another.

In everyday development, Docker is often used for building, testing, and deploying applications. You can run APIs, databases, and even the frontend of an application—each in its own container—while everything connects as if it were in the same environment. And if something goes wrong, you can simply stop the container and spin up a new one, making it much easier to manage and maintain each component.