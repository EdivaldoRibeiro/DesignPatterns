# DesignPatterns
Meu aprendizado no uso de `Design Patterns`.

### Padrões de Criação:

> Abstract Factory
   
- Provê uma interface para criar famílias de objetos relacionados ou inter-dependentes sem especificar suas classes concretas.
```
public interface IButton {
	void paint();
}

public interface IGUIFactory {
	public IButton createButton();
}

public class WinFactory implements IGUIFactory {
	@Override
	public IButton createButton() {
		return new WinButton();
	}
}

public class OSXFactory implements IGUIFactory {
	@Override
	public IButton createButton() {
		return new OSXButton();
	}
}

public class WinButton implements IButton {
	@Override
	public void paint() {
		System.out.println("WinButton");
	}
}

public class OSXButton implements IButton {
	@Override
	public void paint() {
		System.out.println("OSXButton");
	}
}
```
> Builder

- Separa a construção de um objeto complexo da sua representação de forma que o mesmo processo de construção possa criar representações diferentes.
```
abstract class ConversorTexto {
 	public void converterCaractere(char c) {
 		// vazio
 	}

 	public void converterParagrafo() {
 		// vazio
 	}

 	public void converterFonte(Fonte f) {
 		// vazio
 	}
 }

 class ConversorPDF extends ConversorTexto {
 	public void converterCaractere(char c) {
 		System.out.print("Caractere PDF");
 	}

 	public void converterParagrafo() {
 		System.out.print("Parágrafo PDF");
 	}

 	public void converterFonte(Fonte f) {
 		System.out.print("Fonte PDF");
 	}
 }

 class ConversorTeX extends ConversorTexto {
 	public void converterCaractere(char c) {
 		System.out.print("Caractere Tex");
 	}

 	public void converterParagrafo() {
 		System.out.print("Paragrafo Tex");
 	}

 	public void converterFonte(Fonte f) {
 		System.out.print("Fonte Tex");
 	}
 }

 class ConversorASCII extends ConversorTexto {
 	public void converterCaractere(char c) {
 		System.out.print("Caractere ASCII");
 	}
 }

 class LeitorRTF {

 	private ConversorTexto conversor;

 	LeitorRTF(ConversorTexto c) {
 		this.conversor = c;
 	}

 	public void lerRTF() {

 		List<Token> tokens = obterTokensDoTexto();

 		for (Token t : tokens) {
 			if (t.getTipo() == Token.Tipo.CARACTERE) {
 				conversor.converterCaractere(t.getCaractere());
 			}
 			if (t.getTipo() == Token.Tipo.PARAGRAFO) {
 				conversor.converterParagrafo();
 			}
 			if (t.getTipo() == Token.Tipo.FONTE) {
 				conversor.converterFonte(t.getFonte());
 			}
 		}
 	}
 }
```
> Factory Method
    
- Define uma interface para criar um objeto, mas deixa as subclasses decidirem qual classe instanciar. O padrão Factory Method deixa uma classe repassar a responsabilidade de instanciação para subclasses.

```
public abstract class Room {
   abstract void connect(Room room);
}

public class MagicRoom extends Room {
   public void connect(Room room) {}
}

public class OrdinaryRoom extends Room {
   public void connect(Room room) {}
}

public abstract class MazeGame {
    private final List<Room> rooms = new ArrayList<>();

    public MazeGame() {
        Room room1 = makeRoom();
        Room room2 = makeRoom();
        room1.connect(room2);
        rooms.add(room1);
        rooms.add(room2);
    }

    abstract protected Room makeRoom();
}

public class MagicMazeGame extends MazeGame {
    @Override
    protected Room makeRoom() {
        return new MagicRoom(); 
    }
}

public class OrdinaryMazeGame extends MazeGame {
    @Override
    protected Room makeRoom() {
        return new OrdinaryRoom(); 
    }
}

MazeGame ordinaryGame = new OrdinaryMazeGame();
MazeGame magicGame = new MagicMazeGame();
```
> Prototype
    
