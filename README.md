# Projeto DAO JDBC (Java Database Connectivity)

Este repositório contém uma implementação completa do padrão de projeto **DAO (Data Access Object)** para gerenciar um sistema simples de vendedores e departamentos. O objetivo principal é demonstrar a integração entre uma aplicação Java e um banco de dados relacional (MySQL) utilizando JDBC puro.

## Tecnologias e Padrões
* **Java 21**: Utilização de recursos modernos da linguagem.
* **MySQL**: Banco de dados relacional para persistência dos dados.
* **JDBC**: API Java para execução de comandos SQL.
* **Padrão DAO**: Desacoplamento entre a lógica de negócio e a persistência de dados.
* **Padrão Factory**: Uso da classe `DaoFactory` para instanciar as implementações dos DAOs, mantendo as dependências ocultas da camada de aplicação.

## Estrutura do Projeto

O projeto está organizado nos seguintes pacotes:
* `db`: Contém a classe utilitária `DB` para gerir conexões e exceções personalizadas como `DbException`.
* `model.entities`: Classes de domínio `Seller` e `Department`.
* `model.dao`: Interfaces que definem o contrato de persistência.
* `model.dao.impl`: Implementações JDBC específicas (`SellerDaoJDBC` e `DepartmentDaoJDBC`).
* `application`: Classes com o método `main` para execução de testes de integração (`Program` e `Program2`).

## Funcionalidades Implementadas

### Vendedores (Seller)
* **findById**: Busca um vendedor e seu respectivo departamento por ID.
* **findByDepartment**: Lista todos os vendedores de um departamento específico.
* **findAll**: Retorna todos os vendedores ordenados por nome.
* **insert**: Insere um novo vendedor e recupera o ID gerado automaticamente.
* **update**: Atualiza os dados de um vendedor existente.

* ### Departamentos (Department)
* Funcionalidades completas de **CRUD** (Inserção, Consulta, Atualização e Deleção).

## ⚙️ Como Configurar

1.  **Banco de Dados**: Execute o script SQL de criação das tabelas `department` e `seller`.
2.  **Propriedades**: Crie ou edite o arquivo `db.properties` na raiz do projeto:
    ```properties
    user=seu_usuario
    password=sua_senha
    dburl=jdbc:mysql://localhost:3306/nome_do_banco?useSSL=false&allowPublicKeyRetrieval=true
    ```
    *Nota: Os parâmetros `useSSL` e `allowPublicKeyRetrieval` são essenciais para conexões com versões recentes do MySQL (8.0+).*

3.  **Execução**:
    * Execute a classe `application.Program` para testar os métodos de vendedor.
    * Execute a classe `application.Program2` para testar os métodos de departamento.

## 🛡️ Tratamento de Erros
O projeto utiliza exceções personalizadas para garantir que erros de banco de dados não exponham detalhes técnicos da infraestrutura para as camadas superiores:
* `DbException`: Para erros gerais de SQL.
* `DbIntegrityException`: Para erros de integridade referencial (ex: apagar um departamento que possui vendedores vinculados).
