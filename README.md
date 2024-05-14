# aws-knowledge
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

        [               AZ1               ]       [               AZ2               ]
                                            
        |---------------------------------|       |---------------------------------|
        |                                 |       |                                 |
|------------------------------------------------------------------------------------------------------------------|
|       |                                 |       |                                 |                              |
|       |                                 |       |                                 |                              |
|       |                                 |       |                                 |                              |
|  ||===============================================================================================||             |
|  ||   |                                 |       |                                 |               ||             |
|  ||   |                                 |       |                                 |               ||             |
|  ||   |                                 |       |                                 |               ||     ECS     |
|  ||   |---------------------------------|       |---------------------------------|               ||             |
|  ||   |                                 |       |                                 |               ||   Cluster   |
|  ||   |      ECS Container Instance     |       |      ECS Container Instance     |               ||             |
|  ||   |                                 |       |                                 |      ECS      ||             |
|  ||   |  |------------| |------------|  |       |  |------------| |------------|  |    Service    ||             |
|  ||   |  |            | |            |  |       |  |            | |            |  |               ||             |
|  ||   |  |    Task    | |    Task    |  |       |  |    Task    | |    Task    |  |               ||             |
|  ||   |  |            | |            |  |       |  |            | |            |  |               ||             |
|  ||   |  |------------| |------------|  |       |  |------------| |------------|  |               ||             |
|  ||   |                                 |       |                                 |               ||             |
|  ||   |---------------------------------|       |---------------------------------|               ||             |
|  ||   |                                 |       |                                 |               ||             |
|  ||===============================================================================================||             |
|       |                                 |       |                                 |                              |
|------------------------------------------------------------------------------------------------------------------|
        |                                 |       |                                 | 
        |---------------------------------|       |---------------------------------|

```

## Passo 29: Criando um Docker Container no ECS
* Acessar a opção "Serviços" no menu do topo
* Escolher a opção "Contêineres" em seguida "Elastic Container Service"
* Criar um cluster na opção "Criar Cluster"
  - Utilizar a opção "AWS Fargate (sem servidor)"
  - Definir um nome para o cluster: cluster01
  - Criar cluster
* Selecionar o cluster e criar as "Tasks definitions" do tipo "AWS Fargate"
  - Definir um nome para a task: task01
  - Definir a CPU: .25 (Escolher a menor para teste)
  - Definir o tamanho/memória: .5 GB (escolher a menor para teste)
  - Adicionar um contêiner:
    * Nome: nginx
    * Image: nginx
    * Port Mapping: 80
    * Sistema operacional: Linux
    * Clicar em Adicionar
  - Criar Task definition
  - Cerificar que a task definition está "Ativa"
* Retornar ao cluster
* Iniciar uma task em "Tasks -> Run new task"
  - Opções de computação: "Estratégia do provedor de capacidade"
  - Provedor de capacidade: Fargate
  - Versão da plataforma: Latest
  - Configuração de implantação:
    * Tipo de aplicação: Tarefa
    * Família: task01 (nome criado na task definition)
    * Criar um novo grupo de segurança:
      - nome: task01-1234
      - descrição do grupo: Qualquer texto
      - Tipo: HTTP
      - Protocolo: TCP
      - Port Range: 80
      - Origem: Anywhere
      - Salvar
    * Deixar as outras configurações padrão
  - Criar Task
  - Aguardar a task ficar com o status "Em execução"
  - Copiar o endereçamento IP público das task para o navegador e aguardar a exibição da página de "Welcome" do nginx
* Para evitar custos adicionais para a tarefa e excluir o cluster

## Passo 30: Storage S3
* Serviços de armazenamento:
  - Amazon S3 (Simple Storare Service)
  - Amazon Glacer
  - Amazon EFS
  - Amazon SnowBall
  - Amazon CloudFront
  - Amazon Storage Gateway
  - Amazon EBS
  - Amazon Instance Store

* Categorias de conteúdos de armezenamento
  - Block Storage: É parecido com o sistema DAS (Data Attached Storage) e possui latência muito baixa servindo para armazenar arquivos do tipo : Blocos, volumes(disco USB, HD, ...)
  - File Storage: É comparado com o sistema NAS(Network Attached Storage) e serve para armazenar dados que serão compartilhados com 1 usuário ou mais.
  - Object Storage (S3): serve para armazenar objetos, metadata que ganham uma ID única, um endereçamento (Flat Address / URL)

## Passo 31: EBS (Elastic Block Storage)
* Na prática o volume EBS fica fora da Instância EC2.
* Deve estar na mesma zona de disponibilidade da instância EC2 (us-east-1)
* Pode ser conectado até 16 instâncias EC2 na mesma zona de disponibilidade:
  - Através do serviço EBS Multi-Attach
  - Utilizando o tipo de disco IO1
  - As instâncias EC2 devem ser do tipo NITRO

```bash

|--------------------------------------------------|
|                   EC2 Win 2019                   |
|----------------|----------------|----------------|
|      EBS1      |      EBS2      |      EBS3      |
|----------------|----------------|----------------|
|       GP2      |       SC1      |       GP2      |
|----------------|----------------|----------------|
|       50G      |      125G      |      100G      |
|----------------|----------------|----------------|
|                                                  |
|--------------------------------------------------|

