# Injeção de Dependência 

Injeção de Dependência (ou Dependency Injection, em inglês) é um padrão de projeto de software que visa reduzir o acoplamento entre as classes de um sistema, tornando-o mais modular e flexível. Em essência, ele consiste em passar as dependências de uma classe para outra, em vez de criá-las dentro da própria classe.

A ideia por trás da Injeção de Dependência é que as classes devem ser responsáveis apenas por sua própria lógica, e não por criar ou gerenciar suas dependências. Isso facilita a manutenção e a evolução do código, já que cada classe pode ser alterada ou substituída sem afetar as outras classes.

Em C#, a Injeção de Dependência é implementada usando contêineres de IoC (Inversion of Control), como o Unity, Autofac ou o nativo do .NET Core. Esses contêineres são responsáveis por gerenciar as dependências do sistema e injetá-las automaticamente nas classes que precisam delas.

Existem três tipos de Injeção de Dependência em C#:

1. Injeção de Dependência por Construtor: as dependências são passadas como parâmetros para o construtor da classe. Por exemplo:

```
public class MinhaClasse {
    private readonly IService _service;

    public MinhaClasse(IService service) {
        _service = service;
    }

    // ...
}
```

2. Injeção de Dependência por Propriedade: as dependências são definidas como propriedades da classe e injetadas por meio do contêiner de IoC. Por exemplo:

```
public class MinhaClasse {
    public IService Service { get; set; }

    // ...
}
```

3. Injeção de Dependência por Método: as dependências são passadas por meio de métodos específicos da classe. Por exemplo:

```
public class MinhaClasse {
    public void SetService(IService service) {
        // ...
    }

    // ...
}
```

Independentemente do tipo de Injeção de Dependência utilizado, é importante lembrar que o objetivo é tornar o código mais modular e flexível, permitindo que as classes sejam modificadas ou substituídas facilmente. Para isso, é importante definir as dependências de forma clara e usar contêineres de IoC confiáveis e bem configurados.

----

## Exemplo do Mundo Real

A Injeção de Dependência é como um grupo de humoristas como os 4Amigos. Cada membro do grupo representa uma classe do sistema, e eles trabalham juntos para criar um espetáculo de sucesso. Mas para que o espetáculo seja bom, eles precisam se conhecer bem e confiar uns nos outros. Cada um tem sua própria personalidade e seu próprio estilo de humor, mas eles precisam trabalhar em conjunto para que o show seja um sucesso.

Assim como os membros dos 4Amigos, as classes de um sistema também têm suas próprias responsabilidades e características. Algumas classes podem ser mais complexas ou ter mais dependências do que outras, assim como alguns integrantes do grupo podem ter mais piadas ou mais habilidades em palco do que outros.

A Injeção de Dependência permite que as classes trabalhem juntas de forma mais harmoniosa, assim como os membros dos 4Amigos. Ao invés de cada classe ter que se preocupar com suas próprias dependências e configurações, elas podem simplesmente receber as dependências de outras classes por meio do contêiner de IoC. Isso permite que as classes se concentrem em suas próprias responsabilidades, e torna o sistema mais fácil de manter e evoluir.

Além disso, a Injeção de Dependência também permite que as classes sejam facilmente substituídas ou modificadas, assim como os membros dos 4Amigos podem ser substituídos ou o estilo de humor do grupo pode ser modificado. Isso torna o sistema mais flexível e adaptável às mudanças.

Em resumo, assim como os membros dos 4Amigos trabalham juntos para criar um espetáculo de sucesso, as classes de um sistema podem trabalhar juntas de forma mais harmoniosa e flexível com a Injeção de Dependência.





