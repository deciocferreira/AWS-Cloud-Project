A solução proposta consiste em um ambiente AWS com diversos componentes para garantir a escalabilidade, alta disponibilidade e segurança do sistema Moodle.

O Auto Scaling Group (ASG) é responsável por gerenciar a quantidade de instâncias EC2 necessárias para atender a demanda dos usuários de forma escalável. As instâncias EC2 são do tipo t3.large e possuem um volume EBS de 50GB cada para armazenar os dados do sistema operacional e da aplicação Moodle.

O Amazon RDS Multi-AZ é utilizado como banco de dados principal do Moodle, garantindo a alta disponibilidade e durabilidade dos dados. O RDS é configurado com backup automático diário e retenção por um período de 7 dias.

Para o armazenamento dos arquivos de imagens e vídeos, foi criado um Bucket S3 configurado para replicação em diferentes regiões da AWS, permitindo alta disponibilidade e baixa latência de acesso aos arquivos.

A distribuição de conteúdo é feita através do Amazon CloudFront, que garante a baixa latência no acesso aos arquivos e também atua como um firewall para proteger o ambiente.

O Security Group (SG) é responsável por controlar o acesso aos recursos da solução, permitindo apenas o tráfego necessário entre os diferentes componentes.

A solução utiliza o Amazon CloudWatch para monitoramento dos recursos e métricas de desempenho, garantindo que a aplicação esteja sempre disponível e performática.

Para garantir a segurança do ambiente, foi adicionado o AWS WAF, que protege a aplicação contra ataques web comuns, como injeções de SQL e cross-site scripting.

A atualização da plataforma Moodle pode ser feita de forma simples através do lançamento de uma nova imagem AMI que contenha a versão atualizada do Moodle. O ASG irá automaticamente iniciar novas instâncias com a nova versão e descartar as antigas, sem afetar a disponibilidade da aplicação.

Em resumo, a solução proposta utiliza diversos componentes da AWS para garantir a escalabilidade, alta disponibilidade e segurança do ambiente Moodle, permitindo que o sistema seja facilmente atualizado e mantido performático através de monitoramento constante.
