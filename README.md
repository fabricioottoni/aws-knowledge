oxe
8# aws-knowledge
Repo para armazenar os resumos e estudos para certificação aws

# Login
https://933248616516.signin.aws.amazon.com/console

# Tipos de Cloud Computing
  - On-site : (On-premisse) Todo recurso computacional está alocado dentro do cliente
  - IaaS : Infrastructure as a Service
  - PaaS : Platform as a Service
  - SaaS : Software as a Service

```bash
[  On-site  ]       [   IaaS   ]      [   PaaS   ]       [   SaaS   ]

Applications                                             Applications
    Data                                                     Data
   Runtime                              Runtime             Runtime
 Middleware                            Middleware          Middleware
    O/S                                   O/S                 O/S
Virtualization     Virtualization     Virtualization     Virtualization
   Servers            Servers            Servers            Servers
   Storage            Storage            Storage            Storage
  NetWorking         NetWorking         NetWorking         NetWorking

```

## Passo 1: Criação da conta gratuita

## Passo 2: Configuração de alertas
- Procurar pelo serviço: billing
- Acessar o menu lateral Orcamentos/Budgets
- Criar alertas simples ou completos no valor desejado e enviar por email

## Passo 3: AWS CLI e CloudShell

## Passo 4: Regiões
* [us]-[east]-[2] = Ohio
  - Ohio = nome da Região
  - us = localização do continente
  - east = direção dentro do continente
  - 2 = quantidade de data centers dentro daquela região

## Passo 5: Zonas de disponibilidade
* [us]-[east]-[2][a] = Ohio
  - a = data center da Zona de disponibilidade a
  - us-east-2b = ...
  - us-east-2c = ...
  - ...
 
## Passo 6: Zonas Locais (ZL)
* ZL = Data centers menores conectados às zonas de disponibilidade e mais próximos dos usuários finais

## Passo 7: Wavelength
* O AWS Wavelength incorpora serviços de computação e armazenamento da AWS em redes 5G, fornecendo infraestrutura de computação de borda móvel para desenvolvimento, implantação e escalabilidade de aplicações de latência ultrabaixa

## Passo 8: AWS Outposts
* O AWS Outposts é uma família de soluções totalmente gerenciadas que fornecem infraestrutura e serviços da AWS para praticamente qualquer local da borda ou on-premises para uma experiência híbrida verdadeiramente consistente. As soluções do Outposts permitem que os clientes estendam e executem serviços da AWS nativos on-premises

## Passo 9: AWS IAM (Identity Access Management)
```bash
-- console ->         users, roles, groups ------->              IBP (Identity Based Police) -> EC2
-- cli -----> IAM --> federated users (facebook, -> Políticas -> RBP (Resource Based Police) -> S3
-- api ----->         google, etc...)            ->                                          -> Auto Scalling, ALB
                      applications --------------->                                          -> etc...

--| AWS Account |--
|
|   Usuários -> Nome -> Permissões/Privilégios -> Console, CLI, API...
|                       ( cria sem permissões )
|
|   Grupos -> Usuários -> Permissões/Privilégios
|
|
|   Roles -> Serviços
|
|
|   Policies -> Aplicadas aos Usuários ou aos Grupos
|
---
```

## Passo 10: Criar um usuário na AWS
* Procurar pelo serviço: IAM
* Acessar o menu lateral Usuários/Users
* Definir o nome do usuário
* Fornecer acesso para os usuários ao Console de Gerenciamento da AWS - opcional
  - Criar um usuário direto no IAM
* Não atribuir grupo deixando na opção padrão: Adicionar usuário ao grupo (futuramente)
* Criar uma etiqueta (TAG)
  - Chave: Departamento
  - Valor: TI

## Passo 11: Aplicando política de acesso ao usuário
* Procurar pelo serviço: IAM
* Acessar o menu lateral Usuários/Users
* Adicionar permissões
  - Por grupo:
  - Por cópia de outro usuário:
  - Por Police diretamente: AdministratorAccess

## Passo 12: Entendendo sobre o processo de Autenticação
* Basicamente existem 2 formas diferentes de AUTENTICAÇÃO
  - Por informações do usuário: login, senha e MFA (Acesso ao console)
    ```bash
    - Usuário -> login, senha e MFA -> Console
    ```
  - Por informações da conta: Access Key ID e Secret Access Key (Acesso para CLI e API)
    ```bash
    - CLI ou API -> Access Key ID e Secret Access Key -> IAM -> API -> EC2, S3, ALB, Route 53...
    ```

