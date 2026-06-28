# ⚔️ OverLoad: A Turn-Based Card Game Demo

> A console-based 1v1 turn-based card game implemented in C++20, designed to demonstrate core Object-Oriented Programming (OOP) principles in a practical game-logic scenario.

## 📌 Overview

This project simulates a simplified battle between a player and an AI opponent. It features:

- **Card System**: Attack, Defense, and Utility cards with different costs and effects.
- **Resource Management**: Health (HP), Armor, and Energy per turn.
- **AI Opponent**: A basic scripted opponent that plays random cards each turn.

The primary goal is to showcase how **Encapsulation**, **Inheritance**, and **Polymorphism** work together to create extensible, maintainable game code.

## 🧬 Architecture (OOP in Action)

### Class Hierarchy (Inheritance)
```cpp
// Abstract base class (pure virtual)
class Card {
protected:
    std::string m_name;
    int m_cost;
public:
    virtual void Execute(Player& target) = 0; // pure virtual
    virtual ~Card() = default;
};

// Concrete derived class
class AttackCard : public Card {
public:
    void Execute(Player& target) override {
        target.TakeDamage(10);
    }
};
```

Polymorphic Container

All cards are stored in a std::vector<Card*>. During the game loop, calling card->Execute(target) will dynamically dispatch to the correct overridden function based on the actual object type—thanks to the vtable (virtual table).

Encapsulation

Player's m_health and m_energy are private. Modifications are only allowed through public member functions like TakeDamage(), Heal(), and SpendEnergy(). This prevents invalid states (e.g., negative health) caused by accidental external assignments.

🚀 Getting Started (Visual Studio 2022)

Prerequisites

· Visual Studio 2022 (with "Desktop development with C++" workload)
· Windows 10/11 (or Linux with g++ and CMake, if you adapt)

Build & Run

1. Clone the repository:
   ```bash
   git clone git@github.com:yourusername/CardGame-Slg.git
   ```
2. Open the .sln solution file in Visual Studio.
3. Press Ctrl + F5 to run without debugging, or F5 to debug.

🔍 Debugging Tips (Visual Studio)

To see polymorphism in action at the memory level:

1. Set a breakpoint (F9) on the line where card->Execute(...) is called inside the game loop.
2. Press F5 to start debugging.
3. Open the Watch window and add the variable card (a base-class pointer).
4. Expand it – you will see a hidden member called _vfptr (the virtual function table pointer). Expand that to see the actual function address. For an AttackCard, it points to AttackCard::Execute; for a DefenseCard, it points to a different function – this is the runtime magic of polymorphism!

📂 Project Structure

```
CardGame-Slg/
├── src/
│   ├── Core/
│   │   ├── Card.h/cpp          # Abstract Card class
│   │   ├── Player.h/cpp        # Player state (HP, energy, hand)
│   │   └── GameManager.h/cpp   # Turn flow, win/loss conditions
│   ├── Cards/
│   │   ├── AttackCard.h        # Concrete attack card
│   │   ├── DefenseCard.h       # Concrete defense card
│   │   └── UtilityCard.h       # Utility card (draw, heal, etc.)
│   └── main.cpp                # Entry point and game loop
└── README.md
```

📜 License

This project is licensed under the MIT License – feel free to use, modify, and distribute it with proper attribution.

🙏 Acknowledgements

Inspired by the classic deck-building roguelike genre. Built as a practical exercise for mastering C++ OOP (based on C++ Primer).

```

---
