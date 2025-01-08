
# 1 Motivation

Wir kennen Contracts zur formalen Spezifikation von Methoden
➢Können als Ausgangsbasis für die Implementierung dienen

Wie kann man nachweisen, dass die Implementierung den Contract erfüllt?

Antwort 1: Testen der Implementierung gegen den Contract
➢ Viel Testen hilft, ist aber kein Beweis!
Antwort 2: Beweisen, dass das Programm den Contract erfüllt
➢ Voraussetzung für Beweise: Beweiskalkül (hier: Hoare Kalkül)


# 2 While-Sprache

Moderne Sprachen haben (viele) komplexe Features
➢ Umfang zu groß bzw. Konstrukte zu schwierig für Demonstration einfacher Ideen

While-Sprache als formales Berechnungsmodell
• Übersichtlicher Sprachumfang
• Einfache Semantik

➢ Wir verwenden die WHILE-Sprache zur Demonstration. Hoare- Regeln lassen sich aber für beliebige Sprach-Konstrukte erstellen
➢ Viele Konstrukte gängiger Sprachen (z.B. Java) können in die While- Sprache umgeformt werden (turingmächtig)

WHILE Syntax
![](image/Pasted%20image%2020241215162558.png)


![](image/Pasted%20image%2020250108102958.png)
-| 符号 代表 negation B =  nicht B


# 3 partielle Korrektheit und totale Korrektheit

Idee des Hoare-Kalküls: Die Verifikation eines Programms besteht aus zwei Schritten.
• Beweis der partiellen Korrektheit: 通过  partiellen Korrektheit 证明  , das programm beim Alle möglichen Eingaben korrekt functionieren kann 
• Beweis der Terminierung

Am Beispiel Fakultäts-Funktion:
Gilt x=n vor Ausführung, dann gilt y=n! nach Ausführung, sofern die Ausführung terminiert
⟹ partielle Korrektheit

Gilt x=n vor Ausführung, dann terminiert das Programm und y=n!
⟹ totale Korrektheit


## 3.1 partielle Korrektheit und totale Korrektheit
In program verification, partial correctness and total correctness are key concepts that describe different aspects of program behavior. Here's the distinction using the provided example

> Partial correctness focuses on correctness of the result, assuming the program finishes.
> Total correctness guarantees both correctness of the result and termination.

---

Partial Correctness

**Statement**:  
"If x=n holds before execution, then y=n! holds after execution, provided the execution terminates."
- **Meaning**: Partial correctness ensures that if the program terminates, it produces the correct result (y=n!).
- **Focus**: This only guarantees correctness **under the assumption of termination**. It does not concern itself with whether the program actually finishes execution.
- **Verification**: Partial correctness is proven using **Hoare Triples** like `{P} C {Q}`, where termination is assumed but not proven.

---
Total Correctness

**Statement**:  
"If x=n holds before execution, then the program will terminate and y=n!"

- **Meaning**: Total correctness ensures both:
    1. The program terminates.
    2. The result is correct (y=n!).
- **Focus**: Total correctness combines **termination** and **correctness** of the result.
- **Verification**: To prove total correctness, one must:
    1. Prove **partial correctness** (correct output assuming termination).
    2. Prove that the program always terminates, often using mathematical induction or a **termination measure** that decreases with every step.

---
Example in Context

Suppose you have a program that calculates the factorial n!
```
y = 1
while x > 1:
    y = y * x
    x = x - 1

```

- **Partial Correctness**:
    - If x=n initially, then after the program terminates, y=n!
    - Prove by verifying the loop invariant and correctness of the final output.
- **Total Correctness**:
    - Additionally prove that the `while` loop always terminates (e.g., because xxx decreases on each iteration and eventually x≤1, breaking the loop).

## 3.2 Partielle Korrektheit

Ein Programm ist partiell korrekt bzgl. einer Vorbedingung P und einer Nachbedingung Q, falls immer dann, wenn der initiale Zustand die Vorbedingung erfüllt und, wenn das Programm terminiert, der Endzustand die Nachbedingung erfüllt.

Annahme: Programm terminiert nach endlich vielen Schritten
![](image/Pasted%20image%2020241215163130.png)