## Passo 13: Entendendo e habilitando o MFA (Multi-factor authentication)
* Procurar pelo serviço: IAM
* Acessar o menu lateral Painel
* Habilitar MFA
  - Para root
  - Para cada usuário novo

## Passo 14: Alterando a política dde senhas do IAM
* Procurar pelo serviço: IAM
* Acessar o menu lateral: Painel
* Acessar o menu lateral: Configurações da Conta/Account Settings
  - Política de Senha/Password Police
  - Editar e colocar os critérios necessários

## Passo 15: O que é virtualização
   - EC2: Elastic Computing Cloud ( E C [2] )

```bash

[      On-site     ]                     [ EC2 - Elastic Compute Cloud ]

|------------------| -> Word             |-------|  |-------|  |-------|
|   Applications   | -> Excel            |  APP  |  |  APP  |  |  APP  |
|------------------| -> App              |-------|  |-------|  |-------|
                                      
                                      
                                         |-------|  |-------|  |-------|
|------------------|                     |  Win  |  | Linux |  | MacOs |
|                  | -> Windows          |-------|  |-------|  |-------|
| Operating System | -> Linux         
|                  | -> MacOS
|------------------|                     |-----------------------------|
                                         |    Virtualization Layer     |
                                         |-----------------------------|


|------------------|                     |-----------------------------|
|     Hardware     |                     |          Hardware           |
|------------------|                     |-----------------------------|

```

## Passo 16: Conhecendo o EC2
* Vantagens
  - Controle
  - Segurança
  - Serviços AWS
  - Custo Baixo
  - Descomplicado/Fácil

## Passo 17: Criando uma instancia EC2 windows 2019
* Acessar o menu lateral: Computação/Computing
* Procurar pelo serviço: EC2
* Escolher a opção: Executar Instância
* Preencher os campos necessárrios:
  - Nome da Instância: servidor1A (Nome de acordo com o projeto que se deseja criar)
  - Escolher a imagem da Instância: Windows, Linux, MacOs, Etc ... Escolhemos Windows Base para teste
  - Definir a quantidade de Instâcias: 1 (uma para teste)
  - Tipo de Instância: t2.micro
  - Par de chaves: Criar um novo -> aws-server -> Criar certificado
  - Nas configurações de rede: deixar apenas para acesso pelo meu IP
  - Conferir outras configurações caso necessário
  - Clicar em executar Instância

## Passo 18: Acessando uma instancia EC2 windows 2019
* Utilizar acesso RDP local
* Utilizar o par de chaves gerado no passo anterior
* Opções da Instância (principais)
  - Interromper
  - Iniciar
  - Encerrar

## Passo 19: Criando uma instancia EC2 Linux
* Acessar o menu lateral: Computação/Computing
* Procurar pelo serviço: EC2
* Escolher a opção: Executar Instância
* Preencher os campos necessárrios:
  - Nome da Instância: servidor1B (Nome de acordo com o projeto que se deseja criar)
  - Escolher a imagem da Instância: Windows, Linux, MacOs, Etc ... Escolhemos Linux Base para teste
  - Definir a quantidade de Instâcias: 1 (uma para teste)
  - Tipo de Instância: t2.micro
  - Par de chaves: Utilizar existente -> aws-server 
  - Nas configurações de rede: deixar apenas para acesso pelo meu IP
  - Conferir outras configurações caso necessário
  - Clicar em executar Instância
 
## Passo 20: Acessando uma instancia EC2 Linux 2023
* Utilizar acesso Conexão de Instância do EC2
* Utilizar o par de chaves gerado nos passos anteriores
* Opções da Instância (principais)
  - Interromper
  - Iniciar
  - Encerrar

