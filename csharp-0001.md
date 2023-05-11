# As diferenças entre classes do tipo POCO, DAO e DTO em C#

Em C#, POCO, DAO e DTO são padrões de projeto comumente usados em aplicações de software. Eles têm papéis diferentes e podem ser usados ​​em conjunto para fornecer um design robusto e escalável para o seu software.

- POCO: Plain Old CLR Object (Objeto CLR simples e comum) é um padrão de projeto que é usado para representar objetos de negócios em um aplicativo. Eles são objetos simples que não possuem nenhuma lógica de negócios, nenhuma dependência de infraestrutura e nenhuma herança de classes complexas. Eles geralmente são usados ​​como entidades do banco de dados ou como objetos de transferência de dados (DTOs). Em resumo, eles são apenas objetos que representam dados de uma forma que faz sentido para a lógica do negócio.

- DAO: Data Access Object (Objeto de Acesso a Dados) é um padrão de projeto que é usado para encapsular a lógica de acesso a dados em uma classe separada. Isso ajuda a separar a lógica de negócios da lógica de acesso a dados e torna mais fácil manter e testar seu aplicativo. Geralmente, uma classe DAO contém métodos que lidam com operações de banco de dados, como inserção, atualização e exclusão de registros.

- DTO: Data Transfer Object (Objeto de Transferência de Dados) é um padrão de projeto que é usado para transferir dados entre camadas ou sistemas diferentes. Eles são objetos simples que contêm apenas os dados que precisam ser transferidos e não contêm nenhuma lógica de negócios ou acesso a dados. DTOs são frequentemente usados ​​para transferir dados entre a camada de negócios e a camada de apresentação em um aplicativo.

Em resumo, POCOs são objetos de negócios simples que representam dados, DAOs são usados ​​para encapsular a lógica de acesso a dados e DTOs são usados ​​para transferir dados entre diferentes camadas do aplicativo. Todos eles trabalham juntos para fornecer um design robusto e escalável para seu aplicativo.

Seguem alguns exemplos de código em C# que ilustram como usar POCO, DAO e DTO:

1. Exemplo de classe POCO:
```
public class Customer
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
}
```
Neste exemplo, a classe Customer é um objeto simples que representa um cliente. Ele contém apenas as propriedades necessárias para representar um cliente, sem nenhuma lógica de negócios.

2. Exemplo de classe DAO:
```
public class CustomerDao
{
    private readonly IDbConnection _connection;

    public CustomerDao(IDbConnection connection)
    {
        _connection = connection;
    }

    public Customer GetById(int id)
    {
        var sql = "SELECT * FROM Customers WHERE Id = @Id";
        return _connection.Query<Customer>(sql, new { Id = id }).FirstOrDefault();
    }

    public void Save(Customer customer)
    {
        var sql = "INSERT INTO Customers (Name, Email) VALUES (@Name, @Email)";
        _connection.Execute(sql, customer);
    }
}
```
Neste exemplo, a classe CustomerDao encapsula a lógica de acesso a dados para a tabela Customers no banco de dados. Ele contém métodos para recuperar um cliente pelo ID e salvar um novo cliente.

3. Exemplo de classe DTO:
```
public class CustomerDto
{
    public string Name { get; set; }
    public string Email { get; set; }
}
```
Neste exemplo, a classe CustomerDto é um objeto simples que contém apenas as propriedades necessárias para transferir dados de clientes entre camadas ou sistemas diferentes.

-----------
Espero que esses exemplos ajudem a ilustrar como POCO, DAO e DTO podem ser usados em conjunto em um aplicativo C# para fornecer um design robusto e escalável.
