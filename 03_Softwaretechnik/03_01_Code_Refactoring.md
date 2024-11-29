
不同的 Code_Refactoring 的方法

# 1 Klasse extrahieren


Eine Klasse macht die Arbeit, die von zwei Klassen zu erledigen wäre.
Smells: Große Klasse, Datenklumpen, duplizierter Code
Zusammenfassung: Erstellen Sie eine neue Klasse, und verschieben Sie die relevanten Felder und Methoden von der alten Klasse in die neue

![](image/Pasted%20image%2020241129235512.png)

# 2 Methode extrahieren


Ein Fragment im Code kann zusammengefasst werden.

Smells: Lange Methode, duplizierter Code, Kommentare

Zusammenfassung: Machen Sie aus dem Fragment eine Methode, deren Name die Aufgabe der Methode erklärt.


![](image/Pasted%20image%2020241129235619.png)


# 3 Geschachtelte Bedingungen durch Wächterbedingungen ersetzen

Wächter: 守卫者 看守人

Eine Methode weist ein bedingtes Verhalten auf, das den normalen Ablauf nicht leicht erkennen lässt.

Smells: Lange Methode

Zusammenfassung: Verwenden Sie Wächterbedingungen für die Spezialfälle

![](image/Pasted%20image%2020241129235707.png)


# 4 Parameter durch explizite Methode ersetzen

Eine Methode führt abhängig von einem ihrer Parameter unterschiedlichen Code aus.

Smells: Lange Parameterliste, Switch-Befehl

Zusammenfassung: Erstellen Sie eine separate Methode für jeden Wert des Parameters



# 5 Parameterobjekt einführen

Eine Gruppe von Parametern gehört auf natürliche Weise zusammen.
Smells: Lange Parameterliste, Neigung zu elementaren Typen, Datenklumpen
Zusammenfassung: Ersetzen Sie sie durch ein Objekt

![](image/Pasted%20image%2020241130000058.png)



# 6 Methode verschieben

Eine Methode nutzt mehr Elemente einer anderen Klasse oder wird von mehr Elementen einer Klasse benutzt als von denen, in der sie definiert ist.

Smells: Datenklassen, unangebrachte Intimität  不恰当的亲密感 , Neid 嫉妒

Zusammenfassung: Ersetzen Sie sie durch eine neue Methode in der Klasse, die sie am meisten verwendet

