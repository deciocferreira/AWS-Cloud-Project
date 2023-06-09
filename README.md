<p align="center"><image src="https://github.com/deciocferreira/AWS-Cloud-Project/assets/12403699/a8d33565-9ca5-4981-8865-cbd29100785a" width="450" height="350"> 
</p>
  
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
  
- VPC  
- Grupos de segurança no RDS e outro no EC2
- AWS Shield
  
  >  Assim aplicamos camadas de segurança para permitir apenas as conexões necessárias para o Moodle operar. Fora da AWS fica protegido contra ataques na camada de aplicação, como injeção de SQL ou cross-site scripting (XSS) e contra ataques DDoS (Distributed Denial of Service) e dentro abrangindo os elementos, permitindo que eles se comuniquem entre si e com a Internet de forma segura e isolada.
  
4. *Monitoramento e deploy*
  
- Amazon CloudWatch.
- Elastic Beanstalk.
  
  > Desta forma, teremos toda a infraestrutura monitorada, podendo enviar alertas em caso de problemas. Registro das ações realizadas nos serviços da AWS, tendo uma visão mais detalhada e em tempo real do que está acontecendo. Capacidade de identificar possíveis falhas de segurança ou atividades suspeitas. Também simplificamos o processo de deploy e gerenciamento da aplicação do Moodle no ambiente, incluindo testes, autalizações e versão e homologação.
  
## Arquitetura e fluxo do ambiente  
  
<image src="https://github.com/deciocferreira/AWS-Cloud-Project/assets/12403699/1317bdf1-6c7c-4525-84eb-3eb3632ed36e" width="950" height="700"> 
 
- O usuário faz uma requisição para visualizar um vídeo no seu navegador.

- A requisição chega ao Amazon CloudFront, que é um CDN que armazena os arquivos de mídia do site e permite que os usuários acessem esses arquivos com baixa latência.

- O CloudFront verifica se o conteúdo solicitado está em seu cache e, se estiver, o entrega ao usuário. Caso contrário, o CloudFront solicita o arquivo do bucket S3.

- O Amazon S3 armazena os arquivos de mídia e responde à solicitação do CloudFront, fornecendo o vídeo solicitado.

- O CloudFront entrega o arquivo de vídeo ao usuário.

- O Elastic Load Balancer (ALB) direciona a requisição para uma das instâncias EC2 que executam o aplicativo Moodle.

- O Moodle serve o conteúdo de vídeo solicitado ao usuário.

- Durante todo o processo, o Amazon CloudWatch monitora o desempenho da infraestrutura e a saúde das instâncias EC2 e outros recursos.  
 
## Resultados esperados

- Alta disponibilidade;
  
- Maior escalabilidade e flexibilidade para lidar com picos de tráfego e demanda;
  
- Facilidade na implementação de novas funcionalidades e atualizações do sistema;
  
- Melhor desempenho e tempo de resposta para os usuários;
  
- Aumento da segurança e proteção dos dados do sistema;
  
- Melhor visibilidade e monitoramento do ambiente, permitindo uma resposta mais rápida a problemas e falhas.   
  
- Backup e Recuperação de Desastres;

- Redução de custos com infraestrutura e manutenção de servidores.

## Proposta 

Custo mensal: US$ 2,80

Custo anual: US$ 33,60

Calculadora: 