```

 
## Passo 32: Tipos de volume EBS
* A AWS utiliza 2 tipo de disco
  - SSD (Solid State Drive): É mais rápido e muito mais caro
  - HDD (Hard Disk Drive): É mais lento e mais barato
* O EBS utiliza os seguintes tipos de discos
  
  - Para uso geral:
    
    * gp3:
      - Baixo custo SSD
      - Serve para desktops virtuais
      - Instâncias para banco de dados como Microsoft SQL Server e Oracle
      - Aplicações sensíveis a latência
      - Volumes botáveis com o windows, linux ou macos
      - Limite de tamanho de 16 terabites
      - Máximo de IOPS/Volume 16.000
      - Máximo Throughput/volume (cópia): 1.000 MB/s (1GB)
        
    * gp2:
      - (idem ao gp3)
      - Máximo Throughput/volume (cópia): 250 MB/s (mais lento para cópia)
        
  - IOPS:
    
    * io2 Block Express:
      - Alta performance
      - Uso intensivo em NoSQL e banco de dados relacional
      - Tamanho de 4GB a 64TB
      - Máximo de IOPS/Volume: 256.000
      - Máximo Throughput/volume (cópia): 4.000 MB/s (4GB)
      - Máximo de IOPS/Instância: 260.000
      - Máximo Throughput/instância (cópia): 7.500 MB/s
      
      
    * io2:
      - Alta performance
      - Uso intensivo em NoSQL e banco de dados relacional
      - Tamanho de 4GB a 16TB
      - Máximo de IOPS/Volume: 64.000
      - Máximo Throughput/volume (cópia): 1.000 MB/s (1GB)
      - Máximo de IOPS/Instância: 160.000
      - Máximo Throughput/instância (cópia): 4.750 MB/s
        
    * io1:
      - Alta performance
      - Uso intensivo em NoSQL e banco de dados relacional
      - Tamanho de 4GB a 16TB
      - Máximo de IOPS/Volume: 64.000
      - Máximo Throughput/volume (cópia): 1.000 MB/s (1GB)
      - Máximo de IOPS/Instância: 260.000
      - Máximo Throughput/instância (cópia): 7.500 MB/s

  - Throughput Optimized:
    * São HDD (st1) mais lentos

  - Cold HDD:
    * São HDD (sc1) mais lentos
    * Com acesso bem menor

## Passo 33: O que é Snapshot
* É um serviço que: Cria cópias
  - Permite utilizar cópias de Instâncias de volumes entre Zonas de disponibilidades
  - Realiza backup
  - Menu lateral: EBS (Elastic Block Store) > Volumes
    - Escolher o volume para criar o snapshot
    - Clicar em Modify volume > Create Snapshot
    - Atribuir um nome para a cópia
    - Clicar em create Snapshot
  - Menu lateral: EBS (Elastic Block Store) > Snapshot
  - Para utilizar na prática monta uma VM e puxar o volume do snapshot

## Passo 34: O S3 (Simple Storage Service)
* Pastas = Bucket: Com nomes únicos e universais
* Durabilidade: 99.9999999 (íntegro)
* Disponibilidade: 99.95 ou 99.99 (do tempo)

## Passo 35: Criando um Amazon AMI (Amazon Machine Image) customizada
* Através desse recurso é possível subir uma máquina idêntica a outra, isto é, já configurada em outra região
* Existem 2 tipos de imagens:
  - Públicas: Vem com a AWS ou de terceiros
  - Privadas: Minhas imagens criadas
* Em Ec2 > Instâncias
  - Selecionar a instância que será criada a imagem
  - Clicar na opção "Ações > Imagens e Modelos > Criar Imagem"
  - Informar o nome da imagem
  - Informar a descrição da imagem (opcional)
  - Deixar a máquina reiniciar para garantir o snapshot
  - Nos 3 volumes adicionados:
    * Deixar marcada a opção: delete on terminate
    * Se preferir pode encriptar alguns volumes
    * Pode também adicionar volumes
  - Clicar em "Criar Imagem" e aguardar a criação
* Acompanhar o processo em "AMIs"
  - Em ações:
    * Pode editar permissões
    * Pode torná-la publica
* Em EC2 > Instâncias pode se criar uma nova instância a partir daquela imagem:
  - Executar Instância
  - Definir o nome
  - Escolher a opção: Minha AMI
  - Definir as configurações
  - Escolher a nova zona de disponibilidade

## Passo 36: Criando a primeira Bucket
* Em S3 clicar em "Criar Bucket"
* O nome da Bucket deve ser único universalmente
  - Por padrão o prefixo do nome é o identificador único da organização: fabricioottoni-dados
* Escolher a região da AWS: us-east-1 (Virgínia)
* Propiriedades de objetos
  - Habilitar ou desabilitar as ACLs (Access List): por padrão é melhor ligar e futuramente adicionar os filtros
* Acessar a bucket e fazer o upload de arquivos ou pastas
* É possível arrastar os arquivos para uma determinada área e realizar o upload
* Clicando no objeto adicionado exibe todas as propriedades inclusive a uri unica
* ARN: nome do recurso

## Passo 37: Classes de armazenamento SD
* A cobrança pelo armazenamento no S3 é feita com base no tipo de classe de armazenamento
  
* Existem 8 tipos de classe de armazenamento
  1) S3 Padrão: É o tipo de armazenamenbto mais caro da AWS, serve para empresas que fazem o upload e download de arquivos ou utilizam aplicações que fazem o downloa e upload de arquivos de morma automatizada. É a classe mais rápida.
  2) S3 Inteligent-Tiering: Classe que coloca de forma inteligente o arquivo a ser armazenado na padrão (mais cara) e se esse arquivo não for mexido por algum tempo ele será movido para as classes mais baratas. Um nível de custo 60% mais barato que a padrão.
  3) S3 Standard-IA (Infrequent Access): Dentro da S3 se os arquivos não forem acessados com uma frequência muito grande eles podem ser deixados nessa classe. Se os acessos ultrapassarem o limite dessa classe você pode pagar por acesso extra. Esse tipo é recomendado para armazenamento de longa duração, backups e datastore.
  4) S3 One Zone-IA (Infrequant Access): O mesmo que S3 Standard-IA (Infrequent Access), porém em apenas uma zona de disponibilidade diminuindo muito o custo de armazenamento. Isso significa que se essa zona ficar indisponível você perde o acesso ao arquivo.
  5) S3 Glacier Instant Retrieval: Acessados 2 ou 3 vezes ano ano
  6) S3 Glacier Flexible Retrieval: Acessados 2 ou 3 vezes ano ano
  7) S3 Glacier Deep Archive: Armazenados por no mínimo de 7 a 10 anos para possível auditoria ou acesso
  8) S3 Outposts: Basicamente o mesmo sistema dos glaciers, porem dentro de um Outposts

* Gráfico de performance (atualizado):
```bash

                 |               |                    |                    |                  |                  |   S3 Glacier   |   S3 Glacier     |   S3 Glacier   |
                 |   S3 Padrão   |   S3 Inteligent-   |   S3 Express One   |   S3 Standard-   |   S3 One Zone-   |   Instant      |   Flexible       |   Deep         |
                 |               |   Tiering*         |   Zone**           |   IA             |   IA**           |   Retrieval    |   Retrieval***   |   Archive***   |
