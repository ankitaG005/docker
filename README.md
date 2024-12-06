/Q1. You are given an AudioPlayer class that only plays MP3 files. Extend its functionality to support playing both MP4 and VLC files by using the Adapter Pattern./

package Audio.com;

interface MediaPlayer { void play(String audioType, String fileName); }

class AudioPlayer implements MediaPlayer {

@Override
public void play(String audioType, String fileName) {
    if (audioType.equalsIgnoreCase("mp3")) {
        // Play MP3 file
    } else {
        System.out.println("Unsupported audio type");
    }
}
}

class MP4Player implements MediaPlayer {

@Override
public void play(String audioType, String fileName) {
    if (audioType.equalsIgnoreCase("mp4")) {
        // Play MP4 file
    } else {
        System.out.println("Unsupported audio type");
    }
}
}

class VLCPlayer implements MediaPlayer {

@Override
public void play(String audioType, String fileName) {
    if (audioType.equalsIgnoreCase("vlc")) {
        // Play VLC file
    } else {
        System.out.println("Unsupported audio type");
    }
}
}

class MediaAdapter implements MediaPlayer {

private MediaPlayer mediaPlayer;

public MediaAdapter(String audioType) {
    if (audioType.equalsIgnoreCase("mp4")) {
        mediaPlayer = new MP4Player();
    } else if (audioType.equalsIgnoreCase("vlc")) {
        mediaPlayer = new VLCPlayer();
    }
}

@Override
public void play(String audioType, String fileName) {
    mediaPlayer.play(audioType, fileName);
}
}

public class AdapterPatternDemo {

public static void main(String[] args) {
    AudioPlayer audioPlayer = new AudioPlayer();

    // Play MP3 file
    audioPlayer.play("mp3", "beyond_the_horizon.mp3");

    // Play MP4 file using MediaAdapter
    audioPlayer.play("mp4", "memories.mp4");

    // Play VLC file using MediaAdapter
    audioPlayer.play("vlc", "nature.vlc");
}
}

/Q2. Implement a simple system where you have Employee objects. An employee can either be an individual worker or a manager who supervises a team of employees. Use the Composite Pattern to treat both individual employees and managers uniformly in terms of their reporting structure./

package Employee.com; import java.util.*;

interface Employee { void report(); }

class IndividualEmployee implements Employee { private String name;

public IndividualEmployee(String name) {
    this.name = name;
}

@Override
public void report() {
    System.out.println("Individual Employee: " + name);
}
}

class Manager implements Employee { private String name; private List employees;

public Manager(String name) {
    this.name = name;
    this.employees = new ArrayList<>();
}

public void addEmployee(Employee employee) {
    employees.add(employee);
}

public void removeEmployee(Employee employee) {
    employees.remove(employee);
}

@Override
public void report() {
    System.out.println("Manager: " + name);
    for (Employee employee : employees) {
        employee.report();
    }
}
}

public class CompositePatternDemo { public static void main(String[] args) { IndividualEmployee employee1 = new IndividualEmployee("John Doe"); IndividualEmployee employee2 = new IndividualEmployee("Jane Smith"); IndividualEmployee employee3 = new IndividualEmployee("Mike Johnson");

    Manager manager1 = new Manager("Alice Williams");
    manager1.addEmployee(employee1);
    manager1.addEmployee(employee2);

    Manager manager2 = new Manager("Bob Brown");
    manager2.addEmployee(employee3);

    manager1.addEmployee(manager2);

    // Report structure
    manager1.report();
}
}

/Q3. Develop a Java application where you have different types of shapes (e.g., Circle, Rectangle) and draw implementations (e.g., DrawingAPI1, DrawingAPI2). Use the Bridge pattern to separate shape logic from drawing logic./

package DrawingAPT.com;

interface Shape { void draw(); }

interface DrawingAPI { void drawCircle(int radius); void drawRectangle(int x, int y, int width, int height); }

class DrawingAPI1 implements DrawingAPI { @Override public void drawCircle(int radius) { System.out.println("Drawing API 1: Circle with radius " + radius); }

@Override
public void drawRectangle(int x, int y, int width, int height) {
    System.out.println("Drawing API 1: Rectangle at (" + x + ", " + y + ") with width " + width + " and height " + height);
}
}

