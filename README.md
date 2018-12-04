# DesignPatterns
Meu aprendizado no uso de "Design Patterns".

Padrões de Criação:
=

<em><b>Abstract Factory</b></em>
   
Provê uma interface para criar famílias de objetos relacionados ou inter-dependentes sem especificar suas classes concretas.

<em><b>Builder</b></em>

Separa a construção de um objeto complexo da sua representação de forma que o mesmo processo de construção possa criar representações diferentes.

<em><b>Factory Method</b></em>
    
Define uma interface para criar um objeto, mas deixa as subclasses decidirem qual classe instanciar. O padrão Factory Method deixa uma classe repassar a responsabilidade de instanciação para subclasses.

<em><b>Prototype</b></em>
    
Especifica os tipos de objetos a criar usando uma instância-protótipo e cria novos objetos copiando este protótipo.

<em><b>Singleton</b></em>

Garante que uma classe tenha uma única instância e provê um ponto global de acesso à instância.

Padrões Estruturais:
=

<em><b>Adapter</b></em>

Converte a interface de uma classe em outra interface com a qual os clientes estão prontos para lidar. O padrão Adapter permite que classes trabalhem conjuntamente apesar de interfaces incompatíveis.

<em><b>Bridge</b></em>

Desacopla uma abstração de sua implementação de forma que as duas possam mudar independentemente uma da outra.

<em><b>Composite</b></em>

Compõe objetos em estruturas de árvore para representar hierarquias Parte-Todo. O padrão Composite permite que clientes tratem objetos individuais e composições de objetos de uniformemente.

<em><b>Decorator</b></em>

Adiciona responsabilidades a um objeto dinamicamente. Decoradores provêem uma alternativa flexível à herança para estender funcionalidade.

<em><b>Facade</b></em>

Provê uma interface unificada para um conjunto de interfaces num subsistema. O padrão Façade define uma interface de mais alto nível, deixando o subsistema mais fácil de usar.

<em><b>Flyweight</b></em>

Usa o compartilhamento para dar suporte eficiente ao uso de um grande número de objetos de granularidade pequena.

<em><b>Proxy</b></em>

Provê um objeto procurador ou placeholder para um outro objeto para controlar o acesso a ele.

Padrões Comportamentais:
=

<em><b>Chain of Responsibility</b></em>

Evita acoplar o enviador de um pedido ao receptor dando oportunidade a vários objetos para tratarem do pedido. Os objetos receptores são encadeados e o pedido é passado na cadeia até que um objeto o trate.

<em><b>Command</b></em>

Encapsula um pedido em um objeto, permitindo assim parametrizar clientes com pedidos diferentes, enfileirar pedidos, fazer log de pedidos, e dar suporte a operações de undo.

<em><b>Interpreter</b></em>

Dada uma linguagem, define uma representação de sua gramática e um interpretador que usa a representação da gramática para interpretar sentenças da linguagem.

<em><b>Iterator</b></em>

Provê uma forma de acessar os elementos de uma coleção de objetos seqüencialmente sem expor sua representação subjacente.

<em><b>Mediator</b></em>

Define um objeto que encapsule a forma com a qual um conjunto de objetos interagem. O padrão Mediator promove o acoplamento fraco evitando que objetos referenciem uns aos outros explicitamente e permite que suas interações variem independentemente.

<em><b>Memento</b></em>

Sem violar o princípio de encapsulamento, captura e externaliza o estado interno de um objeto de forma a poder restaurar o objeto a este estado mais tarde.

<em><b>Observer</b></em>

Define uma dependência um-para-muitos entre objetos de forma a avisar e atualizar vários objetos quando o estado de um objeto muda.

<em><b>State</b></em>

Permite que um objeto altere seu comportamento quando seu estado interno muda. O objeto estará aparentemente mudando de classe com a mudança de estado.

<em><b>Strategy</b></em>

Define uma família de algoritmos, encapsula cada um, e deixe-os intercambiáveis. O padrão Strategy permite que o algoritmo varie independentemente dos clientes que o usam.

<em><b>Template Method</b></em>

Define o esqueleto de um algoritmo numa operação, deixando que subclasses completem algumas das etapas. O padrão Template Method permite que subclasses redefinem determinadas etapas de um algoritmo sem alterar a estrutura do algoritmo.

<em><b>Visitor</b></em>

Represente uma operação a ser realizada nos elementos de uma estrutura de objetos. O padrão Visitor permite que se defina uma nova operação sem alterar as classes dos elementos nos quais a operação age.
