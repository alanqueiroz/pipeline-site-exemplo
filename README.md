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
- Crie uma bucket S3, no exemplo a seguir criei a bucket www-xpto.techroute.com.br.<p> 


Marque as opções [ACLs enabled] e [Object writer]
![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-bucket-1.png) 

Logo mais abaixo, em <b>Bucket Versioning</b> marque a opção [Enable]
![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-bucket-2.png)

Desça a barra de rolagem para baixo e clique em [Create bucket]
![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-bucket-3.png)


Ainda nas definições da bucket criada, na guia <b>[Management]</b>, clique em <b>[Create lifecycle rule]</b>
![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-bucket-4.png)

Na tela de configurações do lifecycle, em <b>Choose a rule scope</b>, selecione a opção <b>Apply to all objects in the object</b> conforme imagem abaixo
![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-bucket-5.png)

Desça a barra de rolagem para baixo e em <b>Lifecycle rule actions</b> selecione a opção
- [x] Permanently delete noncurrent versions of objects
Logo abaixo, em <b>Permanently delete noncurrent versions of objects</b> defina as os valores das propriedades de acordo com as suas necessidades, nesse exemplo, determinei manter 3 versões dos objetos por um período de 30 dias cada versão. 
![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-bucket-6.png)

```
Nota: Vale lembrar que, já possuímos todo o conteúdo do site no github em uma ou mais branchs.
```

- Na console da AWS busque por <b>CloudFront</b> ![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-cloudfront-1.png)

Nas definições/configurações do CloudFront clique em <b>[Create distribution]</b>
![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-cloudfront-2.png)