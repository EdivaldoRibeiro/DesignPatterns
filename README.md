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
```
/** "Component" */
interface Graphic {

    //Printa o grafico.
    public void print();
}

/** "Composite" */
import java.util.List;
import java.util.ArrayList;
class CompositeGraphic implements Graphic {

    //Coleção de Graficos  filhos
    private List<Graphic> childGraphics = new ArrayList<Graphic>();

    //Printa o grafico
    public void print() {
        for (Graphic graphic : childGraphics) {
            graphic.print();
        }
    }

    //Adiciona o grafico  a composição.
    public void add(Graphic graphic) {
        childGraphics.add(graphic);
    }
    //Remove a forma geometrica da composição.
    public void remove(Graphic graphic) {
        childGraphics.remove(graphic);
    }
}

/** "Leaf" */
class Ellipse implements Graphic {

    //Printa o grafico.
    public void print() {
        System.out.println("Ellipse");
    }
}

/** Client */
public class Program {

    public static void main(String[] args) {
        //Inicializa quatro elipses
        Ellipse ellipse1 = new Ellipse();
        Ellipse ellipse2 = new Ellipse();
        Ellipse ellipse3 = new Ellipse();
        Ellipse ellipse4 = new Ellipse();

        //Inicializa tres componentes do grafico.
        CompositeGraphic graphic = new CompositeGraphic();
        CompositeGraphic graphic1 = new CompositeGraphic();
        CompositeGraphic graphic2 = new CompositeGraphic();

        //Faz o grafico
        graphic1.add(ellipse1);
        graphic1.add(ellipse2);
        graphic1.add(ellipse3);

        graphic2.add(ellipse4);

        graphic.add(graphic1);
        graphic.add(graphic2);
       // Printa quatro vezes a String Ellipse ( Ele printa o grafico completo).
        graphic.print();
    }
}
```
> Decorator

- Adiciona responsabilidades a um objeto dinamicamente. Decoradores provêem uma alternativa flexível à herança para estender funcionalidade.
```
public interface Arma{

  public void montar();

}

public class ArmaBase implements Arma{

  @Override
  public void montar(){
    System.out.println("Essa é uma arma base");
  }

}

public class ArmaDecorator implements Arma{

  public Arma arma;

  public ArmaDecorator(Arma arma){
    this.arma = arma;
  }

  @Override
  public void montar(){
    this.arma.montar();
  }

}

public class Mira extends ArmaDecorator{

  public Mira(Arma arma){
    super(arma);
  }

  @Override
  public void montar(){
    super.montar();
    System.out.println("Adicionando mira a arma");
  }

}

public class Silenciador extends ArmaDecorator{

  public Silenciador(Arma arma){
    super(arma);
  }

  @Override
  public void montar(){
    super.montar();
    System.out.println("Adicionando silenciador a arma");
  }

}

/* Monta uma arma com mira e silenciador */
Arma armaCompleta = new Silenciador( new Mira( new ArmaBase() ) );
armaCompleta->montar();

/* Monta uma arma sem acessórios */
Arma armaB = new ArmaBase();
armaB->montar();

/* Monta uma arma com silenciador */
Arma armaComSilenciador = new Silenciador( armaB );
armaComSilenciador->montar();

/* Monta uma arma com mira */
Arma armaComMira = new Mira( armaB );
armaComMira->montar();
```
> Facade

- Provê uma interface unificada para um conjunto de interfaces num subsistema. O padrão Façade define uma interface de mais alto nível, deixando o subsistema mais fácil de usar.
```
/* Complex parts */

class CPU {
    public void freeze() { ... }
    public void jump(long position) { ... }
    public void execute() { ... }
}

class HardDrive {
    public byte[] read(long lba, int size) { ... }
}

class Memory {
    public void load(long position, byte[] data) { ... }
}

/* Facade */

class ComputerFacade {
    private CPU processor;
    private Memory ram;
    private HardDrive hd;

    public ComputerFacade() {
        this.processor = new CPU();
        this.ram = new Memory();
        this.hd = new HardDrive();
    }

    public void start() {
        processor.freeze();
        ram.load(BOOT_ADDRESS, hd.read(BOOT_SECTOR, SECTOR_SIZE));
        processor.jump(BOOT_ADDRESS);
        processor.execute();
    }
}

/* Client */

class You {
    public static void main(String[] args) {
        ComputerFacade computer = new ComputerFacade();
        computer.start();
    }
}
```
> Flyweight

