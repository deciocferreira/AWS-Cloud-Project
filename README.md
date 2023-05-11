# AWS-Cloud-Project <image src="https://user-images.githubusercontent.com/12403699/234434276-e7cdcab8-c594-47a6-8862-7645e5740a2c.png" width="80" height="50">  
  
## Proposta de arquitetura para migração de uma plataforma de educação para AWS.
  
1. *Banco de Dados*
  
- Criação de um banco de dados MySQL RDS (Relational Database Service) com a configuração db.r5.large, que possui 2 vCPUs e 16 GB de      memória RAM para garantir a alta disponibilidade e tolerância a falhas.
- Configurar o RDS com a opção de Multi-AZ, permitindo a replicação automática de dados para um banco de dados standby em uma zona de disponibilidade diferente. 
- Configurar backups diários automatizados do banco de dados.
  
2. *Aplicação*
  
- Criar uma instância EC2 (Elastic Compute Cloud) do tipo t3.large com o sistema operacional Linux e o AMI (Amazon Machine Image) do    Moodle, que já inclui o PHP e o Apache, necessários para rodar o Moodle.
- Anexar um volume EBS (Elastic Block Store) de 200 GB para armazenar os arquivos da aplicação e do sistema operacional.
- Configurar o Auto Scaling, com o mínimo de 1, o desejado de 2 e o máximo de 4 instâncias EC2. Isso permitirá que a infraestrutura   se adapte automaticamente à demanda de acesso do sistema, escalando ou reduzindo o número de instâncias de acordo com a demanda,  ajudando a manter a estabilidade e evitar quedas do sistema.
- Utilizar um Load Balancer do tipo Application Load Balancer para distribuir o tráfego entre as instâncias EC2 do Moodle. Isso       garantirá a alta disponibilidade da aplicação, uma vez que caso alguma instância apresente problemas, as outras continuarão respondendo às requisições.
- Configurar o Auto Scaling para adicionar novas instâncias EC2 ao grupo quando a CPU ou a memória RAM atingir um determinado limite, definido pelo administrador, permitindo atender aos picos de demanda de acesso previstos pelo cliente.
- Utilizar o Amazon CloudFront para distribuir os conteúdos estáticos (imagens e vídeos) da aplicação, permitindo que os mesmos sejam cacheados em diversos pontos de presença (PoPs) em todo o mundo, garantindo assim uma maior rapidez no acesso aos recursos pelos usuários finais.
  
3. *Segurança*
  
- Configurar um grupo de segurança no RDS e outro no EC2 para permitir apenas as conexões necessárias para a operação do Moodle. Por   exemplo, permitir conexões na porta 80 apenas para o Load Balancer, e permitir conexões na porta 22 apenas para os administradores do    sistema.
- Utilizar o AWS WAF (Web Application Firewall) para proteger a aplicação contra ataques na camada de aplicação, como injeção de SQL ou cross-site scripting (XSS).  
- Utilizar o AWS Shield para proteger contra ataques DDoS (Distributed Denial of Service).
  
4. *Monitoramento e deploy*
  
- Configurar o Amazon CloudWatch para monitorar os recursos da infraestrutura, como CPU, memória RAM e tráfego de rede, e enviar   alertas em caso de problemas.
- Utilizar o AWS CodeDeploy para realizar o deploy das atualizações do Moodle. Com essa ferramenta, é possível automatizar o processo   de atualização do sistema, minimizando o tempo de inatividade da aplicação.
- Utilizar o AWS Cloud
  
## Arquitetura do ambiente

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