|----------------|---------------|--------------------|--------------------|------------------|------------------|----------------|------------------|----------------|
|                | Armazenamento | Economia automática| Armazenamento de   | Dados acessados  | Dados recriáveis | Dados de longa | Backup e         | Arquivamento de|
|                | de uso geral  | de custos para     | alta performance   | com pouca        | acessados com    | duração que    | arquivamento de  | dados que são  |
|                | para dados    | dados com padrões  | para seus dados    | frequência que   | pouca frequência | são acessados  | dados que        | raramente      |
|  Casos de uso  | acessados com | de acesso          | acessados com mais | precisam de      |                  | algumas vezes  | raramente são    | acessados e    |
|                | frequência    | desconhecidos ou   | frequência         | acesso em        |                  | por ano com    | acessados e      | custo muito    | 
|                |               | variáveis          |                    | milisegundos     |                  | recuperações   | baixo custo      | baixo          |
|                |               |                    |                    |                  |                  | instantâneas   |                  |                |
|----------------|---------------|--------------------|--------------------|------------------|------------------|----------------|------------------|----------------|
| Latência de    | Milissegundos |   Milissegundos    | Milissegundos de   |  Milissegundos   |  Milissegundos   | Milissegundos  | Minutos ou horas |      Horas     |
| primeiro byte  |               |                    | um dígito          |                  |                  |                |                  |                |
|----------------|---------------|--------------------|--------------------|------------------|------------------|----------------|------------------|----------------|
|                | O Amazon S3 fornece o armazenamento mais durável na nuvem. Com base em sua arquitetura exclusiva, o S3 foi projetado para exceder uma durabilidade |
|                | de dados de 99,999999999% (onze noves). Além disso, o S3 armazena dados de forma redundante em um mínimo de 3 zonas de disponibilidade por padrão, |
|  Durabilidade  | fornecendo resiliência integrada contra desastres generalizados. Os clientes podem armazenar dados em uma única AZ para minimizar o custo ou a     |
|                | latência do armazenamento, em várias AZs para maior resiliência contra a perda permanente de um data center inteiro ou em várias regiões da AWS    |
|                | para atender aos requisitos de resiliência geográfica.                                                                                             |
|----------------|---------------|--------------------|--------------------|------------------|------------------|----------------|------------------|----------------|
| Projetado para |     99,99%    |        99,9%       |       99,95%       |       99,9%      |       99,5%      |      99,9%     |      99,99%      |     99,99%     |
| disponibilidade|               |                    |                    |                  |                  |                |                  |                |
|----------------|---------------|--------------------|--------------------|------------------|------------------|----------------|------------------|----------------|
| Acordo de nível|               |                    |                    |                  |                  |                |                  |                |
| de serviço de  |     99,9%     |         99%        |        99,9%       |        99%       |        99%       |       99%      |       99,9%      |      99,9%     |
| disponibilidade|               |                    |                    |                  |                  |                |                  |                |
|----------------|---------------|--------------------|--------------------|------------------|------------------|----------------|------------------|----------------|
| Zonas de       |     >= 3      |        >= 3        |          1         |       >= 3       |         1        |      >= 3      |       >= 3       |      >= 3      |
| disponibilidade|               |                    |                    |                  |                  |                |                  |                |
|----------------|---------------|--------------------|--------------------|------------------|------------------|----------------|------------------|----------------|
| Cobrança       |               |                    |                    |                  |                  |                |                  |                |
| mínima pela    |      N/D      |         N/D        |       1 hora       |      30 dias     |      30 dias     |     90 dias    |      90 dias     |    180 dias    |
| duração do     |               |                    |                    |                  |                  |                |                  |                |
| armazenamento  |               |                    |                    |                  |                  |                |                  |                |
|----------------|---------------|--------------------|--------------------|------------------|------------------|----------------|------------------|----------------|
|  Taxa de       |      N/D      |         N/D        |         N/D        |      por GB      |      por GB      |     por GB     |      por GB      |     por GB     |
|  recuperação   |               |                    |                    |    recuperado    |    recuperado    |   recuperado   |    recuperado    |   recuperado   |
|----------------|---------------|--------------------|--------------------|------------------|------------------|----------------|------------------|----------------|
|  Transições de |      Sim      |         Sim        |         Não        |        Sim       |        Sim       |       Sim      |        Sim       |       Sim      |
|  ciclo de vida |               |                    |                    |                  |                  |                |                  |                |
|----------------|---------------|--------------------|--------------------|------------------|------------------|----------------|------------------|----------------|