- Usa o compartilhamento para dar suporte eficiente ao uso de um grande número de objetos de granularidade pequena.
```
import java.util.HashMap;
import java.util.Map;

interface BMWCarCustomisation {
	// customize Tire size
	int getTireSize();
	String getLaserSignature();
	// a lot of customisation attributes can be in there for a BMW car
	void printCustomisations();
}

interface BMWCar {
	double calculatePrice(BMWCarCustomisation custom);
	void printFullCharacteristics(BMWCarCustomisation custom);
}

interface BMWCarFactory {
	BMWCar createCar();
}

interface BMWCarFlyWeightFactory {
	enum Model {Serie1, Serie2, Serie3};
	BMWCar getBMWModel(Model m);
}

class BMWSerie1 implements BMWCar {
	private final static double BASE_PRICE = 25000;

	@Override
	public double calculatePrice(BMWCarCustomisation custom) {
		return BASE_PRICE + getSpecificSerie1PriceBasedOnCustom(custom) + getExportationTaxe(custom);
	}

	@Override
	public void printFullCharacteristics(BMWCarCustomisation custom) {
		// print all BMW 1 Series specific characteristics
		// (codes in there)
		custom.printCustomisations(); // print details based on these customisations
	}

	private double getSpecificSerie1PriceBasedOnCustom(BMWCarCustomisation custom) {
		// (e.g., calculation based on custom specific to Series 1)
		double sum = 0;
		if (custom.getTireSize() == 19) {
			sum += 1200;
		} else {
			sum += 2100;
		}
		return sum;
	}

	private double getExportationTaxe(BMWCarCustomisation custom) {
		// (calculation based on custom exportation taxes only for this model)
		double sum = 0;
		if (!custom.getLaserSignature().isEmpty()) {
			sum += 987;
		}
		return sum;
	}
}

class BMWSerie2 implements BMWCar {
	private final static double BASE_PRICE = 28000;

	@Override
	public double calculatePrice(BMWCarCustomisation custom) {
		return BASE_PRICE + getSpecificSerie2PriceBasedOnCustom(custom);
	}

	@Override
	public void printFullCharacteristics(BMWCarCustomisation custom) {
		// print all BMW 2 Series specific characteristics
		// (codes in there)
		custom.printCustomisations(); // print details based on these customisations
	}

	private double getSpecificSerie2PriceBasedOnCustom(BMWCarCustomisation custom) {
		// (e.g., calculation based on custom specific to Series 2)
		double sum = 0;
		if (custom.getTireSize() == 19) {
			sum += 2000;
		} else {
			sum += 3000;
		}
		if (!custom.getLaserSignature().isEmpty()) {
			if (custom.getLaserSignature().length() > 10) {
				sum += 1200;
			} else {
				sum += 400;
			}
		}
		return sum;
	}
}

class BMWSerie2Factory implements BMWCarFactory {
	@Override
	public BMWCar createCar() {
		return new BMWSerie2();
	}
}

class BMWSerie1Factory implements BMWCarFactory {
	@Override
	public BMWCar createCar() {
		return new BMWSerie1();
	}
}

class BMWSerieFlyWeightFactory implements BMWCarFlyWeightFactory {
	private Map<Model, BMWCar> cache = new HashMap<>();

	public synchronized BMWCar getBMWModel(Model m) {
		if (!cache.containsKey(m)) {
			BMWCarFactory concreteFactory;
			switch (m) {
			case Serie2:
				concreteFactory = new BMWSerie2Factory();
				break;
			case Serie3:
				concreteFactory = new BMWSerie3Factory();
				break;
			/*
			 * Just code to have a hint !
			 */
			default:
				concreteFactory = new BMWSerie1Factory();
				break;
			}
			cache.put(m, concreteFactory.createCar());
		}
		return cache.get(m);
	}
}

class BMWSerieCarCustomisation implements BMWCarCustomisation {

	private int tireSize;
	private String laserSignature;

	public BMWSerieCarCustomisation(int tireSize, String laserSignature) {
		this.tireSize = tireSize;
		this.laserSignature = laserSignature;
	}

	public int getTireSize() {
		return tireSize;
	}

	public String getLaserSignature() {
		return laserSignature;
	}

	@Override
	public void printCustomisations() {
		System.out.println("Tire Size:" + getTireSize());
		System.out.println("LaserSignature:" + getLaserSignature());
		System.out.println("LaserSignature Size:" + getLaserSignature().length());
	}
}

public class MainTest {

	public static void main(String[] args) {
		BMWCarFlyWeightFactory factory = new BMWSerieFlyWeightFactory();
		BMWCar serie1Car = factory.getBMWModel(BMWCarFlyWeightFactory.Model.Serie1);
		BMWCar serie1Car2 = factory.getBMWModel(BMWCarFlyWeightFactory.Model.Serie1);
		System.out.println("check for Object for Serie1:" + (serie1Car == serie1Car2));
		BMWCar serie2Car = factory.getBMWModel(BMWCarFlyWeightFactory.Model.Serie2);
		BMWCar serie2Car2 = factory.getBMWModel(BMWCarFlyWeightFactory.Model.Serie2);
		System.out.println("check for Object for Serie2:" + (serie2Car == serie2Car2));
		BMWCarCustomisation custom1 = new BMWSerieCarCustomisation(19, "Oh yeah");
		BMWCarCustomisation custom2 = new BMWSerieCarCustomisation(21, "For bob");
		BMWCarCustomisation custom3 = new BMWSerieCarCustomisation(26, "give it a ride !!");
		// BMW 1 Series
		System.out.println("BMW Serie1 + Custom1 Price:\nFull Price:" + serie1Car.calculatePrice(custom1));
		serie1Car.printFullCharacteristics(custom1);
		System.out.println("BMW Serie1 + Custom2 Price:\nFull Price:" + serie1Car.calculatePrice(custom2));
		serie1Car.printFullCharacteristics(custom2);
		System.out.println("BMW Serie1 + Custom3 Price:\nFull Price:" + serie1Car.calculatePrice(custom3));
		serie1Car.printFullCharacteristics(custom3);
		/// It's the samed BMW 1 Series Flyweight instance; the variant part is provided
		/// by the operation and customs
		// BMW 2 Series
		System.out.println("BMW Serie2 + Custom1 Price:\nFull Price:" + serie2Car.calculatePrice(custom1));
		serie2Car.printFullCharacteristics(custom1);
		System.out.println("BMW Serie2 + Custom2 Price:\nFull Price:" + serie2Car.calculatePrice(custom2));
		serie2Car.printFullCharacteristics(custom2);
		System.out.println("BMW Serie2 + Custom3 Price:\nFull Price:" + serie2Car.calculatePrice(custom3));
		serie2Car.printFullCharacteristics(custom3);
		/// It's the samed BMW 2 Series Flyweight instance; the variant part is provided
		/// by the operation and customs
	}
}
```
> Proxy