## Passo 21: O que é User Data?
* É a parte dentro da instância EC2 que ao iniciar você consegue adicionar um código e esse código vai rodar somente uma vez no START daquela instância e esse código vai ser executado dentro da instância
* Acessar o menu lateral: Computação/Computing
* Procurar pelo serviço: EC2
* Na criação da Instância, nas configurações avançadas, existe o tópico do "User Data"
  - Pode ser um código como texto (As text):
    ```bash
    #!/usr/bin/env bash

    yum install httpd -y
    systemctl start httpd
    systemctl enable httpd
    ```
  - Pode ser um arquivo de script (As file - Limitado ao tamanho de 16KB):
    - Scripts do tipos: .sh, .bat ou powershell

## Passo 22: Criando uma Instância com User Data
* Acessar o menu lateral: Computação/Computing
* Procurar pelo serviço: EC2
* Escolher a opção: Executar Instância
* Preencher os campos necessárrios:
  - Nome da Instância: webserver01 (Nome de acordo com o projeto que se deseja criar)
  - Escolher a imagem da Instância: Windows, Linux, MacOs, Etc ... Escolhemos Amazon Linux Base para teste
  - Definir a quantidade de Instâcias: 1 (uma para teste)
  - Tipo de Instância: t2.micro
  - Par de chaves: Utilizar existente -> aws-server 
  - Nas configurações de rede:
    - deixar aberto para todos os IPs
    - permitir tráfego http
  - Conferir outras configurações caso necessário
  - Clicar em executar Instância

## Passo 23: Acessando S3 via EC2 com IAM User
* Realizar o "Passo 20" deste tutorial
* No terminal entre no modo admin de privilégio: sudo su
* Listar conteúdo do S3: aws s3 ls
* acontecerá o seguinte erro: Unable to locate credentials. You can configure credentials by running "aws configure"
* Executar o "Passo 10" com as seguintes exceções:
  - Não marcar a opção: Fornecer acesso para os usuários ao Console de Gerenciamento da AWS - opcional
  - A única política associada deve ser S3FullAccess
  - Após o usuário criado criar um par de chaves para ele poder ser utilizado
  - Os valores aparecem apenas 1 vez
* Retomar o terminal da instância e executar o comando: aws configure:
  - informar a chave de acesso: AWS Access Key ID
  - informar a chave de segredo: AWS Secret Key
  - informar a region: us-east-1 (virgínia)
  - informar o outputformat: none
* Listar conteúdo do S3: aws s3 ls
* Agora se consegue ver os aruivos através das credenciais de chaves na aws. (método falho, com pouca segurança)
* Após os testes apagar o usuário
* Após os testes removar as credenciais na pasta do EC2
  - Na pasta ~/.aws remover todo o conteúdo com: rm -rf *

## Passo 24: Acessando S3 via EC2 com IAM Roles (funções)
* Realizar o "Passo 20" deste tutorial
* No terminal entre no modo admin de privilégio: sudo su
* Listar conteúdo do S3: aws s3 ls
* Acontecerá o seguinte erro: Unable to locate credentials. You can configure credentials by running "aws configure"
* Procurar pelo serviço: IAM
* Acessar o menu lateral: Painel
* Acessar o menu lateral: Funções (Roles)
* Clicar em "Criar Perfil"
 - Selecionar o tipo de entidade confiável: Serviço AWS
 - Selecionar caso de uso: EC2
 - Escolher como permissão/acesso: S3FullAccess
 - Escolher um nome para a função: ec2-s3-full-access
* Procurar pelo serviço: EC2
* Escolher a opção: Executar Instância
  - Selecioanr a Instância que receberá a Role/função
  - Cricar em Ações:
    - Segurança
      - Modificar função do IAM
        - Escolher a função: ecs-s3-full-access
        - Atualizar função do IAM

## Passo 25: O AWS Batch (Lote/Grupo)
* Um serviço da AWS criado para rodar scripts em lote/grupo em grande quantidade.
* Para iniciar um batch precisamos das seguintes etapas:
  - Criar um job: Pode ser um job de shell script ou docker images
  - Job definition: Onde definimos os scripts.
  - Job Queue: Fila de trabalho dos scripts
  - Batch compute environment: Recebe ações de EC2/ECS/Fargate

## Passo 26: Sobre o AWS LightSail (Simple cloud server)(com menos poder computacional)
* Significa "Navegar com facilidade"
* Pode iniciar instancias linux, windows
* Toda parte de compute
* Storage
* Configurações básicas de VPC
* Servidores pré configurados
* Conexão SSH