class DrawingAPI2 implements DrawingAPI { @Override public void drawCircle(int radius) { System.out.println("Drawing API 2: Circle with radius " + radius); }

@Override
public void drawRectangle(int x, int y, int width, int height) {
    System.out.println("Drawing API 2: Rectangle at (" + x + ", " + y + ") with width " + width + " and height " + height);
}
}

class Circle implements Shape { private int radius; private DrawingAPI drawingAPI;

public Circle(int radius, DrawingAPI drawingAPI) {
    this.radius = radius;
    this.drawingAPI = drawingAPI;
}

@Override
public void draw() {
    drawingAPI.drawCircle(radius);
}
}

class Rectangle implements Shape { private int x, y, width, height; private DrawingAPI drawingAPI;

public Rectangle(int x, int y, int width, int height, DrawingAPI drawingAPI) {
    this.x = x;
    this.y = y;
    this.width = width;
    this.height = height;
    this.drawingAPI = drawingAPI;
}

@Override
public void draw() {
    drawingAPI.drawRectangle(x, y, width, height);
}
}

public class BridgePatternDemo { public static void main(String[] args) { DrawingAPI drawingAPI1 = new DrawingAPI1(); DrawingAPI drawingAPI2 = new DrawingAPI2();

    Shape circle1 = new Circle(5, drawingAPI1);
    Shape circle2 = new Circle(7, drawingAPI2);
    Shape rectangle1 = new Rectangle(10, 20, 50, 30, drawingAPI1);
    Shape rectangle2 = new Rectangle(30, 40, 70, 60, drawingAPI2);

    circle1.draw();
    circle2.draw();
    rectangle1.draw();
    rectangle2.draw();
}
}

/*Q4. Create a basic Pizza class in Java and then implement decorators to add different toppings (like cheese, olives, and mushrooms) to the pizza. Each topping should be an additional class that extends a base decorator. */

package Pizza.com;

abstract class Pizza { public abstract double getCost(); public abstract String getDescription(); }

class PlainPizza extends Pizza { @Override public double getCost() { return 10.0; }

@Override
public String getDescription() {
    return "Plain Pizza";
}
}

abstract class ToppingDecorator extends Pizza { protected Pizza pizza;

public ToppingDecorator(Pizza pizza) {
    this.pizza = pizza;
}
}

class CheeseTopping extends ToppingDecorator { public CheeseTopping(Pizza pizza) { super(pizza); }

@Override
public double getCost() {
    return pizza.getCost() + 2.0;
}

@Override
public String getDescription() {
    return pizza.getDescription() + ", Cheese";
}
}

class OliveTopping extends ToppingDecorator { public OliveTopping(Pizza pizza) { super(pizza); }

@Override
public double getCost() {
    return pizza.getCost() + 1.5;
}

@Override
public String getDescription() {
    return pizza.getDescription() + ", Olive";
}
}

class MushroomTopping extends ToppingDecorator { public MushroomTopping(Pizza pizza) { super(pizza); }

@Override
public double getCost() {
    return pizza.getCost() + 2.5;
}

@Override
public String getDescription() {
    return pizza.getDescription() + ", Mushroom";
}
}

public class PizzaDecorator { public static void main(String[] args) { Pizza plainPizza = new PlainPizza(); Pizza cheesePizza = new CheeseTopping(plainPizza); Pizza cheeseOlivePizza = new OliveTopping(cheesePizza); Pizza cheeseOliveMushroomPizza = new MushroomTopping(cheeseOlivePizza);

    System.out.println(cheeseOliveMushroomPizza.getDescription());
    System.out.println(cheeseOliveMushroomPizza.getCost());
}
}

/* 2. Implement a VehicleFactory class in Java using the Factory Method design pattern. The factory should be able to create objects of Car and Bike classes based on the input provided.

*/

// Vehicle interface interface Vehicle { void drive(); }

// Car class implementing Vehicle interface class Car implements Vehicle { @Override public void drive() { System.out.println("Driving a car..."); } }

// Bike class implementing Vehicle interface class Bike implements Vehicle { @Override public void drive() { System.out.println("Riding a bike..."); } }