```

## Passo 38: Valores do S3
* Utilizar o AWS Calculator (pesquisar na internet o link)

```bash

|---------------------------------------------------------------------------------------------------------------------------|
| S3 Standard: Armazenamento de uso geral par qualquer tipo de dados, usado normalmente para dados acessados com frequência |
|----------------------|----------------------------------------------------------------------------------------------------|
|  0,023 USD por GB    | Primeiros 50 TB/mês                                                                                |
|  0,022 USD por GB    | Próximos 450 TB/Mês                                                                                |
|  0,021 USD por GB    | Mais de 500 TB/Mês                                                                                 |
|---------------------------------------------------------------------------------------------------------------------------|
| S3 Inteligent-Tiering*: Economia de custo automática pada dados com padrôes de acesso desconhecidos ou variáveis.         |
|----------------------|----------------------------------------------------------------------------------------------------|
| 0,0025 USD por 1.000 | Monitoramento e automação, todo o armazenamento/mês (objetos > 128 KB)                             |
|            objetos   |                                                                                                    |
|----------------------|----------------------------------------------------------------------------------------------------|
|  0,023 USD por GB    | Camada de acesso frequente, primeiros 50 TB/mês                                                    |
|  0,022 USD por GB    | Camada de acesso frequente, próximos 450 TB/mês                                                    |
|  0,021 USD por GB    | Camada de acesso frequente, mais de 500 TB/mês                                                     |
|  0,0125 USD por GB   | Camada de acesso infrequente, todo o armazenamento/mês                                             |
|  0,004 USD por GB    | Camada de acesso instantâneo de arquivamento, todo armazenamento/mês                               |
|---------------------------------------------------------------------------------------------------------------------------|
| S3 Inteligent-Tiering*: Camada de acesso a arquivamento assíncronos opcionais                                             |
|----------------------|----------------------------------------------------------------------------------------------------|
|  0,0036 USD por GB   | Camada de acesso de arquivamento, todo o armazenamento/mês                                         |
|  0,00099 USD por GB  | Camada de acesso de arquivamento profundo, todo o armazenamento/mês                                |
|---------------------------------------------------------------------------------------------------------------------------|
| S3 Standard - Infrequent Access**: Para dados com retenção de longa duração, mas acessados com pouca frequência, que      |
|                      | precisam de acesso em milissegundos                                                                |
|----------------------|----------------------------------------------------------------------------------------------------|
|  0,0125 USD por GB   | Todo armazenamento/mês                                                                             |
|---------------------------------------------------------------------------------------------------------------------------|
| S3 One Zone - Infrequent acess**: Para dados recriáveis e acessados com pouca frequência que precisam de acesso em        |
|                      | milissegundos                                                                                      |
|----------------------|----------------------------------------------------------------------------------------------------|
|  0,01 USD por GB     | Todo o armazenamento/mês                                                                           |
|---------------------------------------------------------------------------------------------------------------------------|
| S3 Glacier Instant Retrieval***: Para dados de arquivo de longa duração acessados uma vez por trimestre com recuperação   |
|                      | instantânea em milissegundos                                                                       |
|----------------------|----------------------------------------------------------------------------------------------------|
|  0,004 USD por GB    | Todo armazenamento/mês                                                                             |
|---------------------------------------------------------------------------------------------------------------------------|
| S3 Glacier Flexible Retrieval (antiga S3 Glacier)***: Para backups de longo período de vigência e arquivs com opção de    |
|                      | recuperação de 1 minuto a 12 horas                                                                 |
|----------------------|----------------------------------------------------------------------------------------------------|
|  0,0036 USD por GB   | Todo oarmazenamento/mês                                                                            |
|---------------------------------------------------------------------------------------------------------------------------|
| S3 Glacier Deep Archive***: Para arquivamento de dados com retenção de longo período de vigência, acessados uma ou duas   |
|                      | vezes por ano e que podem ser restaurados em até 12 horas                                          |
|----------------------|----------------------------------------------------------------------------------------------------|
|  0,00099 USD por GB  | - Todo o armazenamento/mês                                                                         |
|---------------------------------------------------------------------------------------------------------------------------|
| O uso do armazenamento do Amazon S3 é calculado em gigabytes binários (GB), em que 1 GB é 2.30 bytes. Essa unidade de     |
| medida também é conhecida como gibilbyte (GiB), definida pela Comissão Eletrotécnica Internacional (IEC). Da mesma        |
| maneira, 1 TB é 2.40 bytes, ou seja 1024 GB.                                                                              |
|---------------------------------------------------------------------------------------------------------------------------|
```

## Passo 39: Alterando a classe de armazenamento no S3
* Alterar a classe de armazenamento de um aquivo ou pasta:
  - Em S3 abrir o bucket desejado
  - Selecionar o aquivo/pasta para alteração de classe de armazenamento
  - Clicar em Ações > Editar classe de armazenamento
  - Escolher qual classe de armazenamento (As classes que tem dias de armazenamento definidos já te cobrarão por esses dias logo no início)
  - Salvar as alterações

* Fazer o upload de um arquivo com o tipo específico: 
  - Em S3 abrir o bucket desejado
  - Escolher a opção carregar arquivo
  - Em propriedades escolher qual a classe de armazenamento


## Passo 40: O que é o versionamento S3
* A AWS cobra pelo armazenamento de todas as versões do mesmo arquivo.
* É possível apenas suspender o versionamento
* Não é possível excluir o versionamento uma vez qaue esteja feito.
  
```bash

                                                     BUCKET VERSIONING
          
                                  |------------------------------------------------------|
                                  |                                                      |
                                  |    |----------------|                                |
                                  |    | Texto.txt - V3 | -> 2.2 MB -> ID:275DBCC17F     |
                                  |    |----------------|                                |
                                  |    |----------------|                                |
                                  |    | Texto.txt - V2 | -> 2.1 MB -> ID:267ADCS89X     |
              UPLOAD              |    |----------------|                                |
      |-------------------->      |    |----------------|                                |
      |                           |    | Texto.txt - V1 | -> 2.0 MB -> ID:NULL           |
      |                           |    |----------------|                                |
      |                           |                                                      |
      |                           |------------------------------------------------------|
      |         
      |         |------------|