Vorbedingung: Nur wenn diese erfüllt ist kann die Nachbedingung garantiert werden (durch Beweis)
Nachbedingung: Gefordertes Ergebnis (Spezifikation, z.B. Post- Condition eines Contracts)
➢Vorbedingungen ergeben sich oft aus dem Beweis



## 3.3 Bedingungen

Zentrales Element eines Hoare-Beweises sind Bedingungen bzw. Zusicherungen (assertions)
➢ Formeln der Prädikatenlogik
➢ Werden in geschwungenen Klammern hinzugefügt

![](image/Pasted%20image%2020241215163153.png)






# 4 Hoare Calculus, Hoare Kalkül

The **Hoare Calculus**, named after Tony Hoare, is a formal system used for **program verification**. It provides a mathematical framework to prove that a program behaves correctly, meaning it satisfies specified properties. The core concept of the Hoare Calculus is based on **Hoare Triples**, which describe the conditions under which a program is correct.

## 4.1 **Foundation: The Hoare Triple**

A Hoare Triple has the following form:  
**{P} C {Q}**
- **P**: The **precondition**, which specifies the state of the program before the execution of the command **C**.
- **C**: The command or sequence of instructions being analyzed.
- **Q**: The **postcondition**, which describes the state of the program after executing **C** if it starts in a state where **P** is true.

The triple asserts that if the precondition **P** is true before the command **C** is executed, then the postcondition **Q** will be true afterward, provided the program terminates.

## 4.2 **Rules of the Hoare Calculus**

The Hoare Calculus uses a set of inference rules to reason about program correctness. Some key rules include:

1. **Assignment Rule**:
    - If assigning a value to a variable ensures the postcondition, the precondition can be derived:
        - `{Q[x := E]} x := E {Q}`
        - Here, `Q[x := E]` means substituting the variable `x` with the expression `E` in `Q`.
2. **Sequence Rule**:
    - If the first command ensures a state where the second command's precondition holds:
        - `{P} C1 {Q} and {Q} C2 {R} ⇒ {P} C1; C2 {R}`
3. **Conditional (If) Rule**:
    - For a conditional statement:
        - `{P ∧ B} C1 {Q} and {P ∧ ¬B} C2 {Q} ⇒ {P} if B then C1 else C2 {Q}`
        - The branches `C1` and `C2` are verified separately for the corresponding conditions.
4. **While Loop Rule**:
    - Loops are verified using an **invariant** `I`:
        - `{I ∧ B} C {I} ⇒ {I} while B do C {I ∧ ¬B}`
        - The invariant `I` must hold before and after each iteration of the loop, and it must imply the desired postcondition when the loop exits.

# 5 Nachweis partieller Korrektheit
## 5.1 Hoare Kalkül: Axiomen und Inferenzregeln

Hoare Kalkül besteht aus Axiomen 定理 und Inferenzregeln 推导公式 für alle Konstrukte einer Programmiersprache
➢ definiert was ein Konstrukt bewirkt (wie wird es ausgeführt)
➢ gibt der Syntax eine Semantik

Axiome sind Grundsätze eines Systems, ohne weitere Begründung Inferenzregeln ermöglichen das Zerlegen komplexerer Ausdrücke
• Stellen eine logische Schlussfolgerung dar

Formale Beschreibung der Konstrukte ermöglicht es, das Programm für alle Eingaben „durchzurechnen“

### 5.1.1 Axiome

Skip-Axiom
Skip ändert den Zustand nicht und bewahrt dadurch jede Vorbedingung

![](image/Pasted%20image%2020241215164251.png)

Ersetzungs-Axiom (Zuweisung)
Ersetze jede Vorkommen von x in der Nachbedingung P durch syntaktischen Ausdruck E
➢Wird von unten nach oben angewandt

![](image/Pasted%20image%2020241215164309.png)

### 5.1.2 Inferenzregeln

Jedes Kalkül gibt eine Menge von Inferenzregeln vor
- Eine Inferenzregel beschreibt, unter welchen Annahmen eine bestimmte Schlussfolgerung abgeleitet werden kann
    - ![](image/Pasted%20image%2020241215164429.png)
- Beispiel aus dem Kalkül des natürlichen Schließens (Modus Ponens):
    - ![](image/Pasted%20image%2020241215164443.png)
    - „Wenn A und A impliziert B gilt, dann gilt B“
    - 如果分子成立, 则 分母也成立 



