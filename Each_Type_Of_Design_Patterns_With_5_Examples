This is a big topic. Let me break it down clearly and thoroughly.

---

# The 3 Types of Design Patterns

Design patterns are divided into 3 categories based on **what problem they solve**:

| Type | Solves | Simple Meaning |
|---|---|---|
| **Creational** | Object creation | How to create objects smartly |
| **Structural** | Object composition | How to combine objects together |
| **Behavioral** | Object communication | How objects talk to each other |

---

# Type 1 — Creational Patterns

> *"How should I create this object?"*

---

## 1. Singleton

Ensures only **one instance** of a class exists throughout the application.

**Real world:** Database connection, Logger, Config manager

```javascript
class DatabaseConnection {
  constructor() {
    if (DatabaseConnection.instance) {
      return DatabaseConnection.instance;
    }
    this.connection = "Connected to DB"; // expensive operation
    DatabaseConnection.instance = this;
  }

  getConnection() {
    return this.connection;
  }
}

const db1 = new DatabaseConnection();
const db2 = new DatabaseConnection();

console.log(db1 === db2);          // true — same instance
console.log(db1.getConnection());  // Connected to DB
```

**When to use:** When exactly one object is needed to coordinate across the system.

---

## 2. Factory

Creates objects without exposing the **instantiation logic** to the caller.

**Real world:** Payment methods, File exporters, Notification senders

```javascript
class SMSNotification {
  send(message) {
    console.log("SMS sent:", message);
  }
}

class EmailNotification {
  send(message) {
    console.log("Email sent:", message);
  }
}

class PushNotification {
  send(message) {
    console.log("Push sent:", message);
  }
}

class NotificationFactory {
  static create(type) {
    switch (type) {
      case "sms":   return new SMSNotification();
      case "email": return new EmailNotification();
      case "push":  return new PushNotification();
      default: throw new Error(`Unknown type: ${type}`);
    }
  }
}

// Caller never knows which class is instantiated
const notification = NotificationFactory.create("email");
notification.send("Your order is confirmed!");
```

**When to use:** When the exact type of object to create is decided at runtime.

---

## 3. Abstract Factory

Creates **families of related objects** without specifying their concrete classes.

**Real world:** UI themes (Dark/Light), Cross-platform widgets

```javascript
// Dark theme family
class DarkButton {
  render() { console.log("Rendering Dark Button"); }
}
class DarkInput {
  render() { console.log("Rendering Dark Input"); }
}

// Light theme family
class LightButton {
  render() { console.log("Rendering Light Button"); }
}
class LightInput {
  render() { console.log("Rendering Light Input"); }
}

// Abstract factories
class DarkThemeFactory {
  createButton() { return new DarkButton(); }
  createInput()  { return new DarkInput();  }
}

class LightThemeFactory {
  createButton() { return new LightButton(); }
  createInput()  { return new LightInput();  }
}

// UI renderer — never knows which theme it uses
class UIRenderer {
  constructor(factory) {
    this.button = factory.createButton();
    this.input  = factory.createInput();
  }

  render() {
    this.button.render();
    this.input.render();
  }
}

// Swap entire theme without touching UIRenderer
const darkUI = new UIRenderer(new DarkThemeFactory());
darkUI.render();

const lightUI = new UIRenderer(new LightThemeFactory());
lightUI.render();
```

**When to use:** When you need to create multiple related objects that must work together.

---

## 4. Builder

Builds a **complex object step by step**. Separates construction from representation.

**Real world:** Query builder, Form builder, Pizza ordering system

```javascript
class Pizza {
  constructor() {
    this.size     = null;
    this.crust    = null;
    this.toppings = [];
    this.sauce    = null;
  }

  describe() {
    console.log(
      `Pizza: ${this.size} size, ${this.crust} crust, 
       ${this.sauce} sauce, toppings: ${this.toppings.join(", ")}`
    );
  }
}

class PizzaBuilder {
  constructor() {
    this.pizza = new Pizza();
  }

  setSize(size) {
    this.pizza.size = size;
    return this; // allows chaining
  }

  setCrust(crust) {
    this.pizza.crust = crust;
    return this;
  }

  setSauce(sauce) {
    this.pizza.sauce = sauce;
    return this;
  }

  addTopping(topping) {
    this.pizza.toppings.push(topping);
    return this;
  }

  build() {
    return this.pizza;
  }
}

// Build complex object step by step
const pizza = new PizzaBuilder()
  .setSize("Large")
  .setCrust("Thin")
  .setSauce("Tomato")
  .addTopping("Cheese")
  .addTopping("Mushrooms")
  .addTopping("Olives")
  .build();

pizza.describe();
```