## Passo 27: Docker
* Veio para mudar a indústria da virtualização e servidores
```bash

[         Antes do Docker         ]        [         Depois do Docker        ]

|---------------------------------|        |-----------------------------------------|
|       VM1      |       VM2      |        | Container 1 | Container 2 | Container 3 |
|----------------|----------------|        |             |             |             |
|       APP      |       APP      |        |    Pyton    |     .Net    |    Java     |   <- Recurso
|----------------|----------------|        |             |             |             |
|       OS       |       OS       |        | Code/Setup  | Code/Setup  | Code/Setup  |    
|----------------|----------------|        |-----------------------------------------|
| Proc/Disco/Mem | Proc/Disco/Mem |        |              Docker Image               |
|---------------------------------|        |-----------------------------------------|
|           Hypervisor            |        |                Windows OS               |
|---------------------------------|        |-----------------------------------------|
|             Server              |        |                 Server                  |
|---------------------------------|        |-----------------------------------------|

```
## Passo 28: O Amazon Elastic Container Service (ECS)
* Existem 2 tipo de de clusters ECS:
  - ECS EC2 Cluster: Você gerencia, você configura autoscalling, você configura indisponibilidade
  - ECS Fargate Cluster: É serverless, você nao configura nada. A AWS gerencia pra você.
* "Docker Container" é a mesma coisa que "AWS Task" (task = container)
* "Docker Image" é a mesma coisa que "AWS Registry" (registry = image)
* ECR (Elastic Container Registry) é o lugar na AWS que gerencia os registries
* ECS Cluster: Armazena todos os recursos das zonas de disponibilidades (ECS Service)
* ECS Service: Gerencia todos os recursos das zonas de disponibilidades (ECS Container Instance)
* ECS Container Instance: Armazena as configurações de task definitions (Task)
* ECS Task: É o container/task baseado em um registry/image ECR
```bash

        [               AZ1               ]         [               AZ2               ]
                                            
        |---------------------------------|         |---------------------------------|
        |                                 |         |                                 |
|--------------------------------------------------------------------------------------------------------------------|
|       |                                 |         |                                 |                              |
|       |                                 |         |                                 |                              |
|       |                                 |         |                                 |                              |
|  ||=================================================================================================||             |
|  ||   |                                 |         |                                 |               ||             |
|  ||   |                                 |         |                                 |               ||             |
|  ||   |                                 |         |                                 |               ||     ECS     |
|  ||   |---------------------------------|         |---------------------------------|               ||             |
|  ||   |                                 |         |                                 |               ||   Cluster   |
|  ||   |      ECS Container Instance     |         |      ECS Container Instance     |               ||             |
|  ||   |                                 |         |                                 |      ECS      ||             |
|  ||   |  |------------| |------------|  |         |  |------------| |------------|  |    Service    ||             |
|  ||   |  |            | |            |  |         |  |            | |            |  |               ||             |
|  ||   |  |    Task    | |    Task    |  |         |  |    Task    | |    Task    |  |               ||             |
|  ||   |  |            | |            |  |         |  |            | |            |  |               ||             |
|  ||   |  |------------| |------------|  |         |  |------------| |------------|  |               ||             |
|  ||   |                                 |         |                                 |               ||             |
|  ||   |---------------------------------|         |---------------------------------|               ||             |
|  ||   |                                 |         |                                 |               ||             |
|  ||=================================================================================================||             |
|       |                                 |         |                                 |                              |
|--------------------------------------------------------------------------------------------------------------------|
        |                                 |         |                                 | 
        |---------------------------------|         |---------------------------------|

```

<h1 align="center">
  <br>
  <a href="http://www.amitmerchant.com/electron-markdownify"><img src="https://raw.githubusercontent.com/amitmerchant1990/electron-markdownify/master/app/img/markdownify.png" alt="Markdownify" width="200"></a>
  <br>
  Markdownify
  <br>
</h1>

<h4 align="center">A minimal Markdown Editor desktop app built on top of <a href="http://electron.atom.io" target="_blank">Electron</a>.</h4>