// VehicleFactory class class VehicleFactory { // Factory method to create a Vehicle object public Vehicle createVehicle(String type) { if ("car".equalsIgnoreCase(type)) { return new Car(); } else if ("bike".equalsIgnoreCase(type)) { return new Bike(); } return null; // Return null for unknown types } }

// Main class to demonstrate the factory public class Q2 { public static void main(String[] args) { VehicleFactory factory = new VehicleFactory();

    // Create a car
    Vehicle car = factory.createVehicle("car");
    if (car != null) car.drive();

    // Create a bike
    Vehicle bike = factory.createVehicle("bike");
    if (bike != null) bike.drive();

    // Try to create an unknown vehicle
    Vehicle unknown = factory.createVehicle("plane");
    if (unknown == null) {
        System.out.println("Unknown vehicle type.");
    }
}
}

/* 3. Implement a Shape interface with a method clone(). Create concrete classes Circle and Rectangle that implement this interface. Use the Prototype pattern to create a new instance of Circle or Rectangle by cloning the existing objects.

*/

// Shape interface with clone() method interface Shape { Shape clone(); void draw(); }

// Circle class implementing Shape interface class Circle implements Shape { private int radius;

public Circle(int radius) {
    this.radius = radius;
}

@Override
public Shape clone() {
    return new Circle(this.radius);
}

@Override
public void draw() {
    System.out.println("Drawing a Circle with radius: " + radius);
}
}

// Rectangle class implementing Shape interface class Rectangle implements Shape { private int width, height;

public Rectangle(int width, int height) {
    this.width = width;
    this.height = height;
}

@Override
public Shape clone() {
    return new Rectangle(this.width, this.height);
}

@Override
public void draw() {
    System.out.println("Drawing a Rectangle with width: " + width + ", height: " + height);
}
}

// Main class to demonstrate the Prototype pattern public class Q3 { public static void main(String[] args) { // Create original Circle and Rectangle Shape originalCircle = new Circle(5); Shape originalRectangle = new Rectangle(4, 6);

    // Clone the Circle and Rectangle
    Shape clonedCircle = originalCircle.clone();
    Shape clonedRectangle = originalRectangle.clone();

    // Draw the original and cloned shapes
    System.out.println("Original Shapes:");
    originalCircle.draw();
    originalRectangle.draw();

    System.out.println("Cloned Shapes:");
    clonedCircle.draw();
    clonedRectangle.draw();
}
}

ASSIGNMEN NO 2
----------------------------------------------------------------------------------------------------------
Q1.Create a Java class DatabaseConnection using the Singleton design pattern. The class 
should have a method getConnection() that returns a single instance of the connection. Ensure 
that only one instance of DatabaseConnection is created even if multiple threads try to access 
it.
ANS:
import java.util.Scanner;

public class DatabaseConnection{

    private static volatile DatabaseConnection instance;

    private DatabaseConnection() {
        System.out.println("DatabaseConnection: Connection established.");
    }

    public static DatabaseConnection getConnection() {
        if (instance == null) {
            synchronized (DatabaseConnection.class) {
                if (instance == null) {
                    instance = new DatabaseConnection();
                }
            }
        }
        return instance;
    }

    public void executeQuery(String query) {
        System.out.println("Executing query: " + query);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a database query: ");
        String query = scanner.nextLine();

        DatabaseConnection dbConnection = DatabaseConnection.getConnection();

        dbConnection.executeQuery(query);

        DatabaseConnection anotherDbConnection = DatabaseConnection.getConnection();

        System.out.println("Are both connections the same instance? " + (dbConnection == anotherDbConnection));


    }
}

----------------------------------------------------------------------------------------------------------------------------------------------------
Q2.Implement a VehicleFactory class in Java using the Factory Method design pattern. The 
factory should be able to create objects of Car and Bike classes based on the input provided.
ANS:
import java.util.Scanner;

interface Vehicle {
    void typeOfVehicle();
}

class Car implements Vehicle {
    @Override
    public void typeOfVehicle() {
        System.out.println("This is a Car.");
    }
}

class Bike implements Vehicle {
    @Override
    public void typeOfVehicle() {
        System.out.println("This is a Bike.");
    }
}


abstract class VehicleFactory {
    public abstract Vehicle createVehicle(String vehicleType);
}

