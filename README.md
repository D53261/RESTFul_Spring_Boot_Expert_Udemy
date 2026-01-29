## Parte 5 do Curso: Spring Boot Expert: JPA, REST, JWT, OAuth2 com Docker e AWS
Aqui estão apresentados os códigos usados durante a realização do curso da plataforma Udemy com nome mencionado acerca de uma sessão: Desenvolvimento de API's RestFul.

<hr></hr>

## Desenvolvendo API's RestFul com Spring Boot e JPA

Neste projeto temos os códigos reutilizados de sessões anteriores do curso, mas desta vez focados em construção de API's RestFul utilizando Spring Boot e JPA para persistência de dados. A arquitetura do projeto é organizada em camadas, cada uma com responsabilidades específicas, facilitando a manutenção e escalabilidade da aplicação.

## 1. Controllers
Camada responsável por expor os endpoints REST da aplicação. As classes nesta camada são anotadas com @RestController e mapeiam as requisições HTTP para métodos específicos. Exemplos: AutorController, BookController, etc.

## 2. Organização por camadas
Cada parte do projeto é interligada para dar vida a transição de dados entre o banco e a aplicação, começando pelas ja comentadas Entity -> Repository -> Service -> Controller:
* **Models (Entities)**: Representam as tabelas do banco de dados. Cada classe é anotada com @Entity e define os atributos que correspondem às colunas da tabela.
* **Repository**: Interfaces que estendem JpaRepository para realização interna de operações no banco de dados, fornecendo métodos para operações CRUD e consultas customizadas.
* **Service**: Classes que contêm a lógica de negócio da aplicação. Elas utilizam os repositórios para interagir com o banco de dados e são anotadas com @Service.
* **Controller**: Camada que expõe os endpoints REST, recebendo requisições HTTP e delegando a lógica de negócio para os serviços, assim realizando a utilização de alguns verbos HTTP mais conhecidos como:
    - GET: Recuperar dados.
    - POST: Criar novos registros.
    - PUT/PATCH: Atualizar registros existentes.
    - DELETE: Remover

## 3. DTOs (Data Transfer Objects)
Para evitar expor diretamente as entidades do banco de dados, utilizamos DTOs para transferir dados entre a camada de controle e o cliente. Isso ajuda a manter a segurança e a integridade dos dados.

## 4. Contratos de API
Aprendemos sobre como funciona a implementação de API's em um ambiente real de desenvolvimento, precisando seguir padrões especificos (como as mensagens referentes a erros no Response da operação) para que o cliente consiga interpretar corretamente as respostas da API.

## 5. Tratamento de Exceções
Seguimos os padrões de contrato para tratar os erros como devem ser, criando DTO's que representam as partes da mensagem final, criamos exceções personalizadas como RegistroDuplicadoEsception.java, utilizamos try cacth para receber o erro, usamos classes personalizadas para verificações minuciosas (AutorValidator.java) e criamos as mensagens com base em seus DTO's, melhorando a experiência do usuário.

## 6. Configurações
A pasta de config contém classes e arquivos responsáveis por configurar aspectos essenciais do projeto, como conexão com o banco de dados, propriedades do JPA, e outras definições globais.

### Exemplo de configurações comuns:

* application.yml: Define propriedades como URL do banco (ex.: PostgreSQL), usuário, senha, JPA settings (show-sql, ddl-auto), etc.
* Classes com @Configuration: Permitem criar beans personalizados, como DataSource, e configurar aspectos como encoding e compilação.

Essas configurações tornam o projeto flexível e adaptável a diferentes ambientes e necessidades.

<hr></hr> 
Este projeto conectando todas estas partes mencionadas, configura uma API RestFul completa e com funcionalidades especiais que fazem a comunicação cliente-servidor ser rápida e produtiva, ligando todas as partes (entity, repository, services, controllers e config) corretamente e evitando problemas de conexão.

## Como Executar
- **Pela IDE (IntelliJ)**: Execute a classe principal `Application.java` anotada com `@SpringBootApplication`.
- **Pela Linha de Comando (Windows)**:
    - Construir: `mvn clean package`
    - Rodar: `mvn spring-boot:run`
- **Executar Testes**: `mvn test`

## Configurações Úteis (Exemplo em `src/main/resources/application.yml`)
- `spring.datasource.url=jdbc:postgresql://localhost:5432/library` (para PostgreSQL via Docker).
- `spring.jpa.show-sql=true`
- `spring.jpa.properties.hibernate.format_sql=true`
- `spring.jpa.hibernate.ddl-auto=update` (ou `create-drop` para testes).

## Configuração com Docker
- **Criar Rede Docker**: `docker network create library-network`
- **Rodar PostgreSQL**: `docker run --name librarydb -p 5432:5432 -e POSTGRES_PASSWORD=postgres -e POSTGRES_USER=postgres -e POSTGRES_DB=library --network library-network postgres:16.3`
- **Rodar pgAdmin**: `docker run --name pgadmin4 -p 15432:80 -e PGADMIN_DEFAULT_EMAIL=admin@admin.com -e PGADMIN_DEFAULT_PASSWORD=admin dpage/pgadmin4:8.9`

## Visão Geral dos Conceitos e Termos Importantes de API's RestFul
- **REST (Representational State Transfer)**: Estilo arquitetural para sistemas distribuídos, utilizando HTTP.
- **Endpoints**: URLs que representam recursos na API, normalmente ligados as requisições e suas estruturas.
- **Status Codes HTTP**: Códigos que indicam o resultado da requisição (ex.: 200 OK, 201 Created, 400 Bad Request, 404 Not Found, 500 Internal Server Error).
- **Path Variables e Query Parameters**: Formas de passar dados na URL de forma segura em endpoints onde isso é preciso.
- **DTOs (Data Transfer Objects)**: Objetos usados para transferir dados entre camadas, evitando expor diretamente as entidades do banco.
- **CRUD Operations**: Operações básicas de Create, Read, Update, Delete.
- **Exception Handling**: Mecanismos para capturar e tratar erros, garantindo respostas claras

## Caso encontre códigos confusos neste projeto
- Revise os outros projetos postados em meu GitHub relacionados ao curso Spring Boot Expert, provavelmente a explicação mais detalhada estará lá.
- Consulte a documentação oficial do Spring Boot e Spring Data JPA.

## Dicas para Estudo e Experimentação
- Ative `spring.jpa.show-sql=true` e observe SQLs gerados.
- Experimente diferentes estratégias de mapeamento JPA (@OneToMany, @ManyToOne, etc.).
- Teste endpoints com Postman ou Insomnia
- Crie testes com H2.

## Recursos Adicionais
- [Documentação do Spring Boot](https://spring.io/projects/spring-boot)
- [Documentação do Spring Data JPA](https://spring.io/projects/spring-data-jpa)
- [PostgreSQL](https://www.postgresql.org/)

## Feito por:
### Danilo Ribeiro
### Linkedin: https://www.linkedin.com/in/danilo-ribeiro-catroli-da-silva/
### Email: danilo051007@gmail.com