**When to use:** When an object needs many optional configuration steps.

---

## 5. Prototype

Creates new objects by **cloning an existing object** instead of creating from scratch.

**Real world:** Game characters, Document templates, Config copying

```javascript
class Character {
  constructor(name, health, weapon, speed) {
    this.name   = name;
    this.health = health;
    this.weapon = weapon;
    this.speed  = speed;
  }

  clone() {
    // Creates a copy of this character
    return new Character(
      this.name,
      this.health,
      this.weapon,
      this.speed
    );
  }

  describe() {
    console.log(
      `${this.name} — Health: ${this.health}, 
       Weapon: ${this.weapon}, Speed: ${this.speed}`
    );
  }
}

// Create base character once
const baseWarrior = new Character("Warrior", 100, "Sword", 5);

// Clone and customize — no need to rebuild from scratch
const warrior1 = baseWarrior.clone();
warrior1.name = "Warrior 1";
warrior1.weapon = "Axe";

const warrior2 = baseWarrior.clone();
warrior2.name = "Warrior 2";
warrior2.health = 150;

baseWarrior.describe(); // Warrior   — Health: 100, Weapon: Sword, Speed: 5
warrior1.describe();    // Warrior 1 — Health: 100, Weapon: Axe,   Speed: 5
warrior2.describe();    // Warrior 2 — Health: 150, Weapon: Sword, Speed: 5
```

**When to use:** When creating an object is expensive and you need many similar copies.

---

# Type 2 — Structural Patterns

> *"How should I connect and organize these objects?"*

---

## 1. Adapter

Makes **two incompatible interfaces work together**. Like a power plug adapter.

**Real world:** Third party library integration, Legacy code wrapping

```javascript
// Old payment system — legacy code you can't change
class OldPaymentSystem {
  makePayment(dollars) {
    console.log(`Old system: Paid $${dollars}`);
  }
}

// New interface your app expects
class NewPaymentSystem {
  processPayment(amount, currency) {
    throw new Error("processPayment() must be implemented");
  }
}

// Adapter — wraps old system to match new interface
class PaymentAdapter extends NewPaymentSystem {
  constructor() {
    super();
    this.oldSystem = new OldPaymentSystem();
  }

  processPayment(amount, currency) {
    console.log(`Adapter: Converting ${currency} to dollars...`);
    this.oldSystem.makePayment(amount); // delegates to old system
  }
}

// App only knows about NewPaymentSystem interface
const payment = new PaymentAdapter();
payment.processPayment(100, "USD");
```

**When to use:** When integrating a third party library or legacy code with a different interface.

---

## 2. Decorator

**Adds new behavior** to an object dynamically without changing its class.

**Real world:** Coffee customization, Middleware, Logging wrappers

```javascript
// Base coffee
class Coffee {
  cost()        { return 5;       }
  description() { return "Coffee"; }
}

// Base decorator
class CoffeeDecorator {
  constructor(coffee) {
    this.coffee = coffee;
  }
  cost()        { return this.coffee.cost();        }
  description() { return this.coffee.description(); }
}

// Each addon wraps the previous one
class MilkDecorator extends CoffeeDecorator {
  cost()        { return this.coffee.cost() + 2;           }
  description() { return this.coffee.description() + ", Milk"; }
}

class SugarDecorator extends CoffeeDecorator {
  cost()        { return this.coffee.cost() + 1;            }
  description() { return this.coffee.description() + ", Sugar"; }
}

class WhipDecorator extends CoffeeDecorator {
  cost()        { return this.coffee.cost() + 3;           }
  description() { return this.coffee.description() + ", Whip"; }
}

// Build dynamically — add as many addons as needed
let myCoffee = new Coffee();
myCoffee = new MilkDecorator(myCoffee);
myCoffee = new SugarDecorator(myCoffee);
myCoffee = new WhipDecorator(myCoffee);

console.log(myCoffee.description()); // Coffee, Milk, Sugar, Whip
console.log("Total: $" + myCoffee.cost()); // Total: $11
```

**When to use:** When you want to add responsibilities to an object without subclassing.

---

## 3. Facade

Provides a **simplified interface** to a complex subsystem.

**Real world:** Home theatre system, API wrappers, Library interfaces

