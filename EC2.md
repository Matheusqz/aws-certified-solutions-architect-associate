# EC2

Amazon Elastic Compute Cloud is a wer service that provides resizable compute capacity in the cloud. Amazon EC2 reduces the time required to obtain and boot new server instances to minut4es, allowing you quickly scale capacity, both up and down, as your computinf requirements change.

## Pricing Models

### On Demandd

Allows tou pay a fixed rate by the hour (or by second) with no commitment.

#### Useful for

- Users that want the low cost and flexibility of Amazon EC2 without any up-front payment of long-term commitment
- Applications with short term, spiky, or unpredictable workloads that cannot be interrupted
- Applications being developed or tested on AWS EC2 for the first time.

### Reserved

Provides you with a capacity reservation, and offer a significant discount on the hourly charge for an instance. Contract Terms are 1 ou 3 Year Terms.

#### Reserved Price Types

- Standard Reserved Instances: these offer up to 75% off on demand instances. The more you pay up front and the longer the contract, the greater the disconunt
- Comvertible Reserved Instances: these offer up to 54% off on demand capability to change the attributes od RI as long as the exchange result in the creation of Reserved Instances of Equeal or Greater Value.
- Scheduled Reserved Instances: these are available to lanch within the time windows you reserve. This option allows you to match your capacity reservation to a predictable recurriing schedule that only requires a fraction of day, a week, or a month.

#### Useful for

- Applications with steady steady state or predictable usage
- Applications that reserver capacity
- Users able to make upfront payments to reduce their total computins costs even further

### Spot

Enables you to bid whatever price you want for instance capacity, providing for even greates savings if your applications have flexible start and end times.

#### Useful for

- Applications that have flexible star and end times.
- Applications that are only feasible at very low compute prices
- Users with urgent computing needs for large amounts of additional capacity

### Dedicated Host

Physical EC2 server dedicated for your use. Dedicated Hosts can help you reduce costs by allowing you to use your existing server-bound sotfware licenses.

#### Useful for

- Regulatory requirements that may not support multi-tenant virtualization
- Great for licensing which does not suporte multi-tetancy or cloud deployments
- Can be purchased On-Demand (hourly)

## Security Groups

A security group acts as a virtual firewall that controls the traffic for one or more instances.

- All Indound traffic is blocked by default
- All outbound traffic is allowed
- If you create an indound rule allowing traffic in, that traffic is automatically allowed back out again.
- Changes to security groups take effect immediately
- You can have any number of EC2 instances within a security  group
- You can have multiple security groups attached to EC2 Instances
- You can specity allow rules, but not deny rules
- Security Groups are STATEFUL
- Uou cannot block specific IP addresses using Security Groups, instead use Network Access Control Lists.

EBS = Elastic Block Storage
Permite criar volumes de armazenamento e anexá-los em instâncias EC2.
EBS volumes são colocados em áreas disponíveis específicas, onde são automáticamente replicadas para proteger de falhas de um único componente.




Tipos de volume EBS:

Uso geral SSD ( GP2 ), fornece equilíbrio entre perfomance e custo. Famoso custo-benefício.

SDD IOPS provisionado, para aplicações que necessitam de alta perfomance, com aplicações intensas como grandes bancos relacionais ou não-relacionais.

HDD ( ST1 ) rendimento otimizado, para uso de BigData, Data Warehouses, processamento de logs.
Não pode ser utilizado como volume de boot.

Cold HDD ( SC1 ) 
Baixo custo de armazenamento, utilizado para contextos que não precisam acessar frequentemente o disco, como um servidor de arquivos.
Não pode ser utilizado para boot.

Volumes magnéticos, menor custo de armazenamento da categoria dos volumes bootaveis, ideal para para contextos onde os dados não são acessados frequentemente e aplicações onde o menor custo de armazenamento é importante.

