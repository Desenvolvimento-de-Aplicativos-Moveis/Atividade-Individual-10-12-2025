# Atividade-Individual-08-12-2025
Atividade da UC Desenvolvimento de Aplicativos Móveis 2º Semestre de 2025 no Senai utilizando FLutter Flow e API com Java Spring Boot

---


Atividade individual (Continuação)

Telas:
-> Login
-> Cadastro
-> Dados do usuário
-> Tela inicial (Header/Footer/imagem/texto/icone/botão)
-> Tela de endereço (logradouro/localidade/cep/número/complemento/bairro/referência/botão para salvar)

- Complete a documentação já iniciada.
- Pode ser utilizada qualquer API que esteja com deploy no Render;
- No FlutterFlow siga os passos:
--> Crie o API Calls para Cadastro do usuário e Cadastro de endereço, teste pela aba Test e tire prints do cadastro funcionando. Deve ter 3 prints: Call Definition / Response & Test / Aba de Test. Documente.
--> Crie o API Calls para Login e Dados do usuário, teste pela aba Test e tire prints do cadastro funcionando. Deve ter 3 prints para cada: Call Definition / Response & Test / Aba de Test. Documente.

Obs.: Para os que estão na WorldSkills e FTC a data de entrega é dia 08/12.

Entrega:
- Compartilhar o FlutterFlow com debora.souza@docente.firjan.senai.br
- Repositório no GitHub com Readme.md preenchido contendo: título, descrição do projeto, descrição das funcionalidades, tecnologia utilizadas, prints das telas do FlutterFlow, link do deploy do swagger utilizado no consumo, nome do desenvolvedor.
- O Repositório deve estar na organização da UC, compartilhado com debysouza e deve conter dois arquivos: Documentação e Readme.

---


O QUE VOCÊ PRECISA FAZER
1. Preparar sua API para Deploy

Como a atividade exige consumir uma API com deploy no Render:

Suba seu backend Java Spring Boot no Render:

Crie uma conta no Render.

Crie um novo serviço Web Service.

Conecte o repositório do GitHub que contém o seu projeto Spring Boot.

Configure:

Build Command: ./mvnw clean install

Start Command: java -jar target/seu-projeto.jar

Configure variáveis de ambiente se necessário.

Após o deploy, copie a URL da API.

Verifique:

/swagger ou /swagger-ui.html funcionando.

Endpoints de cadastro, login, dados do usuário e endereço funcionando.

Essa URL será usada no FlutterFlow.

2. Configurar o FlutterFlow

Você já tem as telas; agora precisa configurar a lógica.

API Calls necessárias

Você vai criar 4 API Calls:

Cadastro de Usuário

Cadastro de Endereço

Login

Dados do Usuário

Para cada API Call, você deve:

A. Criar a Call

Menu: Settings → API Calls

Informe:

Método (POST/GET)

URL da API do Render

Body (JSON) quando necessário

Headers (Content-Type: application/json)

B. Testar na Aba Test

Você deve produzir 3 prints por API Call:

Call Definition

Response & Test

Aba de Test

E documentar.

3. Documentação

Seu repositório GitHub deve conter dois arquivos:

1. README.md

Com os seguintes requisitos obrigatórios:

Título do projeto

Descrição completa

Funcionalidades

Tecnologias utilizadas

Prints das telas do FlutterFlow

Link do deploy do Swagger

Nome do desenvolvedor

2. Documento de Documentação (PDF ou MD)

Inclui:

Descrição técnica da API consumida

Configuração dos API Calls

Prints das 12 imagens obrigatórias:

3 prints para Cadastro de Usuário

3 prints para Cadastro de Endereço

3 prints para Login

3 prints para Dados do Usuário

Fluxo das telas no FlutterFlow

Explicação da arquitetura (API + FlutterFlow)

4. Entrega

Compartilhar o projeto FlutterFlow com: debora.souza@docente.firjan.senai.br

Repositório deve estar na organização:
Desenvolvimento-de-Aplicativos-Móveis

Conceder acesso aos usuários:

debysouza