class ConcreteVehicleFactory extends VehicleFactory {
    @Override
    public Vehicle createVehicle(String vehicleType) {
        if (vehicleType == null) {
            return null;
        }
        if (vehicleType.equalsIgnoreCase("Car")) {
            return new Car();
        } else if (vehicleType.equalsIgnoreCase("Bike")) {
            return new Bike();
        }
        return null;
    }
}

public class VehicleFactoryDemo {

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the type of vehicle (Car/Bike): ");
        String vehicleType = scanner.nextLine().trim();

        VehicleFactory vehicleFactory = new ConcreteVehicleFactory();

        Vehicle vehicle = vehicleFactory.createVehicle(vehicleType);

        if (vehicle != null) {
            vehicle.typeOfVehicle();
        } else {
            System.out.println("Invalid vehicle type entered.");
        }

        scanner.close();
    }
}

----------------------------------------------------------------------------------------------------------------------------------------
Q3.Implement a Shape interface with a method clone(). Create concrete classes Circle and 
Rectangle that implement this interface. Use the Prototype pattern to create a new instance of 
Circle or Rectangle by cloning the existing objects.
ANS:
import java.util.Scanner;
interface Shape {
    // Clone method
    Shape clone();
}
class Circle implements Shape {
    private double radius;

    // Constructor
    public Circle(double radius) {
        this.radius = radius;
    }

    // Getter for radius
    public double getRadius() {
        return radius;
    }

    // Setter for radius
    public void setRadius(double radius) {
        this.radius = radius;
    }

    @Override
    public Shape clone() {
        // Create a new Circle with the same radius
        return new Circle(this.radius);
    }

    @Override
    public String toString() {
        return "Circle [radius=" + radius + "]";
    }
}
class Rectangle implements Shape {
    private double length;
    private double width;

    // Constructor
    public Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }

    // Getter for length
    public double getLength() {
        return length;
    }

    // Setter for length
    public void setLength(double length) {
        this.length = length;
    }

    // Getter for width
    public double getWidth() {
        return width;
    }


    public void setWidth(double width) {
        this.width = width;
    }

    @Override
    public Shape clone() {

        return new Rectangle(this.length, this.width);
    }

    @Override
    public String toString() {
        return "Rectangle [length=" + length + ", width=" + width + "]";
    }
}

public class PrototypePatternDemo {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Select the shape to clone (1 for Circle, 2 for Rectangle):");
        int choice = scanner.nextInt();

        Shape shapeToClone = null;

        if (choice == 1) {
            // Circle chosen
            System.out.println("Enter radius for Circle:");
            double radius = scanner.nextDouble();
            shapeToClone = new Circle(radius);
        } else if (choice == 2) {
            // Rectangle chosen
            System.out.println("Enter length and width for Rectangle:");
            double length = scanner.nextDouble();
            double width = scanner.nextDouble();
            shapeToClone = new Rectangle(length, width);
        } else {
            System.out.println("Invalid choice.");
            scanner.close();
            return;
        }

        // Display the original shape
        System.out.println("Original Shape: " + shapeToClone);

        // Clone the shape
        Shape clonedShape = shapeToClone.clone();

        // Display the cloned shape
        System.out.println("Cloned Shape: " + clonedShape);

        scanner.close();
    }
}
---------------------------------------------------------------------------------------------------------------------------------------------
ASSIGNMEN NO 3
-------------------------
Q1. The Product class is currently responsible for both holding product information and 
calculating tax. Refactor the code by separating these responsibilities into distinct classes,
ensuring that each class has only one responsibility.
ANS:
//TIP To <b>Run</b> code, press <shortcut actionId="Run"/> or
// click the <icon src="AllIcons.Actions.Execute"/> icon in the gutter.
class Product {
    private String name;
    private double price;

    public Product(String name, double price) {
        this.name = name;
        this.price = price;
    }

    // Getters
    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }
}
class TaxCalculator {
    private double taxRate;

    public TaxCalculator(double taxRate) {
        this.taxRate = taxRate;
    }

    public double calculateTax(Product product) {
        return product.getPrice() * taxRate;
    }

    public double calculatePriceWithTax(Product product) {
        return product.getPrice() + calculateTax(product);
    }
}

