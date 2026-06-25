Great observation. The interviewer was evaluating **how well you can use AI as a tool** — which is a real skill in modern engineering teams. Writing a good prompt is like writing a good requirement — garbage in, garbage out.

---

## The Anatomy of a Great Technical Prompt

A strong prompt has **5 layers:**

```
1. Context       → What is the system/domain?
2. Problem       → What exactly needs to be built?
3. Constraints   → What rules must the solution follow?
4. Design Hints  → What patterns/principles should be applied?
5. Output Format → How should the response look?
```

---

## Bad Prompt vs Good Prompt — Side by Side

### ❌ Bad Prompt (What you probably used)

```
Implement a cache with get and put methods with eviction policy.
```

**Problems:**

- No language specified
- No capacity constraint mentioned
- No mention of pluggability
- No design expectations
- AI will guess everything and may produce mediocre code

---

### ✅ Good Prompt (What you should write)

```
Language: Java

Context:
I need an in-memory caching system for a backend application.

Problem:
Implement a generic cache with:
- get(K key) → returns value or null
- put(K key, V value) → stores value, evicts if at capacity

Constraints:
- Fixed capacity defined at instantiation
- Eviction policy must be pluggable at instantiation time
- Support at least LRU and LFU as built-in eviction policies
- Thread safety is NOT required for now

Design Requirements:
- Follow SOLID principles, especially SRP and OCP
- Use the Strategy design pattern for the eviction policy
- Eviction policy should be an interface, not hardcoded

Output Format:
- Show the EvictionPolicy interface first
- Then LRU and LFU implementations
- Then the Cache class
- Then a main() demo showing both policies in action
- Add comments explaining which SOLID principle each class satisfies
```

---

## The 5 Layers Applied to Every Problem

### Layer 1 — Context

Tell AI the _world_ this code lives in.

```
// Weak
"Build a payment system"

// Strong
"I'm building a checkout service for an e-commerce backend in Java.
The service processes orders and needs to support multiple payment methods."
```

### Layer 2 — Problem

Be precise about inputs, outputs, and behavior.

```
// Weak
"Support multiple payment methods"

// Strong
"Implement a PaymentProcessor with a single method:
process(Order order) → PaymentResult
Support CreditCard, UPI, and Wallet as payment types.
The payment method should be passed at runtime, not hardcoded."
```

### Layer 3 — Constraints

Tell AI what NOT to do, and what boundaries exist.

```
- No Spring Framework, plain Java only
- No external libraries
- Keep it under 150 lines
- No thread safety needed
- Use interfaces, not abstract classes
```

### Layer 4 — Design Hints

This is what separates a junior prompt from a senior prompt.

```
- Apply Strategy Pattern for the payment method
- Each payment class should have one responsibility only (SRP)
- The PaymentProcessor should depend on an interface, not a concrete class (DIP)
- Adding a new payment method should require zero changes to existing classes (OCP)
```

### Layer 5 — Output Format

Control how AI structures the response.

```
- Show class/interface hierarchy first as a diagram or list
- Write code in this order: interface → implementations → main class → demo
- Add a one-line comment above each class stating its single responsibility
- End with: which design pattern is used and which SOLID principles are satisfied
```

---

## A Reusable Prompt Template

Save this and fill it in for every problem:

```
Language: [Java / Python / Go]

Context:
[1-2 sentences about the system this belongs to]

Problem:
Implement [class/system name] with:
- [method 1] → [what it does]
- [method 2] → [what it does]

Constraints:
- [constraint 1]
- [constraint 2]
- [constraint 3]

Design Requirements:
- Follow SOLID principles, especially [SRP / OCP / DIP]
- Use [pattern name] design pattern for [which part]
- [specific structural requirement]

Output Format:
- Start with the interface(s)
- Then concrete implementations
- Then the main class
- Then a working demo in main()
- End with a short explanation of: pattern used + SOLID principles applied
```

---

## One More Important Thing

Even with a perfect prompt, **you must be able to answer these 3 questions about the output:**

| Question                                            | How to Prepare                            |
| --------------------------------------------------- | ----------------------------------------- |
| _"Walk me through this code"_                       | Read every line before the interview      |
| _"Which design pattern is this?"_                   | Ask AI to explain it in the prompt itself |
| _"Which SOLID principle does this follow/violate?"_ | Ask AI to annotate it in the prompt       |

**The interviewer is not just testing your prompting — they're testing if you understand what AI gave you.**

A great prompt gets you great code. But _reading and understanding that code_ is what gets you the job.