|-----------|   | xxxxxxxxxx | Texto.txt -> V1
|  Usuário  |   | yyyyyyyyyy | Texto.txt -> V2
|-----------|   | zzzzzzzzzz | Texto.txt -> V3
                |------------|

```
## Passo 41: Hospedando um website no S3
* Em S3 clicar em "Criar Bucket"
* O nome da Bucket deve ser único universalmente
  - Por padrão o prefixo do nome é o identificador único da organização: fabricioottoni-website
* Escolher a região da AWS: us-east-1 (Virgínia)
* Propiriedades de objetos
  - Habilitar as ACLs (Access List): por padrão é melhor ligar e futuramente adicionar os filtros
  - Habilitar a Hospedagem de site estático apontando para o arquivo index.html
* Acessar a bucket e fazer o upload do aquivo index.html
* É possível arrastar os arquivos para uma determinada área e realizar o upload
* Resolvendo o problema de permissões de acesso:
  - Alterar as permissões do bucket desativando o "Bloqueio de acesso público"
  - Alterar as permissões do arquivo index.html em "Ações de objeto > Tornar público usando ACL" 


## Passo 42: Habilitando o Ciclo de Vida no S3
* Criar regras de ciclo de vida para mover os arquivos/objetos entre classes de armazenamento
* Selecionar o arquivo/objeto dentro do bucket S3
* Clicar em gerenciamento
* Criar regra de ciclo de vida
  - Definir um nome para a regra: mover-30-dias-one-ia
  - Mover através de filtros ou aplicar para todos os objetos
    * Filtros: Definir prefixos "Development, Finance, Private"ou para toda a pasta sem prefixo (ver documentação de prefixo)
    * Aplicar para todos os arquivos da bucket: Aceitar a mensagems de "Reconhecimento" da regra para todos os arquivos da bucket.
  - Aplicar para todos as arquivos
  - Definir as ações da regra de ciclo de vida:
    * Mover versões atuais de objetos entre classes de armazenamento
    * Escolher transições de classes de armazenamento: Uma zona-IA
    * Dias depois da criação do objeto: 30
  - Analisar o resumo do que vai acontecer
  - Clicar em criar regra
  - Regra criada, habilitada, todo o bucket, transição para uma zona-IA
  - Dá para criar uma regra para manter apenas as 10 ultimas versões e evitar custos adicionais por versionamento de arquivos
* Clicar em gerenciamento
* Criar regra de ciclo de vida
  - Definir um nome para a regra: remover-versoes-antigas
  - Aplicar para todos as arquivos
  - Definir as ações da regra de ciclo de vida:
    * Excluir permanentemente versões desatualizadas de objetos
    * Dias após os objetos ficarem desatualizados: 30
    * Número de versões mais recentes a serem retidas: 10
  - Analisar o resumo do que vai acontecer
  - Clicar em criar regra


## Passo 43: Replicação de Objetos
* Replicar objetos de um bucket nos Estados Unidos para outra em Londres
* Você paga pela replicação e pelo armazenamento
* Criar um novo bucket s3
  - Nome: fabricioottoni-dados-london
  - Região da AWS: UE(Londres) eu-west-2
  - Habilitar o versionamento: Necessário estar habilidado na origem e no destino para que haja replicação
* Selecionar o bucket de origem
  - Selecionar "gerenciamento"
  - Regras de replicação > Criar Regra de replicação
  - Nome: us-london
  - Status: Habilitado
  - Bucket Origem
    * Aplicar a todos os objetos do bucket
  - Destino
    * Escolha um bucket nesta conta: fabricioottoni-dados-london
  - Função do IAM
    * Escolha em funçÕes do IAM existentes
    * Criar uma nova função
  - Categoria de armazenamento de destino
    * Alterar a classe de armazenamento dos objetos replicados
  - Classe de armazenamento
    * Padrão-IA
  - Salvar
* A mensagem: Replicar objetos existentes -> Sim
* Configurações de trabalho
* Escolher: Executar automaticamente o trabalho quando estiver pronto
* Desabilitar: Relatório de conclusão
* Salvar


## Passo 44: IAM Policies no S3
* Existem 3 formas de segurança no Bucket S3
  - Via IAM : Aplica a regra ao grupo ou ao usuário ou a role (controle centralizado)
  - Via Bucket Police
  - Via Access List
* Via IAM (Identity Access Management) Policies: Regras mais centralizadas e gernciamento mais fácil, escritas em JSON e a AWS ajuda nessa escrita.
  - Políticas aplicadas aos usuários
  - Políticas aplicadas a Grupos
  - Políticas aplicadas a Roles

  ```bash
                           IAM Policies


                 |---|
  |----------|   | x |  ------> User 
  |          |   | v |
  |  Bucket  |   | x |  ------> Group
  |          |   | v |
  |----------|   | x |  ------> Role
                 |---|

                |------| (Upload)
                | JSON | (List)
                |------| (etc)
  ```


## Passo 45: Bucket Policies no S3
* Permite ou bloqueia quem acessa o conteúdo de uma bucket aplicados diretamente/individualmente em uma bucket
* Bucket Policies
```bash
{
  "Version": "2012-10-27",
  "Statement": [{
    "Sid": "Allow",
    "Effect": "Allow",
    "Principal": {
      "AWS": [
        "arn:aws:iam:616161616161:root",
        "arn:aws:iam:616161616161:user/jason"
      ]
    },
    "Action": "s3:GetObject",
    "Resource": "arn:aws:s3:::foobucket/*"
  }]
}
```
* Endentendo o bucket policies
  - Bucket: foobucket
  - Usuários: jason e root
  - Ação: s3:GetObject
  - Efeito: permitir
  - Conteúdo: Bucket e todo conteúdo interno do bucket (/*)


## Passo 46: Utilizando o S3 Glacier
* o S3 Glacier foi criado para armazenamento de arquivos que não serão acessados por um longo período de tempo
* Muitas empresas utilizam como uma origem de backup
* Os objetos ficam armazenados no COLD D.C. (Data Center)
* Possui um custo de transição de objeto (retrieval per object)
* Existem 2 classes de arquivos/objetos dentro do S3 Glacier
  - Glacier: Você paga barato ($$) e pode pedir o retriever dos objetos com uma quantidade de tempo menor
  - Glacier Deep Archive: Você paga muito mais barato ($)
* Existem 3 formas de se recuperar os arquivos:
```bash
  |------------------------------------------------------------|-----------------|----------------------|
  |             Formas de recuperar arquivos                   |     Glacier     | Glacier Deep Archive |
  |------------------------------------------------------------|-----------------|----------------------|
  | Expedited | Acesso rápido (maior custo - $$$)              |   de 1 a 5 min  |       Não Tem        |
  |------------------------------------------------------------|-----------------|----------------------|
  | Standard  | Acesso mediano (médio custo - $$)              |  de 3 a 5 horas |       12 horas       |
  |------------------------------------------------------------|-----------------|----------------------|
  | Bulk      | Acesso demorado (baixo custo - $)              | de 5 a 12 horas |       48 horas       |
  |------------------------------------------------------------|-----------------|----------------------|
