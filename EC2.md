# EC2

EC2 = Elastic Compute Cloud, fornece máquinas virtuais, com a possibilidade de redimensionar a capacidade computacional livremente.
Reduz o tempo para ligar e reiniciar as máquinas em minutos.
Paga somente pela capacidade que utilizar

Opções de assinatura:

- Por demanda: permite pagar uma taxa fixa por hora ou até mesmo por segundo, dependendo do S.O escolhido para a instância:
Linux: paga por segundo, Windows: por hora, mas é esperado que mude este modelo de pagamento.
Bom para usuários que desejam baixo custo e flexibilidade, sem ter que pagar adiantado ou assumir compromissos de longo prazo.
Aplicações em desenvolvimento ou testados na AWS pela primeira vez.

- Por reserva: você faz um contrato de 1 ou 3 anos, paga adiantado um parte ou o total do contrato e ganha um considerável desconto pela
hora cobrada da instância.
Bom para aplicações já estáveis, com usabilidade previsível.
Reserved instances agendadas para serem utilizadas num determinado período que você configurar, essa opção permite combinar a capacidade da
máquina com momentos de utilização previsível que só requer parte de um dia, semana ou mês.

- Spot: permite oferecer qualquer valor pela capacidade computacional da instância, gerando ainda mais descontos caso a sua aplicação
tenha horários flexíveis para ligar e desligar.

- Host dedicado: é um servidor EC2 físico, dedicado e ele pode ajudar a reduzir custos, permitindo você utilizar suas licenças
já existentes, por exemplo: VM Ware, Oracle, SQL Server entre outros.
Vantajoso para requirementos regulatórios que não permitem virtualização multi-tenant ( https://www.treinaweb.com.br/blog/o-que-e-uma-aplicacao-multitenant/ ).
Pode ser comprado por demanda, pagando por hora.
Pode ser comprado por reserva, até 70% mais barato que por demanda.

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

