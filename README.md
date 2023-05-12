# AWS Cloud Project <image src="https://user-images.githubusercontent.com/12403699/234434276-e7cdcab8-c594-47a6-8862-7645e5740a2c.png" width="80" height="50">  
  
## Proposta de arquitetura para migração de uma plataforma de educação para AWS.
  
1. *Banco de Dados*
  
- MySQL RDS (Relational Database Service) com a configuração **db.r5.large**, que possui **2 vCPUs e 16 GB** de memória RAM. Adicionar opção de Multi-AZ.
- Backups diários automatizados do banco de dados.
  
  > Desta forma teremos a replicação automática de dados para um banco de dados standby e backups contínuos em uma zona de disponibilidade diferente para garantir a alta disponibilidade e tolerância a falhas.
  
2. *Aplicação*
  
- Instâncias EC2 (Elastic Compute Cloud) do tipo **t3.large** com **2 vCPUs e 8 GB de RAM**, sistema operacional Linux e o AMI (Amazon Machine Image) do Moodle, que já inclui o PHP e o Apache, necessários para executá-lo.
- Armazenamento será um volume EBS (Elastic Block Store) de 50 GB para os arquivos da aplicação e do sistema operacional em cada instância, um Bucket S3 para os arquivos estáticos e de mídia e outro para guardar os logs do CloudFront.
- Auto Scaling com o mínimo de 1, desejado de 2 e o máximo de 4 instâncias com triggers de adicão de novas instâncias EC2 ao grupo quando a CPU ou a memória RAM atingir um determinado limite.
- Load Balancer do tipo Application Load Balancer para distribuir o tráfego entre as instâncias EC2 do Moodle. 
- Utilizar o Amazon CloudFront para distribuir os conteúdos estáticos (imagens e vídeos) da aplicação.
  
  > Isso permitirá que a infraestrutura se adapte automaticamente à demanda de acesso, escalando ou reduzindo o número de instâncias, mantendo a estabilidade e evitando quedas do sistema garantindo a alta disponibilidade da aplicação. Uma vez que alguma instância apresente problemas, outras continuarão respondendo às requisições tolerando picos de acesso imprevistos pelo cliente. O conteúdo vai ficar em diversos pontos de presença, garantindo assim uma maior rapidez no acesso aos recursos pelos usuários finais.
  
3. *Segurança*
  
- Grupos de segurança no RDS e outro no EC2.
- AWS WAF (Web Application Firewall).
- AWS Shield.
  
  >  Assim aplicamos camadas de segurança para permitir apenas as conexões necessárias para o Moodle operar. Protegemos ele contra ataques na camada de aplicação, como injeção de SQL ou cross-site scripting (XSS) e contra ataques DDoS (Distributed Denial of Service).
  
4. *Monitoramento e deploy*
  
- Amazon CloudWatch.
- Amazon CloudTrail.
- Elastic Beanstalk.
  
  > Desta forma, teremos toda a infraestrutura monitorada, podendo enviar alertas em caso de problemas. Registro das ações realizadas nos serviços da AWS, tendo uma visão mais detalhada e em tempo real do que está acontecendo. Capacidade de identificar possíveis falhas de segurança ou atividades suspeitas. Também simplificamos o processo de deploy e gerenciamento da aplicação do Moodle no ambiente, incluindo testes, autalizações e versão e homologação.
  
## Arquitetura do ambiente  
  
<image src="https://github.com/deciocferreira/AWS-Cloud-Project/assets/12403699/79215028-8898-4566-abc9-6d6a6f7de769" width="750" height="700">  
 
## Resultados esperados
  
- Redução de custos com infraestrutura e manutenção de servidores;
  
- Maior escalabilidade e flexibilidade para lidar com picos de tráfego e demanda;
  
- Facilidade na implementação de novas funcionalidades e atualizações do sistema;
  
- Melhor desempenho e tempo de resposta para os usuários;
  
- Aumento da segurança e proteção dos dados do sistema;
  
- Melhor visibilidade e monitoramento do ambiente, permitindo uma resposta mais rápida a problemas e falhas.   
  
- Alta disponibilidade: a arquitetura proposta utiliza vários recursos e técnicas para garantir alta disponibilidade. O uso do Amazon ECS e Auto Scaling garante que a aplicação esteja sempre disponível, mesmo em caso de falhas em uma ou mais instâncias. Além disso, o uso de múltiplas zonas de disponibilidade e balanceamento de carga distribui o tráfego de forma equilibrada, reduzindo a chance de interrupções no serviço.

-  Escalabilidade: a arquitetura proposta é altamente escalável, permitindo que a aplicação cresça de forma elástica de acordo com as necessidades de negócios. O Amazon ECS e o Auto Scaling garantem que o número de instâncias possa aumentar ou diminuir automaticamente, conforme necessário, sem afetar a disponibilidade ou o desempenho.

- Segurança: a arquitetura proposta também é projetada para ser segura. A utilização de várias camadas de segurança, como VPC, grupos de segurança e SSL, reduz a possibilidade de ataques e invasões maliciosas.

- Monitoramento: a arquitetura proposta é altamente monitorada, permitindo uma visão clara do desempenho e saúde da aplicação. O uso de ferramentas de monitoramento, como o Amazon CloudWatch e o Amazon S3, garante que os dados estejam sempre disponíveis e acessíveis para a análise e tomada de decisões.

- Backup e Recuperação de Desastres: A arquitetura proposta inclui uma estratégia de backup e recuperação de desastres, permitindo a restauração rápida da aplicação em caso de falhas ou desastres. O uso do Amazon RDS com replicação em várias zonas e a utilização de snapshots garantem a disponibilidade dos dados e uma recuperação rápida em caso de falhas.