```
* Existem 2 features que são habilitadas e vem com as classes Glacier e Glacier Deep Archive:
  - S3 Object Lock
  - S3 Glacier Vault Lock
  - (Ninguém pode remover/alterar/mexer nesses arquivos por um determinado período de tempo: compliance, auditoria, etc)


## Passo 47: AWS Storage Gateway
* É o serviço da AWS que vai permitir que os servidores OnPremisse acessem o storage da AWS (S3). Para manter a compatibilidade da sua estrutura com a AWS.
* É considerado um sistema híbrido de armazenamento que vc armazena tanto na sua empresa quanto na cloud
* Muito utilizado para backup
* Possui um sistema de cache fantástico que habilita um recurso chamado LOW LATENCY para comunicação do OnPremisse com o S3
* Em resumo a AWS te envia um equipamento chamado "Storage Gateway" que vc conecta na rede logal e ele acessa diretamente seu bucket. Esse equipamento pode ser utilizado de 3 formas:
  - File Gateway: Utiliza o mesmo sistema de armazenamento do S3 se comportando igual ao S3
  - Volume Gateway: Utiliza o mesmo sistema de armazenamento do S3 se comportando igual a um Block Storage
  - Backup Gateway: Você escolhe o comportamento como file ou block storage
* Utilizar a calculadora de preços da AWS para ver qto custará a solução.


## Passo 48: Introdução ao DNS (Domain Name System)
* O DNS faz a tradução do nome do host/servidor para o número do IP/Endereço
```bash
                                                          |---------------|
                                               (2)|------>|               |
                                                  |  (3)  |   Root DNS    |
                                                  |   |---|               |
                                 |------------|   |   |   |---------------|
                                 |            |---|   | 
                                 |            |       |
                                 |   I S P    |<------|   |---------------|
   |------|      DNS Query (1)   |            |        (4)|               |
   |  PC  |--------------------->|            |---------->|   Top Level   |
   |------|<---------------------|            |<----------|    Domain     |  (2)
  |--------|         |     (8)   |            |        (5)|               |
 |----------|        |           |   D N S    |-------|   |---------------|
                     |           |   Server   |       |
              www.google.com     |            |<--|   |
                                 |------------|   |   |(6)|---------------|
                 154.1.1.2                        |   |-->|               |
                   TTL: 8 horas                   |       | Authoritative |
                                               (7)|-------|    DYN DNS    |  (3)
                                                          |               |
                                                          |---------------|
