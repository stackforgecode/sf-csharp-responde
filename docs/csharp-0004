# Exemplo de consulta com query sql em comparação com LINQ e análise de desempenho

<a href="https://github.com/stackforgecode/sf-csharp-responde/blob/main/README.md" style="position: sticky;">Voltar</a>

Vamos supor que você tem uma tabela chamada "produtos" com as seguintes colunas: "id" (int), "nome" (varchar), "preco" (decimal) e "estoque" (int). 

Aqui está um exemplo de consulta com SQL e com LINQ em C#:

SQL:
```
SELECT nome, preco FROM produtos WHERE estoque > 0;
```

LINQ:
```csharp
var produtos = dbContext.Produtos.Where(p => p.Estoque > 0).Select(p => new { p.Nome, p.Preco }).ToList();
```

Para realizar um benchmark das duas consultas, você pode medir o tempo de execução de cada uma delas usando a classe `Stopwatch` do namespace `System.Diagnostics`. 

Por exemplo:

```csharp
var stopwatch = new Stopwatch();
stopwatch.Start();

// Consulta SQL aqui

stopwatch.Stop();
Console.WriteLine("Tempo de execução da consulta SQL: " + stopwatch.ElapsedMilliseconds + "ms");

stopwatch.Reset();
stopwatch.Start();

// Consulta LINQ aqui

stopwatch.Stop();
Console.WriteLine("Tempo de execução da consulta LINQ: " + stopwatch.ElapsedMilliseconds + "ms");
```

Lembre-se de que o tempo de execução pode variar dependendo do tamanho da tabela, do índice utilizado e de outras condições de ambiente. Portanto, é importante realizar vários testes para obter uma medida mais precisa.

------

## Tomando uma entidade do tipo DAO como exemplo

Supondo que você tenha uma classe DAO para sua entidade "Produto", aqui está um exemplo de consulta SQL e LINQ para obter a lista de produtos com estoque maior que zero:

SQL:
```sql
SELECT * FROM produtos WHERE estoque > 0;
```

C# com ADO.NET e SQL:

```csharp
using (SqlConnection connection = new SqlConnection(connectionString))
{
    connection.Open();
    using (SqlCommand command = new SqlCommand("SELECT * FROM produtos WHERE estoque > 0", connection))
    {
        using (SqlDataReader reader = command.ExecuteReader())
        {
            while (reader.Read())
            {
                Produto produto = new Produto();
                produto.Id = Convert.ToInt32(reader["id"]);
                produto.Nome = reader["nome"].ToString();
                produto.Preco = Convert.ToDecimal(reader["preco"]);
                produto.Estoque = Convert.ToInt32(reader["estoque"]);
                produtos.Add(produto);
            }
        }
    }
}
```

C# com LINQ to SQL:
```csharp
using (var context = new MeuDataContext(connectionString))
{
    var produtos = (from p in context.Produtos
                    where p.Estoque > 0
                    select p).ToList();
}
```

Para realizar o benchmark, você pode usar o mesmo código que o exemplo anterior. Aqui está um exemplo com a consulta SQL:
```csharp
var stopwatch = new Stopwatch();
stopwatch.Start();

using (SqlConnection connection = new SqlConnection(connectionString))
{
    connection.Open();
    using (SqlCommand command = new SqlCommand("SELECT * FROM produtos WHERE estoque > 0", connection))
    {
        using (SqlDataReader reader = command.ExecuteReader())
        {
            while (reader.Read())
            {
                Produto produto = new Produto();
                produto.Id = Convert.ToInt32(reader["id"]);
                produto.Nome = reader["nome"].ToString();
                produto.Preco = Convert.ToDecimal(reader["preco"]);
                produto.Estoque = Convert.ToInt32(reader["estoque"]);
                produtos.Add(produto);
            }
        }
    }
}

stopwatch.Stop();
Console.WriteLine("Tempo de execução da consulta SQL: " + stopwatch.ElapsedMilliseconds + "ms");
```

E aqui está um exemplo com a consulta LINQ to SQL:
```csharp
var stopwatch = new Stopwatch();
stopwatch.Start();

using (var context = new MeuDataContext(connectionString))
{
    var produtos = (from p in context.Produtos
                    where p.Estoque > 0
                    select p).ToList();
}

stopwatch.Stop();
Console.WriteLine("Tempo de execução da consulta LINQ to SQL: " + stopwatch.ElapsedMilliseconds + "ms");
```

-----

<a href="https://github.com/stackforgecode/sf-csharp-responde/blob/main/README.md" style="position: sticky;">Voltar</a>

Lembre-se de que o tempo de execução pode variar dependendo do tamanho da tabela, do índice utilizado e de outras condições de ambiente. Portanto, é importante realizar vários testes para obter uma medida mais precisa.

