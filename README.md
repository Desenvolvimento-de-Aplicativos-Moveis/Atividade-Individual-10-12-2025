# Atividade-Individual-08-12-2025
Atividade da UC Desenvolvimento de Aplicativos Móveis 2º Semestre de 2025 no Senai utilizando FLutter Flow e API com Java Spring Boot

---
## Telas no FLutter Flow:
-> Login
-> Cadastro
-> Dados do usuário
-> Tela inicial (Header/Footer/imagem/texto/icone/botão)
-> Tela de endereço (logradouro/localidade/cep/número/complemento/bairro/referência/botão para salvar)

## Tarefas no FLutter Flow:
--> Crie o API Calls para Cadastro do usuário e Cadastro de endereço, teste pela aba Test e tire prints do cadastro funcionando. Deve ter 3 prints: Call Definition / Response & Test / Aba de Test. Documente.
--> Crie o API Calls para Login e Dados do usuário, teste pela aba Test e tire prints do cadastro funcionando. Deve ter 3 prints para cada: Call Definition / Response & Test / Aba de Test. Documente.

## Entrega:
- Compartilhar o FlutterFlow com debora.souza@docente.firjan.senai.br
- Repositório no GitHub com Readme.md preenchido contendo: título, descrição do projeto, descrição das funcionalidades, tecnologia utilizadas, prints das telas do FlutterFlow, link do deploy do swagger utilizado no consumo, nome do desenvolvedor.
- O Repositório deve estar na organização da UC, compartilhado com debysouza e deve conter dois arquivos: Documentação e Readme.

---
## Descrição do Gemini