- Especifica os tipos de objetos a criar usando uma instância-protótipo e cria novos objetos copiando este protótipo.
```
// Prototype pattern
public abstract class Prototype implements Cloneable {
    public Prototype clone() throws CloneNotSupportedException{
        return (Prototype) super.clone();
    }
}
	
public class ConcretePrototype1 extends Prototype {
    @Override
    public Prototype clone() throws CloneNotSupportedException {
        return (ConcretePrototype1)super.clone();
    }
}

public class ConcretePrototype2 extends Prototype {
    @Override
    public Prototype clone() throws CloneNotSupportedException {
        return (ConcretePrototype2)super.clone();
    }
}
```
> Singleton

- Garante que uma classe tenha uma única instância e provê um ponto global de acesso à instância.
```
public final class Singleton {

    private static final Singleton INSTANCE = new Singleton();

    private Singleton() {}

    public static Singleton getInstance() {
        return INSTANCE;
    }
}
```
### Padrões Estruturais:

> Adapter

- Converte a interface de uma classe em outra interface com a qual os clientes estão prontos para lidar. O padrão Adapter permite que classes trabalhem conjuntamente apesar de interfaces incompatíveis.
```
//Classe adaptada(Adaptee)
class EntradaPS2 {

    //Solicitação Especifica
    public void conectarEntradaPS2() {
        System.out.println("Conectado na entrada PS2");
    }
}

//Classe alvo(Target)
class EntradaUSB {

    //Solicitação
    public void conectarEntradaUSB() {
        System.out.println("Conectado na entrada USB");
    }
}

//Classe adaptador(Adapter)
class AdapterEntrada extends EntradaUSB {

    private EntradaPS2 entradaPS2;

    public AdapterEntrada(EntradaPS2 entradaPs2) {
        this.entradaPS2 = entradaPs2;
    }

    //Solicitação
    public void conectarEntradaUSB() {
        entradaPS2.conectarEntradaPS2();
    }
}

//Classe Cliente(Client)
public class Teclado {

    public static void main(String[] args) {
        EntradaPS2 ps2 = new EntradaPS2();
        AdapterEntrada adaptador = new AdapterEntrada(ps2);
        adaptador.conectarEntradaUSB();
    }
}
```
> Bridge

- Desacopla uma abstração de sua implementação de forma que as duas possam mudar independentemente uma da outra.
```
/** "Implementor" */
interface DrawingAPI {
    public void drawCircle(final double x, final double y, final double radius);
}

/** "ConcreteImplementor"  1/2 */
class DrawingAPI1 implements DrawingAPI {
    public void drawCircle(final double x, final double y, final double radius) {
        System.out.printf("API1.circle at %f:%f radius %f%n", x, y, radius);
    }
}

/** "ConcreteImplementor" 2/2 */
class DrawingAPI2 implements DrawingAPI {
    public void drawCircle(final double x, final double y, final double radius) {
        System.out.printf("API2.circle at %f:%f radius %f%n", x, y, radius);
    }
}

/** "Abstraction" */
abstract class Shape {
    protected DrawingAPI drawingAPI;

    protected Shape(final DrawingAPI drawingAPI){
        this.drawingAPI = drawingAPI;
    }

    public abstract void draw();                                 // low-level
    public abstract void resizeByPercentage(final double pct);   // high-level
}

/** "Refined Abstraction" */
class CircleShape extends Shape {
    private double x, y, radius;
    public CircleShape(final double x, final double y, final double radius, final DrawingAPI drawingAPI) {
        super(drawingAPI);
        this.x = x;  this.y = y;  this.radius = radius;
    }

    // low-level i.e. Implementation specific
    public void draw() {
        drawingAPI.drawCircle(x, y, radius);
    }
    // high-level i.e. Abstraction specific
    public void resizeByPercentage(final double pct) {
        radius *= (1.0 + pct/100.0);
    }
}

/** "Client" */
class BridgePattern {
    public static void main(final String[] args) {
        Shape[] shapes = new Shape[] {
            new CircleShape(1, 2, 3, new DrawingAPI1()),
            new CircleShape(5, 7, 11, new DrawingAPI2())
        };

        for (Shape shape : shapes) {
            shape.resizeByPercentage(2.5);
            shape.draw();
        }
    }
}
```
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
