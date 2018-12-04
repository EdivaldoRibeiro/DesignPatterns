# DesignPatterns
Meu aprendizado no uso de `Design Patterns`.

### Padrões de Criação:

> Abstract Factory
   
- Provê uma interface para criar famílias de objetos relacionados ou inter-dependentes sem especificar suas classes concretas.

> Builder

- Separa a construção de um objeto complexo da sua representação de forma que o mesmo processo de construção possa criar representações diferentes.

> Factory Method
    
- Define uma interface para criar um objeto, mas deixa as subclasses decidirem qual classe instanciar. O padrão Factory Method deixa uma classe repassar a responsabilidade de instanciação para subclasses.

> Prototype
    
- Especifica os tipos de objetos a criar usando uma instância-protótipo e cria novos objetos copiando este protótipo.

> Singleton

- Garante que uma classe tenha uma única instância e provê um ponto global de acesso à instância.

### Padrões Estruturais:

> Adapter

- Converte a interface de uma classe em outra interface com a qual os clientes estão prontos para lidar. O padrão Adapter permite que classes trabalhem conjuntamente apesar de interfaces incompatíveis.

> Bridge

- Desacopla uma abstração de sua implementação de forma que as duas possam mudar independentemente uma da outra.

> Composite

- Compõe objetos em estruturas de árvore para representar hierarquias Parte-Todo. O padrão Composite permite que clientes tratem objetos individuais e composições de objetos de uniformemente.

> Decorator

- Adiciona responsabilidades a um objeto dinamicamente. Decoradores provêem uma alternativa flexível à herança para estender funcionalidade.

> Facade

- Provê uma interface unificada para um conjunto de interfaces num subsistema. O padrão Façade define uma interface de mais alto nível, deixando o subsistema mais fácil de usar.

> Flyweight

- Usa o compartilhamento para dar suporte eficiente ao uso de um grande número de objetos de granularidade pequena.

> Proxy

- Provê um objeto procurador ou placeholder para um outro objeto para controlar o acesso a ele.

### Padrões Comportamentais:

> Chain of Responsibility

- Evita acoplar o enviador de um pedido ao receptor dando oportunidade a vários objetos para tratarem do pedido. Os objetos receptores são encadeados e o pedido é passado na cadeia até que um objeto o trate.

> Command

- Encapsula um pedido em um objeto, permitindo assim parametrizar clientes com pedidos diferentes, enfileirar pedidos, fazer log de pedidos, e dar suporte a operações de undo.

> Interpreter

- Dada uma linguagem, define uma representação de sua gramática e um interpretador que usa a representação da gramática para interpretar sentenças da linguagem.

> Iterator

- Provê uma forma de acessar os elementos de uma coleção de objetos seqüencialmente sem expor sua representação subjacente.

> Mediator

- Define um objeto que encapsule a forma com a qual um conjunto de objetos interagem. O padrão Mediator promove o acoplamento fraco evitando que objetos referenciem uns aos outros explicitamente e permite que suas interações variem independentemente.

> Memento

- Sem violar o princípio de encapsulamento, captura e externaliza o estado interno de um objeto de forma a poder restaurar o objeto a este estado mais tarde.

> Observer

- Define uma dependência um-para-muitos entre objetos de forma a avisar e atualizar vários objetos quando o estado de um objeto muda.

> State

- Permite que um objeto altere seu comportamento quando seu estado interno muda. O objeto estará aparentemente mudando de classe com a mudança de estado.

> Strategy

- Define uma família de algoritmos, encapsula cada um, e deixe-os intercambiáveis. O padrão Strategy permite que o algoritmo varie independentemente dos clientes que o usam.

> Template Method

- Define o esqueleto de um algoritmo numa operação, deixando que subclasses completem algumas das etapas. O padrão Template Method permite que subclasses redefinem determinadas etapas de um algoritmo sem alterar a estrutura do algoritmo.

> Visitor

- Represente uma operação a ser realizada nos elementos de uma estrutura de objetos. O padrão Visitor permite que se defina uma nova operação sem alterar as classes dos elementos nos quais a operação age.