```


## Passo 49: O que é Route53
* Ele não é apenas um DNS, é um DNS bombado, turbinado.
* Se tiver 2 servidores de página web ele monitora os 2 e redireciona o tráfego para o que estiver no ar.
* Faz o rotemanto das querys de DNS para o servidor mais próximo.
* O Route 53:
  - Armazena as Zonas Hospedadas
  - Armazena os registros de redirecionamento para as zonas
  - Armazena as regras de geo localização
  - Possui outras regras e consultas de resolução de nomes


## Passo 50: Como registrar o seu domínio
* Acessar o Route 53
* No menu lateral acessar "Hosted Zones"
* No menu lateral acessar "Registered Domain"
  - Clicar em "Register Domain"
  - Escolher um nome para o domínio: fabricioottoni.link
  - Adicionar ao carrinho
  - Clicar em "Continue"
* Na próxima tela preencher os dados de contato
  - Concordar com os termos
  - Clicar em "Complete Order"
* A ordem será enviada com cucesso
* Receberá um email para verificar se o endereçamento de email está correto ou não em até 15 dias senão a solicitação será suspensa.


## Passo 51: Diferença entre Scaling UP x Scaling Out (Escalabilidade preditiva)
```bash

                    UP                                                       OUT
|----------------------------------------|               |----------------------------------------|
|                                        | EC2           |                                        |
|  |----------------------------------|  |               |  |----------------------------------|  | 
|  |               APP                |  |               |  |               APP                |  |
|  |----------------------------------|  |               |  |----------------------------------|  |
|                                        |               |                                        |
|  |----------------------------------|  |               |  |----------------------------------|  |
|  |              Linux               |  |               |  |              Linux               |  | 
|  |----------------------------------|  |               |  |----------------------------------|  | 
|                                        |               |                                        | 
|  |------| |------|  |------| |------|  |               |  |------| |------|  |------| |------|  | 
|  | CPU  | | Disk |  |  ENI | | RAM  |  |               |  | CPU  | | Disk |  |  ENI | | RAM  |  |
|  |------| |------|  |------| |------|  |               |  |------| |------|  |------| |------|  |
|                                        |               |                                        |
|----------------------------------------|               |----------------------------------------|
|  Voce pode aumentar os recursos dessa  |               |  Você pode não apenas aumentar os      |
|  VM, porém corre o risco dela falar e  |               |  recursos da VM como também duplicar,  |
|  parar de atender com o serviço        |               |  triplicar as instâncias (+redundancia |
|----------------------------------------|               |----------------------------------------|

```

## Passo 52: EC2 Auto Scaling (Scaling OUT)
* Permite criar de forma automática mais recursos para equilibrar a quantidade de acessos, procesamento e requisições.
* É necessário criar um grupo chamado "Auto Scaling Group", onde srão escritos as regras.
* Todo trabalho de monitoramento para verificar se precisa escalar ou não é feito pelo Amazon CloudWatch
* O AutoScalling foi criado apenas para iniciar e terminar instâncias e acontece via performance
* Basicamente quando se cria o Scalling Group tem que se criar uma mega instância chamada de Launch Template
```bash
                                     EC2 Auto Scaling

                                       |----------|
                                       |   EC2    |
|-----------------------------------|  |  Launch  |  |-----------------------------------|
|             Subnet - A            |  | Template |  |             Subnet - B            |
|-----------------------------------|  |-----|----|  |-----------------------------------|
|  |-----------------------------------------|----------------------------------------|  |
|  |  |-----------|  |-----------|  |                |  |-----------|  |-----------|  |  |
|  |  | Instância |  | Instância |  |  Auto Scaling  |  | Instância |  | Instância |  |  |
|  |  |    1A     |  |    1B     |  |     Group      |  |    2A     |  |    2B     |  |  |
|  |  |-----|-----|  |-----|-----|  |                |  |-----|-----|  |-----|-----|  |  |
|  |--------|--------------|----------------------------------|--------------|--------|  |
|-----------|--------------|--------|                |--------|--------------|-----------|
            |              |                                  |              |
            |              |                                  |              |
            |              |        |----------------|        |              |
            |              |--------|     Amazon     |--------|              |
            |-----------------------|   CloudWatch   |-----------------------|
                                    |----------------|
                                    Performance Monitor

```

## Passo 53: Criando um EC2 Auto Scaling
* Acessar o painel EC2
* Em EC2 > Modelo de execução - Criar um modelo de execução
  - Nome do modelo: webserver-template
  - Descrição da versão do modelo: 1.0
  - Imagem de aplicação do sistema operacional: Procurar por linux, escolher AMIs (Qualificado para nível gratuito)
  - Tipo de instância: t2.micro (Qualificado para nível gratuito)
  - Par de chaves: aws-server (utilizar a chave criada anteriormente)
  - Configurações de rede: us-east-1a (Iniciar nessa zona, utilizando a subnet e a vpc)
  - Grupo de segurança: web-ssh (criar um novo)
  - Descrição do grupo de segurança: Permitir tráfego http e ssh (se tiver certificado colocar - https)
  - Regras do grupo de segurança (adicionar):
    * ssh: Origem -> 0.0.0.0/0 (qualquer lugar)
    * http: Origem -> 0.0.0.0/0 (qualquer lugar)
    * https: Origem -> 0.0.0.0/0 (qualquer lugar)
  - Configurar armazenamento:
    * 1x de 8 GiB gp2
  - Detalhes avançados:
    * Em "Dados de Usuário" colocar um código de script que executará as seguintes ações:
      - Atualizar a versão de linux
      - Instalar o serviço de web server
      - Iniciar o serviço de webserver
      - Habilitar o serviço de web server
      - Criar uma variável para armazenar informações sobre a zona de disponibilidade
      - Enviar a informação para a apágina da web em forma de um arquivo *.txt
      - O arquivo *.txt se transformará em um arquivo *.html
        ```bash

	#!/bin/bash
	yum update -y
	yum install -y httpd
	systemctl start httpd
	systemctl enable httpd
	EC2AZ=$(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone)
	echo '<center><h1>Esta EC2 esta na Zona: AZID </h1></center>' > /var/www/html/index.txt
	sed "s/AZID/$EC2AZ/" /var/www/html/index.txt > /var/www/html/index.html

        ```
  - Criar modelo de execução
* Em EC2 > Grupo de Auto Scaling - Criar um grupo de auto scaling
  - Nome do grupo de auto scaling: webservers-AS
  - Modelo de execução: webserver_template
  - Próximo (Rede)
  - Qual VPC será utilizada: padrão da região
  - Escolher em quais zonas de disponibilidades e sub-redes as instancias serão criadas
    * us-east-1a, us-east-1b, us-east-1c
  - Próximo (Configurar opções avançadas)
  - Balanceamanto de carga
    * Nenhum load balancer (a princípio)
  - Configurações adicionais
    * Habiliter coleta de métricas
  - Próximo (Configurar políticas de escalabilidade e tamanho do grupo)
  - Tamanho do grupo
    * Capacidade desejada: 3 (Iniciar com 3 instâncias)
    * Capacidade Mínima: 3 (Ter no mínimo 3 instâncias)
    * Capacidade Máxima: 6 (Ter no máximo 6 instâncias)
  - Políticas de escalabilidade
    * Nenhuma
  - Próximo (Adicionar notificações)
    * Se quiser adicionar notificações SNS no email ou celular
  - Próximo (Adicionar tags)
    * Nenhuma por enquanto
  - Próximo (Análise)
    * Revisar tudo
  - Criar grupo do Auto Scaling
  - Abrir o Auto Scaling e em "Atividades" Visualizar a execução
  - Em EC2 "Instâncias" verificar se as 3 foram/estão sendo criadas
  - Pegar o endereço público de todas as instancias e verificar se o script do index.html deu certo
  
```bash
                                                          AUTO SCALING                                                                                        
                                                                                                                                         US-EAST-1
                                                            |------------------------------------------------------------------------------------|
                                                            |                                                                                    |
                                                            |                     |-----------------------------------------------------------|  |
                                                            |                     |  |-----|                                       US-EAST-1A |  |
                                                            |                     |  | EC2 |                                                  |  |
                                                            |                     |  |-----|                                                  |  |
                                                            |                     |-----------------------------------------------------------|  |
                                                            |                                                                                    |
                                                            |                     |-----------------------------------------------------------|  |
                                                            |                     |  |\---/|                                       US-EAST-1B |  |
                                                            |                     |  | \ / |                                                  |  |
                 |------------|                             |                     |  |-/-\-|                                                  |  |
                 |            |                             |                     |-----------------------------------------------------------|  |
                 |  Internet  |                             |                                                                                    |
                 |            |                             |                     |-----------------------------------------------------------|  |
                 |------------|                             |                     |  |-----|                                       US-EAST-1C |  |
   |------|                                                 |                     |  | EC2 |                                                  |  |
   |  PC  |                                                 |                     |  |-----|                                                  |  |
   |------|                                                 |                     |-----------------------------------------------------------|  |
  |--------|                                                |                                                                                    |
 |----------|                                               |------------------------------------------------------------------------------------|
     USER                                                                                                           
                                                                                                                    
                                                                                                                    
                                                                                                                    
```
## Passo 54: Introdução ao Load Balancer
* Faz a distribuição de carga entre a regiões da AWS
* Previne contra instâncias com falha
* Combinado com Auto Scaling as instâncias são restauradas/criadas

```bash
                                                          LOAD BALANCERS                                                                                        
                                                                                                                                                 
                                                            |------------------------------------------------------------------------------------|
                                                            |                                                                                    |
                                                            |                     |-----------------------------------------------------------|  |
                                                            |                     |                                                           |  |
                                                            |                     |     |-------|             |-------|                       |  |
                                                            |           |-------------->|  EC2  |      |----->|  EC2  |                       |  |
                                                   |-----------------|  |         |     |-------|      |      |-------|                       |  |
                        |---- www.empresa.com      |                 |--|         |        IP A        |         IP B                         |  |
                        |         |                |      Load       |      |--------------------------|                                      |  |
                        |         |---------> IP E |                 |------|     |----------------------------------------|--------------|---|  |
                       DNS              |--------->|     Balancer    |------|                                              | AUTO SCALING |      |
                 |------------|         |          |                 |      |     |----------------------------------------|--------------|---|  |
                 |            |         |          |                 |--|   |--------------------------|                                      |  |
       |-------->|  Internet  |---------|          |-----------------|  |         |     |-------|      |      |-------|                       |  |
       |         |            |                             |           |-------------->|  EC2  |      |----->|  EC2  |                       |  |
       |         |------------|                             |                     |     |-------|             |-------|                       |  |
   |------|                                                 |                     |        IP C                  IP D                         |  |
   | USER |                                                 |                     |                                                           |  |
   |------|                                                 |                     |-----------------------------------------------------------|  |
  |--------|                                                |                                                                                    |
 |----------|                                               |------------------------------------------------------------------------------------|
www.empresa.com                                                                                                          
                                                                                                                    
                                                                                                                    
                                                                                                                    
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