- Provê um objeto procurador ou placeholder para um outro objeto para controlar o acesso a ele.
```
interface Image {
    public void displayImage();
}

// On System A
class RealImage implements Image {

    private String filename = null;
    /**
     * Constructor
     * @param filename
     */
    public RealImage(final String filename) {
        this.filename = filename;
        loadImageFromDisk();
    }

    /**
     * Loads the image from the disk
     */
    private void loadImageFromDisk() {
        System.out.println("Loading   " + filename);
    }

    /**
     * Displays the image
     */
    public void displayImage() {
        System.out.println("Displaying " + filename);
    }

}

// On System B
class ProxyImage implements Image {

    private RealImage image = null;
    private String filename = null;
    /**
     * Constructor
     * @param filename
     */
    public ProxyImage(final String filename) {
        this.filename = filename;
    }

    /**
     * Displays the image
     */
    public void displayImage() {
        if (image == null) {
           image = new RealImage(filename);
        }
        image.displayImage();
    }

}

class ProxyExample {

   /**
    * Test method
    */
   public static void main(final String[] arguments) {
        final Image image1 = new ProxyImage("HiRes_10MB_Photo1");
        final Image image2 = new ProxyImage("HiRes_10MB_Photo2");

        image1.displayImage(); // loading necessary
        image1.displayImage(); // loading unnecessary
        image2.displayImage(); // loading necessary
        image2.displayImage(); // loading unnecessary
        image1.displayImage(); // loading unnecessary
    }
}
```
### Padrões Comportamentais:

> Chain of Responsibility

