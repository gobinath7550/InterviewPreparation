Here are 10 problems similar to the cache interview — each one tests **implementation + design pattern + SOLID principles** together, just like you experienced.

---

## The 10 Problems

### 1. 🔔 Event System (Publisher-Subscriber)

Design an in-memory event bus where components can **subscribe to events** and **publish events**. Subscribers should be pluggable — you can add or remove them at runtime.

- _Pattern to discover:_ Observer
- _SOLID to watch:_ Open/Closed Principle

---

### 2. 📝 Logger with Multiple Outputs

Build a logger that can write to **Console, File, and Database**. The output destination should be configurable. Adding a new destination should not require changing the Logger class.

- _Pattern to discover:_ Strategy / Chain of Responsibility
- _SOLID to watch:_ Single Responsibility, Open/Closed

---

### 3. 💳 Payment Processing System

Implement a checkout system that supports **multiple payment methods** (Credit Card, UPI, Wallet, NetBanking). The payment method should be swappable without touching the order processing logic.

- _Pattern to discover:_ Strategy
- _SOLID to watch:_ Dependency Inversion

---

### 4. 🗂️ File Exporter

Build a report exporter that can export data as **PDF, CSV, or Excel**. The format should be decided at runtime, and adding a new format should require zero changes to existing code.

- _Pattern to discover:_ Strategy / Factory
- _SOLID to watch:_ Open/Closed, Interface Segregation

---

### 5. 🔁 Retry Mechanism

Design a retry utility where you can execute any operation with a **pluggable retry policy** — Fixed Delay, Exponential Backoff, or No Retry. The caller should not care about which policy is active.

- _Pattern to discover:_ Strategy / Template Method
- _SOLID to watch:_ Single Responsibility, Dependency Inversion

---

### 6. 🛒 Discount Engine

Build a pricing engine where **discount rules** (Flat, Percentage, Buy-1-Get-1) can be applied to a cart. Rules should be composable and adding new rules should not break existing ones.

- _Pattern to discover:_ Strategy / Decorator
- _SOLID to watch:_ Open/Closed, Single Responsibility

---

### 7. 🔐 Authentication System

Implement a login system that supports **multiple auth methods** — Username/Password, OTP, OAuth. The core login flow should remain unchanged regardless of which method is used.

- _Pattern to discover:_ Strategy / Template Method
- _SOLID to watch:_ Liskov Substitution, Dependency Inversion

---

### 8. 📦 Notification Service

Build a notification system that sends alerts via **Email, SMS, and Push**. A single event should be able to trigger multiple notification channels simultaneously.

- _Pattern to discover:_ Observer / Decorator
- _SOLID to watch:_ Interface Segregation, Open/Closed

---

### 9. 🗄️ Database Connection Pool

Design a connection pool that manages reusable database connections with a **pluggable pool size strategy** — Fixed Pool, Dynamic Pool. Getting and releasing connections should be clean and thread-safe.

- _Pattern to discover:_ Object Pool / Strategy
- _SOLID to watch:_ Single Responsibility, Dependency Inversion

---

### 10. 🧾 Order Processing Pipeline

Build an order pipeline where each step — **Validate → Apply Discount → Calculate Tax → Notify** — is a separate pluggable stage. Steps should be reorderable and new steps should be addable without changing the pipeline core.

- _Pattern to discover:_ Chain of Responsibility / Pipeline
- _SOLID to watch:_ Single Responsibility, Open/Closed

---

## How to Practice Each One

For every problem, challenge yourself to answer these 4 questions **before looking anything up:**

| Question                                      | Why It Matters                        |
| --------------------------------------------- | ------------------------------------- |
| What interfaces will I create?                | Tests your abstraction thinking       |
| Which class has more than one responsibility? | Tests SRP awareness                   |
| What changes if I add a new variant?          | Tests Open/Closed awareness           |
| What design pattern does this resemble?       | Connects implementation to vocabulary |

Start with problems **1, 2, and 3** — they are the closest to your cache interview. Once those feel comfortable, work through the rest in order.

Final questions that candidate should ask to interviewer:

"Is there anything you'd like me to clarify or elaborate on from our discussion today?"
"Are there any areas you'd suggest I explore further for this kind of role?"
"What qualities does your ideal candidate for this role typically have?"