Parte 1: Deploy da sua API Spring Boot no Render
O objetivo é ter sua API rodando em uma URL pública (ex: https://minha-api.onrender.com) e conectada a um banco de dados também na nuvem.

1. Crie o Banco de Dados (PostgreSQL)
Antes de publicar sua API, crie o banco de dados que ela vai usar.

No Dashboard do Render, clique em New > PostgreSQL.

Dê um nome (ex: meu-banco-api) e escolha o plano "Free".

Aguarde o banco ser criado. Assim que estiver "Available", vá até ele e role para baixo até "Connections".

Você verá os dados de conexão: Username, Password, Host e Database Name. Mantenha essa aba aberta.

2. Configure sua API Spring Boot (Localmente)
Sua API não pode mais usar um banco local (localhost ou H2). Ela precisa apontar para o banco do Render.

CORS (Cross-Origin Resource Sharing): Este é o passo MAIS IMPORTANTE e o que mais causa erros. O FlutterFlow (rodando em app.flutterflow.io) tentará acessar sua API (rodando em onrender.com). O navegador bloqueará isso por padrão.

Crie uma classe de configuração no seu projeto Spring (ex: CorsConfig.java):

Java

import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class CorsConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**") // Libera todos os endpoints ("/**")
                .allowedOrigins("https://app.flutterflow.io") // Permite requisições do FlutterFlow
                .allowedMethods("GET", "POST", "PUT", "DELETE", "OPTIONS") // Métodos permitidos
                .allowedHeaders("*") // Permite todos os cabeçalhos
                .allowCredentials(true);
    }
}
Commit e Push: Faça o commit dessa nova classe CorsConfig.java e dê push no seu repositório do GitHub.

3. Crie o "Web Service" da API no Render
No Dashboard, clique em New > Web Service.

Conecte seu repositório do GitHub e selecione o repositório da sua API.

Configure os campos:

Name: minha-api (isso será parte da sua URL).

Build Command: Se você usa Maven: mvn clean package -DskipTests. Se usa Gradle: ./gradlew build -x test.

Start Command: Aqui você precisa saber o nome do arquivo .jar que seu build gera.

Maven: java -jar target/nome-do-seu-arquivo-0.0.1-SNAPSHOT.jar

Gradle: java -jar build/libs/nome-do-seu-arquivo-0.0.1-SNAPSHOT.jar (Verifique o nome exato do arquivo .jar na sua pasta target ou build/libs localmente).

Variáveis de Ambiente (Environment Variables): Este é o segundo passo mais importante. É aqui que você conecta sua API ao banco de dados.

Clique em "Add Environment Variable" para CADA uma das linhas abaixo.

Use os dados de conexão do seu banco (Passo 1).

Variável: SPRING_DATASOURCE_URL

Valor: jdbc:postgresql://<Host-do-Passo-1>:5432/<Database-Name-do-Passo-1>

Variável: SPRING_DATASOURCE_USERNAME

Valor: <Username-do-Passo-1>

Variável: SPRING_DATASOURCE_PASSWORD

Valor: <Password-do-Passo-1>

Variável (Recomendado): SPRING_JPA_HIBERNATE_DDL_AUTO

Valor: update (ou validate. Evite create ou create-drop em produção).

Clique em "Create Web Service".

4. Verifique o Deploy
O Render vai agora buscar seu código no GitHub, rodar o "Build Command" e depois o "Start Command".

Vá na aba "Logs" do seu Web Service.

Observe o build. Você deve ver "BUILD SUCCESSFUL" e depois o logo do Spring Boot subindo.

Se der erro, o log mostrará (erros comuns são: não achar o .jar ou não conseguir conectar ao banco).

Quando estiver "Deploy successful", copie a URL pública que o Render lhe deu (ex: https://minha-api.onrender.com).

Teste: Abra https://minha-api.onrender.com/swagger-ui.html (ou o caminho do seu Swagger) no navegador. Você deve ver sua documentação de API. Use o Swagger para testar se o cadastro e o login estão funcionando.

Parte 2: Configuração Detalhada das API Calls no FlutterFlow
Agora que sua API está 100% online e testada no Swagger, vamos ao FlutterFlow.

Vá em API Calls (ícone 🔌).

Crie um Grupo (Opcional, mas recomendado):

Clique em "+ Add" > "API Group".

Nome: Minha API

Base URL: https://minha-api.onrender.com (a URL que você pegou do Render).

Isso economiza tempo, pois você só precisará digitar os endpoints (ex: /login) em cada chamada.

Criando a Chamada (Ex: cadastrarUsuario)

Dentro do grupo, clique em "+ Add API Call".

Name: cadastrarUsuario

Method Type: POST

Endpoint: /usuarios (ou seu endpoint de cadastro). A URL completa será [Base URL] + /usuarios.

Aba "Body"

Selecione JSON.

Vá para a sub-aba "Variables" (logo abaixo de "Body"). Aqui você define o que o FlutterFlow vai perguntar para enviar.

Clique em "+ Add Variable" e crie (ex: nome, email, senha). Deixe-os como tipo String.

Volte para a sub-aba "JSON". Monte o corpo (body) que sua API espera, usando as variáveis que você acabou de criar:

JSON

{
  "nome": "<nome>",
  "email": "<email>",
  "senha": "<senha>"
}
Aba "Response & Test"

É aqui que você tira os prints.

Print 3 (Aba de Test): Vá para a sub-aba "Test". Preencha os valores das variáveis (ex: nome = "Usuário Teste", email = "teste@email.com", senha = "123"). Clique em "Test API Call".

Print 2 (Response & Test): Se tudo der certo (graças ao CORS!), você verá "Status Code: 200" (ou 201) e o "Response Body" (o JSON que sua API retornou). Tire o print desta tela agora.

Aba "Call Definition"

Print 1 (Call Definition): Volte para a primeira aba, "Call Definition", que agora está toda preenchida. Tire o print dela.

Repita esse processo para as 4 chamadas.

Ponto Crítico: Chamada "Dados do Usuário" (com Autenticação)
Esta chamada (provavelmente GET /usuarios/me ou GET /usuarios/{id}) precisa de um Token de autenticação.

Na "Call Definition":

Vá para a aba "Headers".

Adicione um Header: Accept: application/json

Adicione outro Header: Authorization: Bearer <token>

Mas como pegar o <token>?

Vá na aba "Variables" (as variáveis da própria chamada, não do "Body").

Crie uma variável chamada authToken (tipo String).

Volte nos Headers e mude o valor do Authorization para: Bearer <authToken> (arrastando a variável authToken para lá).

No "Response & Test":

Para testar essa chamada, você precisará de um token válido.

Vá na sua API Call de Login, execute um teste e copie o token que ela retorna.

Volte na chamada "Dados do Usuário", aba "Test", e cole o token no campo da variável authToken.

Clique em "Test API Call". Agora deve funcionar.

Parte 3: Documentação e Entrega
Documentação (Arquivo separado):

Crie seções para "Cadastro Usuário", "Login", etc.

Para cada seção, cole os 3 prints pedidos:

Print da "Call Definition" (mostrando URL, Endpoint, e o Body se houver).

Print da "Response & Test" (mostrando o Status 200 e o JSON de resposta).

Print da sub-aba "Test" (mostrando os dados que você inseriu para o teste).

Isso totalizará 12 prints (4 chamadas x 3 prints).

Readme.md (Arquivo principal):

Aqui você coloca o link do seu Swagger (ex: https://minha-api.onrender.com/swagger-ui.html).

Coloque os prints das telas do FlutterFlow (as 5 telas prontas).

Preencha o resto (tecnologias, descrição, etc.).

Seguindo este guia, os pontos que mais geram problemas (CORS, Variáveis de Ambiente do Banco, e teste de chamadas autenticadas) estarão cobertos.
Repositório deve estar na organização:
Desenvolvimento-de-Aplicativos-Móveis

Conceder acesso aos usuários:

debysouza
