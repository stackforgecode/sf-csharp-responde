# Desenvolvimento C# 11: quais as diferenças entre HttpClient e HttpClientFactory

> Vamos lembrar que, independente da linguagem, tudo depende de como utilizamos e preparamos um determinado serviço

<a href="https://github.com/stackforgecode/sf-csharp-responde/blob/main/README.md" style="position: sticky;">Voltar</a>




HttpClient é uma classe disponível na biblioteca padrão do .NET que permite fazer chamadas HTTP para servidores. Já HttpClientFactory é uma classe que foi introduzida no .NET Core 2.1 para gerenciar a criação de instâncias de HttpClient.

A seguir, as principais diferenças entre essas duas classes:

1. Gerenciamento de recursos: Quando usamos a classe HttpClient diretamente, devemos gerenciar a instância manualmente, o que pode levar a vazamentos de recursos, como conexões TCP. Por outro lado, o HttpClientFactory gerencia as instâncias de HttpClient para nós, garantindo que as conexões sejam fechadas corretamente.

2. Performance: O uso do HttpClientFactory pode melhorar a performance do aplicativo, pois ele reutiliza as conexões TCP já existentes, em vez de criar uma nova conexão para cada chamada HTTP.

3. Configuração: O HttpClientFactory oferece a possibilidade de configurar instâncias de HttpClient de forma mais fácil e centralizada, o que é útil em aplicativos maiores com várias chamadas HTTP. Ele permite, por exemplo, definir headers, timeout e política de retry.

4. Testabilidade: Com o HttpClientFactory, é mais fácil escrever testes unitários, pois ele permite a injeção de dependência de uma interface IHttpClientFactory, que pode ser facilmente mockada para testes.

Os riscos de usar a classe HttpClient diretamente incluem a falta de gerenciamento de recursos, o que pode levar a vazamentos de memória e conexões, e a necessidade de configurar instâncias manualmente.

Em resumo, o uso do HttpClientFactory oferece vantagens em termos de gerenciamento de recursos, performance, configuração e testabilidade, e é altamente recomendado para aplicativos que fazem chamadas HTTP.

---

## Vamos aos Códigos

Aqui está um exemplo de como usar a classe HttpClient diretamente para fazer uma chamada HTTP:

```csharp
using System.Net.Http;

class Program
{
    static async Task Main(string[] args)
    {
        var client = new HttpClient();
        var response = await client.GetAsync("https://api.example.com/users");
        var content = await response.Content.ReadAsStringAsync();
        Console.WriteLine(content);
    }
}
```

Agora, veja um exemplo de como usar o HttpClientFactory para configurar e criar instâncias de HttpClient:

```csharp
using System.Net.Http;

class Program
{
    static async Task Main(string[] args)
    {
        var builder = new HostBuilder()
            .ConfigureServices((hostContext, services) =>
            {
                services.AddHttpClient("example", c =>
                {
                    c.BaseAddress = new Uri("https://api.example.com/");
                    c.DefaultRequestHeaders.Add("Accept", "application/json");
                });
            })
            .Build();

        var httpClientFactory = builder.Services.GetService<IHttpClientFactory>();
        var httpClient = httpClientFactory.CreateClient("example");

        var response = await httpClient.GetAsync("users");
        var content = await response.Content.ReadAsStringAsync();
        Console.WriteLine(content);
    }
}
```

----
<a href="https://github.com/stackforgecode/sf-csharp-responde/blob/main/README.md" style="position: sticky;">Voltar</a>

Neste exemplo, estamos usando o método `AddHttpClient` para configurar uma instância de HttpClient chamada "example". A configuração inclui a definição do endereço base da API e o header "Accept". Em seguida, usamos o método `CreateClient` do IHttpClientFactory para criar uma instância de HttpClient com base na configuração "example".