## 5.2 Hoare Kalkül: Regeln


根据 inferenzregel, 如果 分子上面的条件成立, 则分母上的条件也会成立 

![](image/Pasted%20image%2020250108103713.png)



### 5.2.1 Sequenzregel

Hoare-Tripel können sequentiell komponiert werden, wenn die Nachbedingung der ersten Anweisung mit der Vorbedingung der zweiten Anweisung kompatibel ist

![](image/Pasted%20image%2020241215164557.png)

### 5.2.2 Rule of Consequence

• die Vorbedingung darf verschärft werden
• die Nachbedingung darf abgeschwächt werden  减弱，减轻 减薄 稀释


![](image/Pasted%20image%2020241215164715.png)

![](image/Pasted%20image%2020241215164721.png)

### 5.2.3 If-Regel

Für die if-Anweisung müssen beide möglichen Fälle entsprechend berücksichtigt werden

![](image/Pasted%20image%2020241215164810.png)

### 5.2.4 While-Regel

- Beweise für Schleifen basieren auf Invarianten I
- Die Invariante muss vom Schleifenrumpf S bewahrt werden
- Wenn vor der Schleife I gilt, gilt I auch nach der Schleife, zusätzlich gilt die Schleifenbedingung nicht

➢ keine Vorgabe zur Ermittlung der Schleifeninvariante: muss manuell ermittelt werden

![](image/Pasted%20image%2020241215165235.png)

## 5.3 Fahrplan zur Anwendung des Hoare-Kalküls

Muss gelten: 
- Aus Vorbedingung folgt Nachbedingung (RoC / Äquivalenz)

Beweisführung meist rückwärts
➢ vom spezifizierten Ergebnis (post) die (möglichst schwächsten) Vorbedingungen ableiten

Vorgehensweise: Vom aktuellen Punkt aus gesehen nach oben arbeiten. Zwei

Möglichkeiten:
• Darüber steht ein Programmausdruck
    ➢ Regel anwenden
• Darüber steht eine Bedingung
    ➢ Äquivalenz/RoC prüfen/ableiten
    ➢ Beweis schließen


![](image/Pasted%20image%2020241215165925.png)


# 6 Totale Korrektheit


Ein Programm S ist total korrekt bzgl. Vorbedingung P und Nachbedingung Q, wenn es partiell korrekt ist und immer terminiert
![](image/Pasted%20image%2020241215170848.png)

Finde für jede Schleife eine Terminierungsfunktion 𝑡 … ↦ ℕ, so dass
![](image/Pasted%20image%2020241215170903.png)


Wenn eine solche Terminierungsfunktion (auch: Schleifenvariante) für jede Schleife gefunden werden kann, dann ist die totale Korrektheit bewiesen


## 6.1 Proving Total Correctness

To prove total correctness, two aspects must be addressed:

1. **Partial Correctness**:
    - Show that if the program terminates, it produces the correct output. This is typically done by verifying a **loop invariant** and demonstrating that the final state satisfies the postcondition QQQ.
2. **Termination**:
    - Prove that the program always terminates. This involves defining a **termination metric** or measure, which:
        - Is a non-negative integer.
        - Decreases with each iteration of a loop or step of the program.
        - Eventually reaches zero, causing the program to stop.


## 6.2 Example: Factorial Calculation

Consider a program that computes the factorial of a number nn:

```
y = 1
while x > 1:
    y = y * x
    x = x - 1

```

**pecification:**
- Precondition (PPP): x=nx = nx=n, where n≥0n \geq 0n≥0.
- Postcondition (QQQ): y=n!y = n!y=n!.

**Steps to Prove Total Correctness:**
1. **Partial Correctness**:
    - **Invariant**: y⋅x!=n!y \cdot x! = n!y⋅x!=n! (remains true throughout execution).
    - Before the loop, y=1y = 1y=1 and x!=n!x! = n!x!=n!.
    - At each step, yyy accumulates the product, and xxx decrements until x=1x = 1x=1, ensuring y=n!y = n!y=n! when the loop exits.
2. **Termination**:
    - Define a **termination metric**: xxx, which starts at nnn and decreases by 1 on each iteration.
    - The loop condition (x>1x > 1x>1) ensures xxx will eventually reach 1, causing the loop to terminate.