public class Main {
    public static void main(String[] args) {
        Product product = new Product("Laptop", 1000);
        TaxCalculator taxCalculator = new TaxCalculator(0.15); // 15% tax rate

        double taxAmount = taxCalculator.calculateTax(product);
        double totalPrice = taxCalculator.calculatePriceWithTax(product);

        System.out.println("Product: " + product.getName());
        System.out.println("Price: " + product.getPrice());
        System.out.println("Tax: " + taxAmount);
        System.out.println("Total Price with Tax: " + totalPrice);
    }
}

------------------------------------------------------------------------------------------------------------------------------------------------  
Q2. Refactor the ShapeCalculator that calculates areas for Circle and Rectangle. Allow it to 
support new shapes (like Triangle) without modifying the existing code. Make it easy to add 
future shapes.
ANS:
interface Shape1 {
    double calculateArea();
}
class Circle1 implements Shape1 {
    private double radius;

    public Circle1(double radius) {
        this.radius = radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}
class Rectangle1 implements Shape1 {
    private double width;
    private double height;

    public Rectangle1(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double calculateArea() {
        return width * height;
    }
}
class Triangle1 implements Shape1 {
    private double base;
    private double height;

    public Triangle1(double base, double height) {
        this.base = base;
        this.height = height;
    }

    @Override
    public double calculateArea() {
        return 0.5 * base * height;
    }
}
class ShapeCalculator {
    public double calculateArea(Shape shape) {
        return shape.calculateArea();
    }
}
public class q2 {
    public static void main(String[] args) {
        Shape circle = new Circle(5);
        Shape rectangle = new Rectangle(4, 6);
        Shape triangle = new Triangle(4, 5);

        ShapeCalculator calculator = new ShapeCalculator();

        System.out.println("Circle Area: " + calculator.calculateArea(circle));
        System.out.println("Rectangle Area: " + calculator.calculateArea(rectangle));
        System.out.println("Triangle Area: " + calculator.calculateArea(triangle));
    }
}
-------------------------------------------------------------------------------------------------------------------------------------------
Q3. The SavingsAccount class alters how interest is calculated compared to the Account class, 
breaking the Liskov Substitution Principle (LSP). Refactor the code so that SavingsAccount
can replace Account without affecting functionality. Keep interest calculation logic uniform 
for all account types.
ANS:
interface InterestCalculator {
    double calculateInterest(double balance);
}
class DefaultInterestCalculator implements InterestCalculator {
    @Override
    public double calculateInterest(double balance) {
        return balance * 0.03;  // Default 3% interest
    }
}

class SavingsInterestCalculator implements InterestCalculator {
    @Override
    public double calculateInterest(double balance) {
        return balance * 0.05;  // 5% interest for Savings Account
    }
}
class Account {
    protected double balance;
    private InterestCalculator interestCalculator;

    public Account(double balance, InterestCalculator interestCalculator) {
        this.balance = balance;
        this.interestCalculator = interestCalculator;
    }

    public double calculateInterest() {
        return interestCalculator.calculateInterest(balance);
    }

    public double getBalance() {
        return balance;
    }
}

class SavingsAccount extends Account {
    public SavingsAccount(double balance) {
        super(balance, new SavingsInterestCalculator());
    }
}
public class q3 {
    public static void main(String[] args) {
        Account regularAccount = new Account(1000, new DefaultInterestCalculator());
        Account savingsAccount = new SavingsAccount(1000);

        System.out.println("Regular Account Interest: " + regularAccount.calculateInterest());
        System.out.println("Savings Account Interest: " + savingsAccount.calculateInterest());
    }
}
----------------------------------------------------------------------------------------------------------------------------------------------
Q4. Refactor the TaskManager interface, which has methods like createTask(),deleteTask(), 
assignTask(), and markTaskAsComplete(). Break it into smaller interfaces: TaskCreation, 
TaskAssignment, and TaskCompletion. Ensure classes only implement the interfaces they 
actually need.
ANS:
interface TaskCreation {
    void createTask();
}

// TaskAssignment interface
interface TaskAssignment {
    void assignTask();
}

// TaskCompletion interface
interface TaskCompletion {
    void markTaskAsComplete();
}

// TaskDeletion interface
interface TaskDeletion {
    void deleteTask();
}

// A class that only needs to create and complete tasks
class SimpleTaskManager implements TaskCreation, TaskCompletion {
    @Override
    public void createTask() {
        System.out.println("Task created.");
    }