```javascript
// Complex subsystems
class DVDPlayer {
  on()       { console.log("DVD Player on");      }
  play()     { console.log("DVD playing");        }
  off()      { console.log("DVD Player off");     }
}

class Projector {
  on()       { console.log("Projector on");       }
  setInput() { console.log("Projector input set");}
  off()      { console.log("Projector off");      }
}

class SoundSystem {
  on()          { console.log("Sound system on");      }
  setVolume(v)  { console.log(`Volume set to ${v}`);   }
  off()         { console.log("Sound system off");     }
}

class Lights {
  dim()   { console.log("Lights dimmed");  }
  on()    { console.log("Lights on");      }
}

// Facade — one simple interface hides all complexity
class HomeTheatreFacade {
  constructor() {
    this.dvd       = new DVDPlayer();
    this.projector = new Projector();
    this.sound     = new SoundSystem();
    this.lights    = new Lights();
  }

  watchMovie() {
    console.log("--- Starting Movie ---");
    this.lights.dim();
    this.projector.on();
    this.projector.setInput();
    this.sound.on();
    this.sound.setVolume(20);
    this.dvd.on();
    this.dvd.play();
  }

  endMovie() {
    console.log("--- Ending Movie ---");
    this.dvd.off();
    this.sound.off();
    this.projector.off();
    this.lights.on();
  }
}

// Caller only interacts with one simple interface
const theatre = new HomeTheatreFacade();
theatre.watchMovie();
theatre.endMovie();
```

**When to use:** When you want to provide a simple interface to a complex set of classes.

---

## 4. Composite

Treats **individual objects and groups of objects** the same way.

**Real world:** File system (files and folders), UI components, Organization hierarchy

```javascript
// Base component
class FileSystemItem {
  getName()    { throw new Error("getName() must be implemented");    }
  getSize()    { throw new Error("getSize() must be implemented");    }
  display(indent = "") { throw new Error("display() must be implemented"); }
}

// Leaf — single file
class File extends FileSystemItem {
  constructor(name, size) {
    super();
    this.name = name;
    this.size = size;
  }

  getName()          { return this.name;                             }
  getSize()          { return this.size;                             }
  display(indent="") { console.log(`${indent}📄 ${this.name} (${this.size}kb)`); }
}

// Composite — folder contains files or other folders
class Folder extends FileSystemItem {
  constructor(name) {
    super();
    this.name     = name;
    this.children = [];
  }

  add(item)     { this.children.push(item);                          }
  getName()     { return this.name;                                  }
  getSize()     { return this.children.reduce((sum, child) => sum + child.getSize(), 0); }

  display(indent = "") {
    console.log(`${indent}📁 ${this.name}`);
    this.children.forEach(child => child.display(indent + "  "));
  }
}

// Build tree structure
const root = new Folder("root");
const src  = new Folder("src");
const test = new Folder("test");

src.add(new File("index.js",  10));
src.add(new File("app.js",    20));
test.add(new File("app.test.js", 5));

root.add(src);
root.add(test);
root.add(new File("package.json", 2));

root.display();
console.log("Total size:", root.getSize(), "kb"); // 37kb
```

**When to use:** When you need to treat single objects and groups of objects uniformly.

---

## 5. Proxy

Provides a **substitute or placeholder** for another object to control access to it.

**Real world:** Lazy loading, Caching, Access control, Logging

```javascript
// Real service — expensive to call
class RealWeatherService {
  getWeather(city) {
    console.log(`Calling real API for ${city}...`);
    return { city, temperature: 28, condition: "Sunny" };
  }
}

// Proxy — adds caching without changing RealWeatherService
class WeatherServiceProxy {
  constructor() {
    this.realService = new RealWeatherService();
    this.cache       = {};
  }

  getWeather(city) {
    if (this.cache[city]) {
      console.log(`Cache hit for ${city}`);
      return this.cache[city];
    }

    const result      = this.realService.getWeather(city);
    this.cache[city]  = result; // store in cache
    return result;
  }
}

const weather = new WeatherServiceProxy();

console.log(weather.getWeather("Chennai")); // calls real API
console.log(weather.getWeather("Chennai")); // returns from cache
console.log(weather.getWeather("Mumbai"));  // calls real API
console.log(weather.getWeather("Mumbai"));  // returns from cache
```

**When to use:** When you need to add access control, caching, or logging around an object.

---

# Type 3 — Behavioral Patterns

> *"How should these objects communicate and share responsibility?"*

---

## 1. Strategy

