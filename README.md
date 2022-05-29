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


- Marque as opções [ACLs enabled] e [Object writer]
![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-bucket-1.png) 

- Mais abaixo, em <b>Bucket Versioning</b> marque a opção [Enable]
![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-bucket-2.png)

- Desça a barra de rolagem para baixo e clique em [Create bucket]
![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-bucket-3.png)


- Ainda nas definições da bucket criada, na guia <b>[Management]</b>, clique em <b>[Create lifecycle rule]</b>
![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-bucket-4.png)

- Na tela de configurações do lifecycle, em <b>Choose a rule scope</b>, selecione a opção <b>Apply to all objects in the object</b> conforme imagem abaixo
![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-bucket-retencao-3.png)

- Desça a barra de rolagem para baixo e em <b>Lifecycle rule actions</b> selecione a opção
- [x] Permanently delete noncurrent versions of objects
Logo abaixo, em <b>Permanently delete noncurrent versions of objects</b> defina as os valores das propriedades de acordo com as suas necessidades, nesse exemplo, determinei manter 3 versões dos objetos por um período de 30 dias cada versão. 
![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-bucket-6.png)

```
Nota: Vale lembrar que, já possuímos todo o conteúdo do site no github em uma ou mais branchs.
```

Ainda em S3, crie uma nova bucket com o mesmo nome alterando o sufixo, acrescente <b>-log</b> 
Exemplo: <b>www-xpto.techroute.com.br-log</b>, nesse momento, não será necessário tornar essa bucket pública, mas defina as configurações de <b>Object Owership</b> como <b>[ACLs enabled]</b> e <b>[Object writer]</b>

- Na console da AWS busque por <b>CloudFront</b>

![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-cloudfront-1.png)

- Nas definições/configurações do CloudFront clique em <b>[Create distribution]</b>

![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-cloudfront-2.png)

- Em <b>Origin domain</b> busque e selecione a bucket que foi criada em passos anteriores.

![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-cloudfront-3.png)

- Desça a barra de rolagem para baixo, selecione a opção <b>Yes use OAI (bucket can restrict access to only CloudFront</b> clique em [<b>Create new OAI</b>] e por fim marque a opção <b>Yes, update the bucket policy</b>

![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-cloudfront-4.png)


![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-cloudfront-5.png)

- Em <b>Default cache behavior</b> em <b>Viewer</b> selecione a opção <b>GET, HEAD</b>

![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-cloudfront-6.png)

- Mais abaixo, em <b>Settings</b> selecione o certificado SSL Wilcard correspondente ao domínio que está trabalhando.

![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-cloudfront-7.png)

- Desça a barra de rolagem para baixo e preencha os campos conforme image abaixo:

- Em <b>Default root object - optional</b> informe o nome do objeto que corresponde as requisições do site em "/"

- Em <b>Standard logging</b> marque a opção <b>On</b> e selecione uma bucket que armazenará os logs do CloudFront, por fim no campo <b>Description - optional</b> adicione uma breve descrição para identificar com a facildade essa distribuição de CDN.

![alt text](https://s3.amazonaws.com/public.techroute.com.br/imagens/create-cloudfront-8.png)

- Ainda nas configurações do CloudFront 