    @Override
    public void markTaskAsComplete() {
        System.out.println("Task completed.");
    }
}

// Another class that needs to assign and delete tasks
class AdvancedTaskManager implements TaskAssignment, TaskDeletion {
    @Override
    public void assignTask() {
        System.out.println("Task assigned.");
    }

    @Override
    public void deleteTask() {
        System.out.println("Task deleted.");
    }
}
public class q4 {
    public static void main(String[] args) {
        TaskCreation simpleTaskManager = new SimpleTaskManager();
        TaskAssignment advancedTaskManager = new AdvancedTaskManager();

        simpleTaskManager.createTask();
        ((TaskCompletion) simpleTaskManager).markTaskAsComplete();

        advancedTaskManager.assignTask();
        ((TaskDeletion) advancedTaskManager).deleteTask();
    }
}
------------------------------------------------------------------------------------------------------------------------------------------------
ASSIGNMEN NO 4
----------------------
/*
1.Create a directory structure using the Composite pattern. You should be able to add File and Folder objects.
 The Folder can contain multiple File objects and other Folder objects.
Hint:
•	Create a Component interface with methods like showDetails().
•	Implement File and Folder classes based on this interface.

*/


package Ass4.com;

import java.util.ArrayList;
import java.util.List;
// Component interface
interface FileSystemComponent {
    void showDetails();
}

// File class implementing the Component interface
class File implements FileSystemComponent {
    private String name;

    public File(String name) {
        this.name = name;
    }

    @Override
    public void showDetails() {
        System.out.println("File: " + name);
    }
}

// Folder class implementing the Component interface
class Folder implements FileSystemComponent {
    private String name;
    private List<FileSystemComponent> components = new ArrayList<>();

    public Folder(String name) {
        this.name = name;
    }

    public void add(FileSystemComponent component) {
        components.add(component);
    }

    @Override
    public void showDetails() {
        System.out.println("Folder: " + name);
        for (FileSystemComponent component : components) {
            component.showDetails();
        }
    }
}

// Main class to demonstrate the Composite pattern
public class assQ1 {
    public static void main(String[] args) {
        // Create files
        File file1 = new File("File1.txt");
        File file2 = new File("File2.txt");
        File file3 = new File("File3.txt");

        // Create folders
        Folder folder1 = new Folder("Folder1");
        Folder folder2 = new Folder("Folder2");
        Folder rootFolder = new Folder("RootFolder");

        // Build the directory structure
        folder1.add(file1);
        folder1.add(file2);

        folder2.add(file3);

        rootFolder.add(folder1);
        rootFolder.add(folder2);

        // Display the directory structure
        rootFolder.showDetails();
    }
}



-----------------------------------------------------------------------------------------------------------------------------------------

/*
  2. Implement a bridge pattern where you have a Vehicle interface with methods startEngine() and
   stopEngine(). You also have two types of Engine classes: PetrolEngine and ElectricEngine.
   Implement two vehicle types: Car and Motorbike. Each vehicle should be able to use either type of engine,
    demonstrating the flexibility of the bridge pattern.
Hint:
•	Vehicle interface will use Engine interface methods.

*/

interface Engine {
    void start();
    void stop();
}

class PetrolEngine implements Engine {
    @Override
    public void start() {
        System.out.println("Petrol engine started.");
    }

    @Override
    public void stop() {
        System.out.println("Petrol engine stopped.");
    }
}

class ElectricEngine implements Engine {
    @Override
    public void start() {
        System.out.println("Electric engine started.");
    }

    @Override
    public void stop() {
        System.out.println("Electric engine stopped.");
    }
}

interface Vehicle {
    void startEngine();
    void stopEngine();
}

class Car implements Vehicle {
    private Engine engine;

    public Car(Engine engine) {
        this.engine = engine;
    }

    @Override
    public void startEngine() {
        engine.start();
    }

    @Override
    public void stopEngine() {
        engine.stop();
    }
}

class Motorbike implements Vehicle {
    private Engine engine;

    public Motorbike(Engine engine) {
        this.engine = engine;
    }

    @Override
    public void startEngine() {
        engine.start();
    }