<p align="center">
  <a href="https://badge.fury.io/js/electron-markdownify">
    <img src="https://badge.fury.io/js/electron-markdownify.svg"
         alt="Gitter">
  </a>
  <a href="https://gitter.im/amitmerchant1990/electron-markdownify"><img src="https://badges.gitter.im/amitmerchant1990/electron-markdownify.svg"></a>
  <a href="https://saythanks.io/to/bullredeyes@gmail.com">
      <img src="https://img.shields.io/badge/SayThanks.io-%E2%98%BC-1EAEDB.svg">
  </a>
  <a href="https://www.paypal.me/AmitMerchant">
    <img src="https://img.shields.io/badge/$-donate-ff69b4.svg?maxAge=2592000&amp;style=flat">
  </a>
</p>

<p align="center">
  <a href="#key-features">Key Features</a> •
  <a href="#how-to-use">How To Use</a> •
  <a href="#download">Download</a> •
  <a href="#credits">Credits</a> •
  <a href="#related">Related</a> •
  <a href="#license">License</a>
</p>

![screenshot](https://raw.githubusercontent.com/amitmerchant1990/electron-markdownify/master/app/img/markdownify.gif)

## Key Features

* LivePreview - Make changes, See changes
  - Instantly see what your Markdown documents look like in HTML as you create them.
* Sync Scrolling
  - While you type, LivePreview will automatically scroll to the current location you're editing.
* GitHub Flavored Markdown  
* Syntax highlighting
* [KaTeX](https://khan.github.io/KaTeX/) Support
* Dark/Light mode
* Toolbar for basic Markdown formatting
* Supports multiple cursors
* Save the Markdown preview as PDF
* Emoji support in preview :tada:
* App will keep alive in tray for quick usage
* Full screen mode
  - Write distraction free.
* Cross platform
  - Windows, macOS and Linux ready.

## How To Use

To clone and run this application, you'll need [Git](https://git-scm.com) and [Node.js](https://nodejs.org/en/download/) (which comes with [npm](http://npmjs.com)) installed on your computer. From your command line:

```bash
# Clone this repository
$ git clone https://github.com/amitmerchant1990/electron-markdownify

# Go into the repository
$ cd electron-markdownify

# Install dependencies
$ npm install

# Run the app
$ npm start
```

> **Note**
> If you're using Linux Bash for Windows, [see this guide](https://www.howtogeek.com/261575/how-to-run-graphical-linux-desktop-applications-from-windows-10s-bash-shell/) or use `node` from the command prompt.


## Download

You can [download](https://github.com/amitmerchant1990/electron-markdownify/releases/tag/v1.2.0) the latest installable version of Markdownify for Windows, macOS and Linux.

## Emailware

Markdownify is an [emailware](https://en.wiktionary.org/wiki/emailware). Meaning, if you liked using this app or it has helped you in any way, I'd like you send me an email at <bullredeyes@gmail.com> about anything you'd want to say about this software. I'd really appreciate it!

## Credits

This software uses the following open source packages:

- [Electron](http://electron.atom.io/)
- [Node.js](https://nodejs.org/)
- [Marked - a markdown parser](https://github.com/chjj/marked)
- [showdown](http://showdownjs.github.io/showdown/)
- [CodeMirror](http://codemirror.net/)
- Emojis are taken from [here](https://github.com/arvida/emoji-cheat-sheet.com)
- [highlight.js](https://highlightjs.org/)

## Related

[markdownify-web](https://github.com/amitmerchant1990/markdownify-web) - Web version of Markdownify

## Support

<a href="https://www.buymeacoffee.com/5Zn8Xh3l9" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/purple_img.png" alt="Buy Me A Coffee" style="height: 41px !important;width: 174px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;" ></a>

<p>Or</p> 

<a href="https://www.patreon.com/amitmerchant">
	<img src="https://c5.patreon.com/external/logo/become_a_patron_button@2x.png" width="160">
</a>

## You may also like...

- [Pomolectron](https://github.com/amitmerchant1990/pomolectron) - A pomodoro app
- [Correo](https://github.com/amitmerchant1990/correo) - A menubar/taskbar Gmail App for Windows and macOS

## License

MIT

---

> [amitmerchant.com](https://www.amitmerchant.com) &nbsp;&middot;&nbsp;
> GitHub [@amitmerchant1990](https://github.com/amitmerchant1990) &nbsp;&middot;&nbsp;
> Twitter [@amit_merchant](https://twitter.com/amit_merchant)