Resumo
EC2 pricing
Sob demanda (on demand): 
Você paga pela capacidade computacional por hora ou por segundo, dependendo das instâncias executadas
Não são necessários compromissos de longo prazo nem pagamentos antecipados. 
Você pode aumentar ou diminuir a capacidade computacional dependendo das demandas do aplicativo e pagar apenas as taxas por hora especificadas para a instância utilizada.
As instâncias sob demanda são recomendadas para:
Usuários que preferem o custo baixo e a flexibilidade do Amazon EC2 sem nenhum pagamento adiantado ou compromisso de longo prazo
Aplicações com cargas de trabalho breves, com picos de utilização ou imprevisíveis e que não podem ser interrompidas
Aplicativos sendo desenvolvidos ou testados no Amazon EC2 pela primeira vez


Instâncias reservadas (reserved):
As instâncias reservadas proporcionam um desconto significativo (até 75%) em comparação com a definição de preço das instâncias por demanda.
Para aplicações com estado constante ou uso previsível, as instâncias reservadas podem oferecer uma economia considerável em comparação ao uso de instâncias sob demanda. 
Contratos de 1 ou 3 anos.
As Instâncias Reservadas são recomendadas para:
Aplicações com estado constante
Aplicações que podem exigir capacidade reservada
Clientes que podem se comprometer com o uso do EC2 por um período de 1 ou 3 anos para reduzir os custos totais de computação


Spot:
As instâncias spot do Amazon EC2 permitem solicitar capacidade computacional extra do Amazon EC2 com desconto de até 90% em relação ao preço das instâncias sob demanda.
Funciona como um leilão
A qualquer momento a Amazon pode parar de fornecer essa máquina se alguém oferecer um valor maior por ela e você não cobrir a oferta
As instâncias spot são recomendadas para:
Aplicati	vos que têm períodos de início e de término flexíveis
Aplicativos que são viáveis somente por preços computacionais muito baixos
Usuários com necessidades computacionais urgentes para grandes quantidades de capacidade adicional
Dedicadas (dedicated):
Um host dedicado é um servidor físico do EC2 dedicado exclusivamente ao seu uso. 
Os hosts dedicados ajudam você a reduzir custos, permitindo que você use licenças existentes de software vinculadas ao servidor, incluindo Windows Server, SQL Server e SUSE Linux Enterprise Server (sujeito aos termos das suas licenças), além de ajudar a cumprir requisitos de conformidade.


Se uma instância spot for encerrada pela AWS, não é feita a cobrança pela hora que ela estava rodando. Se ela for encerrada manualmente pelo usuário, a hora toda é cobrada.

Tipos de instâncias EC2
F -> FPGA (Field Programmable Gate Array). Genomic, financial analytics, real-time video processing, big data
I -> IOPS (Input/Output Operations Per Second). High speed storage
G -> Graphics, video encoding, 3D application
H -> High disk throughput 
T -> cheap general purpose (T2 Micro)
D -> Density
R -> RAM optimized
M -> Main choice for general purpose
C -> Compute (GPU, machine learning, bitcoin mining)
P -> Pics (graphics)
X -> Xtreme Memory

Tipos de Instâncias EBS 

SSD
GP2: General Purpose SSD
Propósito geral
Equilibra preço e performance
IO1: Provisioned IOPS SSD
SSD de maior performance para sistemas com muita leitura de disco ou que precisam de latências muito baixas
More than 10000 IOPS, up to 20000 IOPS
Magnético
ST1: Throughput Optimized HDD 
HDDs de baixo custo para acessos frequentes e altos throughputs 
Cannot be a boot volume
SC1: Cold HDD
HDD de menor custo e menor performance, para sistemas com pouco acesso/leitura
Cannot be a boot volume either
Magnetic
Lowest cost per gigabyte that is bootable
Ideal for data accessed infrequently or 
Applications where low cost for data storing is important

ELB 
3 tipos de load balancers:
Application LB
Network LB
Classic LB (ou Elastic Load Balancer)

Error 504 -> Gateway error. Aplicação não está respondendo corretamente (no tempo correto)
Erro pode estar no servidor da aplicação ou no banco de dados

Usar o HTTP-Header X-Forwarded-For para  capturar o IPV4 do usuário dentro da aplicação.