    @Override
    public void stopEngine() {
        engine.stop();
    }
}

public class assQ2 {
    public static void main(String[] args) {
        Car petrolCar = new Car(new PetrolEngine());
        Car electricCar = new Car(new ElectricEngine());

        Motorbike petrolBike = new Motorbike(new PetrolEngine());
        Motorbike electricBike = new Motorbike(new ElectricEngine());

        petrolCar.startEngine();
        petrolCar.stopEngine();

        electricCar.startEngine();
        electricCar.stopEngine();

        petrolBike.startEngine();
        petrolBike.stopEngine();

        electricBike.startEngine();
        electricBike.stopEngine();
    }
}

----------------------------------------------------------------------------------------------------------------------------------------Q3. You are tasked with designing an organizational structure using the composite pattern. 
/*
3. You are tasked with designing an organizational structure using the composite pattern.
Create a Employee class and a Manager class. A Manager can have multiple employees reporting to them.
Implement the structure where a Manager can delegate tasks to Employee objects and also manage other Manager objects.
Hint:
•	Use the composite pattern to represent managers and employees as a tree structure.

*/

package Ass4.com;
import java.util.ArrayList;
import java.util.List;

interface Employee {
    void doTask();
}

class Manager implements Employee {
    private String name;
    private List<Employee> subordinates;

    public Manager(String name) {
        this.name = name;
        this.subordinates = new ArrayList<>();
    }

    public void addSubordinate(Employee employee) {
        subordinates.add(employee);
    }

    @Override
    public void doTask() {
        System.out.println(name + " is managing tasks.");
        for (Employee subordinate : subordinates) {
            subordinate.doTask();
        }
    }
}

class Worker implements Employee {
    private String name;

    public Worker(String name) {
        this.name = name;
    }

    @Override
    public void doTask() {
        System.out.println(name + " is doing a task.");
    }
}

public class ass3 {
    public static void main(String[] args) {
        // Create a hierarchical structure
        Manager ceo = new Manager("CEO");
        Manager manager1 = new Manager("Manager 1");
        Manager manager2 = new Manager("Manager 2");
        Worker worker1 = new Worker("Worker 1");
        Worker worker2 = new Worker("Worker 2");
        Worker worker3 = new Worker("Worker 3");

        ceo.addSubordinate(manager1);
        ceo.addSubordinate(manager2);
        manager1.addSubordinate(worker1);
        manager1.addSubordinate(worker2);
        manager2.addSubordinate(worker3);

        // Delegate tasks
        ceo.doTask();
    }
}
---------------------------------------------------------------------------------------------------------------------------------------------
/*
4. Implement a proxy pattern to control access to a BankAccount class.
The real class BankAccount has methods like deposit() and withdraw().
The BankAccountProxy will control access to these methods, ensuring that withdrawals can only be made if the account has sufficient balance.
Hint:
•	The proxy class can check if the account has enough balance before allowing the withdrawal.

*/

interface BankAccount {
    void deposit(double amount);
    void withdraw(double amount);
}

class RealBankAccount implements BankAccount {
    private double balance;

    public RealBankAccount(double initialBalance) {
        this.balance = initialBalance;
    }

    @Override
    public void deposit(double amount) {
        balance += amount;
        System.out.println("Deposited: " + amount);
    }

    @Override
    public void withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
            System.out.println("Withdrew: " + amount);
        } else {
            System.out.println("Insufficient balance.");
        }
    }

    public double getBalance() {
        return balance;
    }
}

class BankAccountProxy implements BankAccount {
    private RealBankAccount realAccount;

    public BankAccountProxy(RealBankAccount realAccount) {
        this.realAccount = realAccount;
    }

    @Override
    public void deposit(double amount) {
        realAccount.deposit(amount);
    }

    @Override
    public void withdraw(double amount) {
        if (realAccount.getBalance() >= amount) {
            realAccount.withdraw(amount);
        } else {
            System.out.println("Insufficient balance.");
        }
    }
}

public class assQ4 {
    public static void main(String[] args) {
        RealBankAccount account = new RealBankAccount(1000);
        BankAccountProxy proxy = new BankAccountProxy(account);

        proxy.deposit(500);
        proxy.withdraw(2000); // Insufficient balance
        proxy.withdraw(1000);
    }
}

-------------------------------------------------------------------------------------------------------------------
