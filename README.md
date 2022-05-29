# Pipeline Site Exemplo - www-xtpo.techroute.com.br - Readme em construção
Descrever passo a passo, a instrução para criação de um pipeline na AWS, de um site estático (HTML, CSS e JavaScript) de exemplo, que tem como proposta a arquitetura abaixo:

![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/Arquitetura_SITE_XPTO-TECHROUTE.png)

- <b>Abrangência</b>:
    - Aplica-se a criação de pipeline de qualquer site estático (HTML, CSS e JavaScript) que tenha como objetivo sua infraestrutura na Cloud AWS.
- <b>Pré-requisitos</b>:
    - Acesso a console da AWS com privilégios administrativos
    - Conhecimentos em administração/criação de recursos na AWS
    - Bucket S3 - Para armazenamento do conteúdo do site
    - CloudFront - Para distribuição rápida do conteúdo nas regiões da AWS
    - Route53 - Para resolução de nomes
    - CodeBuild - Para o projeto de compilação do site
    - CodePipeline - Para automação da entrega contínua
    - Certificate Manager - Para uso de certificado SSL válido
    - AWS Backup - Para backup do conteúdo da bucket S3
    - Grafana - Para dashboad
- <b>Justificativas de uso</b>:
    - Oferecer atualizações rápidas, confiáveis, automatizar a fase de compilação e implantação sempre que ocorrer mudanças no código, sem que haja a necessidade de alocação de um profissional de infraestrutura, diminuir o custo operacional e tornar o ambiente mais resiliente.

<b>Descrição</b><p>
* Crie uma bucket S3, no exemplo a seguir criei a bucket www-xpto.techroute.com.br.<p> 
 <b>Observação</b>: {c:red}Não definir como pública, pois o conteúdo será acessível pelo CloudFront.{/c}<p>
* Habilite a opção ACLOwnership, na guia Permissions na bucket para que seja possível aplicar ACLs em objetos.
