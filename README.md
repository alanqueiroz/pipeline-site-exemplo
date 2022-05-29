# Pipeline Site Exemplo - www-xtpo.techroute.com.br
Descrever passo a passo, a instrução para criação de um pipeline na AWS,de um site estático (HTML, CSS e JavaScript) de exemplo, que tem como proposta a arquitetura abaixo:

![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/Arquitetura_SITE_XPTO-TECHROUTE.png)

- Abrangência
    Aplica-se a criação de pipeline de qualquer site estático (HTML, CSS e JavaScript) que tenha como objetivo sua infraestrutura na Cloud AWS.
- Pré-requisitos
    - Acesso a console da AWS com privilégios administrativos
    - Conhecimentos em administração/criação de recursos na AWS
    - Bucket S3 - Para armazenamento do conteúdo do site
    - CloudFront - Para distribuição rápida do conteúdo nas regiões da AWS
    - Route53 - Para resolução de nomes
    - CodeBuild - Para o projeto de compilação do site
    - CodePipeline - Para automação da entrega contínua
    - Certificate Manager - Para uso de certificado SSL válido
    - AWS Backup - Para backup do conteúdo da bucket S3   