- Evita acoplar o enviador de um pedido ao receptor dando oportunidade a vários objetos para tratarem do pedido. Os objetos receptores são encadeados e o pedido é passado na cadeia até que um objeto o trate.
```
abstract class PurchasePower {
    protected static final double BASE = 500;
    protected PurchasePower successor;

    abstract protected double getAllowable();
    abstract protected String getRole();

    public void setSuccessor(PurchasePower successor) {
        this.successor = successor;
    }

    public void processRequest(PurchaseRequest request) {
        if (request.getAmount() < this.getAllowable()) {
            System.out.println(this.getRole() + " will approve $" + request.getAmount());
        } else if (successor != null) {
            successor.processRequest(request);
        }
    }
}

class ManagerPPower extends PurchasePower {
    
    protected double getAllowable() {
        return BASE * 10;
    }

    protected String getRole() {
        return "Manager";
    }
}

class DirectorPPower extends PurchasePower {
    
    protected double getAllowable() {
        return BASE * 20;
    }

    protected String getRole() {
        return "Director";
    }
}

class VicePresidentPPower extends PurchasePower {
    
    protected double getAllowable() {
        return BASE * 40;
    }

    protected String getRole() {
        return "Vice President";
    }
}

class PresidentPPower extends PurchasePower {

    protected double getAllowable() {
        return BASE * 60;
    }

    protected String getRole() {
        return "President";
    }
}

class PurchaseRequest {

    private double amount;
    private String purpose;

    public PurchaseRequest(double amount, String purpose) {
        this.amount = amount;
        this.purpose = purpose;
    }

    public double getAmount() {
        return this.amount;
    }

    public void setAmount(double amount)  {
        this.amount = amount;
    }

    public String getPurpose() {
        return this.purpose;
    }
    public void setPurpose(String purpose) {
        this.purpose = purpose;
    }
}

class CheckAuthority {

    public static void main(String[] args) {
        ManagerPPower manager = new ManagerPPower();
        DirectorPPower director = new DirectorPPower();
        VicePresidentPPower vp = new VicePresidentPPower();
        PresidentPPower president = new PresidentPPower();
        manager.setSuccessor(director);
        director.setSuccessor(vp);
        vp.setSuccessor(president);

        // Press Ctrl+C to end.
        try {
            while (true) {
                System.out.println("Enter the amount to check who should approve your expenditure.");
                System.out.print(">");
                double d = Double.parseDouble(new BufferedReader(new InputStreamReader(System.in)).readLine());
                manager.processRequest(new PurchaseRequest(d, "General"));
            }
        }
        catch (Exception exc) {
            System.exit(1);
        }
    }
}
```
> Command

- Encapsula um pedido em um objeto, permitindo assim parametrizar clientes com pedidos diferentes, enfileirar pedidos, fazer log de pedidos, e dar suporte a operações de undo.
```
import java.util.List;
import java.util.ArrayList;

/** The Command interface */
public interface Command {
   void execute();
}

/** The Invoker class */
public class Switch {
   private List<Command> history = new ArrayList<Command>();

   public void storeAndExecute(final Command cmd) {
      this.history.add(cmd); // optional
      cmd.execute();
   }
}

/** The Receiver class */
public class Light {

   public void turnOn() {
      System.out.println("The light is on");
   }

   public void turnOff() {
      System.out.println("The light is off");
   }
}

/** The Command for turning on the light - ConcreteCommand #1 */
public class FlipUpCommand implements Command {
   private Light theLight;

   public FlipUpCommand(final Light light) {
      this.theLight = light;
   }

   @Override    // Command
   public void execute() {
      theLight.turnOn();
   }
}

/** The Command for turning off the light - ConcreteCommand #2 */
public class FlipDownCommand implements Command {
   private Light theLight;

   public FlipDownCommand(final Light light) {
      this.theLight = light;
   }

   @Override    // Command
   public void execute() {
      theLight.turnOff();
   }
}

/* The test class or client */
public class PressSwitch {
   public static void main(final String[] arguments){
      // Check number of arguments
      if (arguments.length != 1) {
         System.err.println("Argument \"ON\" or \"OFF\" is required!");
         System.exit(-1);
      }

      final Light lamp = new Light();
	  
      final Command switchUp = new FlipUpCommand(lamp);
      final Command switchDown = new FlipDownCommand(lamp);

      final Switch mySwitch = new Switch();

      switch(arguments[0]) {
         case "ON":
            mySwitch.storeAndExecute(switchUp);
            break;
         case "OFF":
            mySwitch.storeAndExecute(switchDown);
            break;
         default:
            System.err.println("Argument \"ON\" or \"OFF\" is required.");
            System.exit(-1);
      }
   }
}
```
> Interpreter