Defines a family of algorithms and makes them **interchangeable at runtime**.

**Real world:** Sorting algorithms, Payment methods, Compression formats

```javascript
// You have already mastered this one across all 7 problems!

class SortStrategy {
  sort(data) { throw new Error("sort() must be implemented"); }
}

class BubbleSort extends SortStrategy {
  sort(data) {
    console.log("Sorting using Bubble Sort");
    return [...data].sort((a, b) => a - b);
  }
}

class QuickSort extends SortStrategy {
  sort(data) {
    console.log("Sorting using Quick Sort");
    return [...data].sort((a, b) => a - b);
  }
}

class MergeSort extends SortStrategy {
  sort(data) {
    console.log("Sorting using Merge Sort");
    return [...data].sort((a, b) => a - b);
  }
}

class Sorter {
  constructor(strategy) {
    this.strategy = strategy;
  }

  setStrategy(strategy) {
    this.strategy = strategy;
  }

  sort(data) {
    return this.strategy.sort(data);
  }
}

const data   = [5, 2, 8, 1, 9, 3];
const sorter = new Sorter(new BubbleSort());

console.log(sorter.sort(data));

sorter.setStrategy(new QuickSort());
console.log(sorter.sort(data));
```

**When to use:** When you want to swap algorithms or behaviors at runtime.

---

## 2. Observer

Defines a **one-to-many dependency** so when one object changes, all dependents are notified automatically.

**Real world:** Event systems, Stock price alerts, Social media notifications

```javascript
// You implemented this in Problem 1!

class Subject {
  constructor() {
    this.observers = [];
  }

  subscribe(observer)   { this.observers.push(observer);                              }
  unsubscribe(observer) { this.observers = this.observers.filter(o => o !== observer);}
  notify(data)          { this.observers.forEach(o => o.update(data));                }
}

class StockMarket extends Subject {
  constructor() {
    super();
    this.price = 0;
  }

  setPrice(price) {
    this.price = price;
    console.log(`Stock price changed to $${price}`);
    this.notify(price);
  }
}

class StockAlert {
  constructor(name) { this.name = name; }
  update(price) {
    console.log(`${this.name} notified: new price $${price}`);
  }
}

const market  = new StockMarket();
const alice   = new StockAlert("Alice");
const bob     = new StockAlert("Bob");
const charlie = new StockAlert("Charlie");

market.subscribe(alice);
market.subscribe(bob);
market.subscribe(charlie);

market.setPrice(150);

market.unsubscribe(bob);

market.setPrice(200); // bob not notified
```

**When to use:** When a change in one object requires updating many others automatically.

---

## 3. Template Method

Defines the **skeleton of an algorithm** in a base class and lets subclasses fill in specific steps.

**Real world:** Data processing pipelines, Login flows, Report generation

```javascript
// You implemented this in Problem 7!

class DataProcessor {
  // Template method — fixed skeleton
  process(data) {
    const extracted  = this.extract(data);
    const transformed = this.transform(extracted);
    this.load(transformed);
  }

  extract(data)          { throw new Error("extract() must be implemented");    }
  transform(data)        { throw new Error("transform() must be implemented");  }
  load(data)             { console.log("Loading data:", data);                  }
}

class CSVProcessor extends DataProcessor {
  extract(data) {
    console.log("Extracting CSV data");
    return data.split(",");
  }

  transform(data) {
    console.log("Transforming CSV data");
    return data.map(item => item.trim().toUpperCase());
  }
}

class JSONProcessor extends DataProcessor {
  extract(data) {
    console.log("Extracting JSON data");
    return JSON.parse(data);
  }

  transform(data) {
    console.log("Transforming JSON data");
    return Object.entries(data).map(([k, v]) => `${k}:${v}`);
  }
}

const csvProcessor  = new CSVProcessor();
csvProcessor.process("gobi, kumar, developer");

const jsonProcessor = new JSONProcessor();
jsonProcessor.process('{"name":"gobi","role":"developer"}');
```

**When to use:** When multiple classes share the same algorithm structure but differ in specific steps.

---

## 4. Chain of Responsibility

Passes a request along a **chain of handlers** until one handles it.

**Real world:** Middleware, Support ticket escalation, Request validation