- Dada uma linguagem, define uma representação de sua gramática e um interpretador que usa a representação da gramática para interpretar sentenças da linguagem.
```
import java.util.Map;

interface Expression {
    public int interpret(final Map<String, Expression> variables);
}

class Number implements Expression {
    private int number;
    public Number(final int number)       { this.number = number; }
    public int interpret(final Map<String, Expression> variables)  { return number; }
}

class Plus implements Expression {
    Expression leftOperand;
    Expression rightOperand;
    public Plus(final Expression left, final Expression right) {
        leftOperand = left;
        rightOperand = right;
    }
		
    public int interpret(final Map<String, Expression> variables) {
        return leftOperand.interpret(variables) + rightOperand.interpret(variables);
    }
}

class Minus implements Expression {
    Expression leftOperand;
    Expression rightOperand;
    public Minus(final Expression left, final Expression right) {
        leftOperand = left;
        rightOperand = right;
    }
		
    public int interpret(final Map<String, Expression> variables) {
        return leftOperand.interpret(variables) - rightOperand.interpret(variables);
    }
}

class Variable implements Expression {
    private String name;
    public Variable(final String name)       { this.name = name; }
    public int interpret(final Map<String, Expression> variables) {
        if (null == variables.get(name)) return 0; // Either return new Number(0).
        return variables.get(name).interpret(variables);
    }
}

import java.util.Map;
import java.util.Stack;

class Evaluator implements Expression {
    private Expression syntaxTree;

    public Evaluator(final String expression) {
        final Stack<Expression> expressionStack = new Stack<Expression>();
        for (final String token : expression.split(" ")) {
            if (token.equals("+")) {
                final Expression subExpression = new Plus(expressionStack.pop(), expressionStack.pop());
                expressionStack.push(subExpression);
            } else if (token.equals("-")) {
                // it's necessary to remove first the right operand from the stack
                final Expression right = expressionStack.pop();
                // ..and then the left one
                final Expression left = expressionStack.pop();
                final Expression subExpression = new Minus(left, right);
                expressionStack.push(subExpression);
            } else
                expressionStack.push(new Variable(token));
        }
        syntaxTree = expressionStack.pop();
    }

    public int interpret(final Map<String, Expression> context) {
        return syntaxTree.interpret(context);
    }
}

import java.util.Map;
import java.util.HashMap;

public class InterpreterExample {
    public static void main(final String[] args) {
        final String expression = "w x z - +";
        final Evaluator sentence = new Evaluator(expression);
        final Map<String, Expression> variables = new HashMap<String, Expression>();
        variables.put("w", new Number(5));
        variables.put("x", new Number(10));
        variables.put("z", new Number(42));
        final int result = sentence.interpret(variables);
        System.out.println(result);
    }
}
```
> Iterator

- Provê uma forma de acessar os elementos de uma coleção de objetos seqüencialmente sem expor sua representação subjacente.
```
import java.util.Iterator;
import java.util.HashSet;
import java.util.Set;

class RedHead implements Iterable<RedHead> {
    private Set<RedHead> redHeads = new HashSet<RedHead>();
    
    public void add(final RedHead redHead) {
        redHeads.add(redHead);
    }
    @Override
    public Iterator<RedHead> iterator() {
        return redHeads.iterator();
    }
}

class Weasley extends RedHead {
    private String name;
    
    public Weasley(final String name) {
        this.name = name;
    }
    public String toString() {
        return this.name + " Weasley";
    }
}

public static IteratorExample {
    public static void main(String[] args) {
        RedHead redHead = new RedHead();
        
        redHead.add(new Weasley("Arthur"));
        redHead.add(new Weasley("Molly"));
        redHead.add(new Weasley("Bill"));
        redHead.add(new Weasley("Charlie"));
        redHead.add(new Weasley("Percy"));
        redHead.add(new Weasley("Fred"));
        redHead.add(new Weasley("George"));
        redHead.add(new Weasley("Ron"));
        redHead.add(new Weasley("Ginny"));
        
        for (ReadHead rh : redHead) {
            System.out.println(rh);
        }
    }
}
```
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