```javascript
class Handler {
  constructor(name) {
    this.name = name;
    this.next = null;
  }

  setNext(handler) {
    this.next = handler;
    return handler; // allows chaining
  }

  handle(request) {
    if (this.next) {
      return this.next.handle(request);
    }
    console.log(`No handler found for: ${request}`);
  }
}

class LevelOneSupport extends Handler {
  handle(request) {
    if (request === "password reset") {
      console.log(`${this.name}: Handling password reset`);
    } else {
      console.log(`${this.name}: Can't handle. Escalating...`);
      super.handle(request);
    }
  }
}

class LevelTwoSupport extends Handler {
  handle(request) {
    if (request === "billing issue") {
      console.log(`${this.name}: Handling billing issue`);
    } else {
      console.log(`${this.name}: Can't handle. Escalating...`);
      super.handle(request);
    }
  }
}

class LevelThreeSupport extends Handler {
  handle(request) {
    console.log(`${this.name}: Handling critical issue — ${request}`);
  }
}

// Build the chain
const level1 = new LevelOneSupport("Level 1");
const level2 = new LevelTwoSupport("Level 2");
const level3 = new LevelThreeSupport("Level 3");

level1.setNext(level2).setNext(level3);

// Each request travels the chain until handled
console.log("--- Password Reset ---");
level1.handle("password reset");

console.log("\n--- Billing Issue ---");
level1.handle("billing issue");

console.log("\n--- Server Down ---");
level1.handle("server down");
```

**When to use:** When more than one object may handle a request and the handler is not known upfront.

---

## 5. Command

Encapsulates a **request as an object**, allowing you to queue, undo, or log operations.

**Real world:** Undo/Redo in text editors, Remote controls, Task queues

```javascript
// Command interface
class Command {
  execute() { throw new Error("execute() must be implemented"); }
  undo()    { throw new Error("undo() must be implemented");    }
}

// Receiver — the actual object being controlled
class TextEditor {
  constructor() { this.content = ""; }
  write(text)   { this.content += text;                              }
  delete(count) { this.content = this.content.slice(0, -count);     }
  getContent()  { return this.content;                               }
}

// Concrete commands
class WriteCommand extends Command {
  constructor(editor, text) {
    super();
    this.editor = editor;
    this.text   = text;
  }

  execute() { this.editor.write(this.text);         }
  undo()    { this.editor.delete(this.text.length); }
}

// Invoker — controls command execution and history
class CommandManager {
  constructor() { this.history = []; }

  execute(command) {
    command.execute();
    this.history.push(command);
    console.log("Content:", this.history[this.history.length - 1]
      .editor.getContent());
  }

  undo() {
    const command = this.history.pop();
    if (command) {
      command.undo();
      console.log("After undo:", command.editor.getContent());
    }
  }
}

const editor  = new TextEditor();
const manager = new CommandManager();

manager.execute(new WriteCommand(editor, "Hello "));
manager.execute(new WriteCommand(editor, "World"));
manager.execute(new WriteCommand(editor, "!!!"));

console.log("--- Undo ---");
manager.undo(); // removes !!!
manager.undo(); // removes World
```

**When to use:** When you need undo/redo, operation queuing, or logging of requests.

---

# Complete Summary

## Creational — *How to create*

| Pattern | One Line | Your Problems |
|---|---|---|
| Singleton | One instance only | EventBus |
| Factory | Create by type string | FileExporter, Checkout |
| Abstract Factory | Create families of objects | UI Themes |
| Builder | Build step by step | Pizza, Query builders |
| Prototype | Clone existing objects | Game characters |

## Structural — *How to connect*

| Pattern | One Line | Your Problems |
|---|---|---|
| Adapter | Make incompatible things work | Legacy integrations |
| Decorator | Add behavior by wrapping | DiscountEngine |
| Facade | Simplify complex systems | Home Theatre |
| Composite | Treat one and many the same | File System |
| Proxy | Control access to an object | Weather cache |

## Behavioral — *How to communicate*

| Pattern | One Line | Your Problems |
|---|---|---|
| Strategy | Swap algorithms at runtime | All 7 problems |
| Observer | Notify many when one changes | EventBus |
| Template Method | Fixed skeleton, flexible steps | LoginSystem |
| Chain of Responsibility | Pass request along a chain | Support tickets |
| Command | Encapsulate request as object | Text editor undo |

---

## The Biggest Insight

Look at the problems you solved across this conversation — you have already **used 6 of these 15 patterns** without even realizing it:

- Strategy → every single problem
- Observer → EventBus
- Factory → FileExporter, Checkout, DiscountEngine
- Singleton → EventBus
- Decorator → DiscountEngine
- Template Method → LoginSystem

You didn't just learn design patterns today. **You practiced them.**