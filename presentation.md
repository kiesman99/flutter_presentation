---
marp: true
theme: uncover
class: invert
---

# Flutter 💙
Ein Crash-Course

___

# Agenda
- Eigenheiten von Dart
- Einleitung in die Konzepte von Flutter
- Live-Programmierung einer Counter-App
- Live Programmierung einer kleinen Animation
- State-Management
- Kurzer Einblick in Bloc (Redux)
- Ressourcen für weitere Bildung

___

# Dart, eine komisch-schöne Sprache

___

## Ursprung

- Sollte mal Javascript ersetzen.
    - Daher stellenweise limitiert/orientiert an JavaScript 
- Geht seit 2.0 neue Wege
    - Kann beispielsweise zu bytecode compiliert werden
- Borgt sich Elemente aus anderen Sprachen
    - noch aktiv in Entwicklung (Nichts schlechtes)
___

### Konstruktoren

___

### Normaler Konstruktor

```java
class Hund {
    String name;
    int alter;

    Klasse(final String name, final int alter) {
        this.name = name;
        this.alter = alter;
    }
}
```

```dart
class Hund {
    String name;
    int alter;

    Hund(this.name, this.alter);
}
```

___

### Named Parameter

```dart
class Hund {
    String name;
    int alter;

    Hund({this.name, this.alter});
}

void main() {
    // das 'new' Keyword ist überflüssig
    // die Reihenfolge von Parametern in named
    // Parametern ist egal
    // Paramter hier sind auch OPTIONAL
    Hund hund = Hund(alter: 54, name: "Fredo")
}
```

___

### Optional Parameter

```dart
class Hund {
    String name;
    int age;

    Hund(this.name, [this.age]);
}

void main() {
    var dog1 = Hund("Fredo", 31);
    var dog2 = Hund("Bello");
}
```

Man kann nur **entweder** Optionale Parameter ([]), oder named Parameter
({}) haben.
___

### Überladungen sind NICHT möglich

Ungültig:

```dart
class Hund {
    void bark(String b) { ... }
    void bark(int b) { ... }
}
```

___ 

#### Lösung für Konstruktoren
##### Named-Constructors

```dart
class Hund {
    String name;
    int age;
    Hund(this.name, this.age);
    Hund.unborn(this.name) : this.age = 0;
    // schnelle Schreibweise für
    // Hund.unborn(this.name) {
    //   this.age = 0;    
    // }
}
```

___

## Private Variablen

Es gibt kein **Keyword private**, stattdessen wir ein **_** vor den Namen der Variable geschrieben:
`String _iamPrivate;`

___ 

### Extension Methods

In Dart kann man Funktionalität zu bereits bestehenden Klassen hinzufügen.
Dies ist toll, wenn man eine Klasse auf die man keinen Einfluss hat erweitern möchte.

___ 

#### Beispiel

```dart
 if ("blubber".isInteger) { ... }
```

Dies auf einem String fragen zu können wäre vielleicht hilfreich.
Wir könne uns eine Extension basteln:

```dart
extension MyStringExtension on String {
    bool isInteger() {
        var num = int.tryParse(this);
        return num != null;
    }
}
```
___ 

### Null-Safety

Dart bekommt derzeit **Null-Safety**.
Dadurch ist folgender Code möglich:

```dart
VoidCallback callback;

callback?.call();
```

Der *callback* wird nur ausgeführt, wenn er nicht `null`ist.
___

# Everything is a Widget!
- Stateless
- Stateful
___

## Definition eines Widgets

Widgets (das UI) wird **im Code** definiert. 
Jedes Widget is eine **eigene Klasse**.

___

```dart
@override
Widget build(BuildContext context) {
    // ...Definition des Widgets
}
```
___

## Grundlegende Widgets

```dart
// Ein einfacher Text
Text(String content); 
// Container, welcher ein anderes Widget als Unterelement nehmen kann 
// Container sind vergleichbar mit dem `div-Tag` aus HTML
// Container können verschiedene Style-Attribute nehmen
Container(Widget child, ...);
// Row nimmt mehrere Elemente und arrangiert diese horizontal
Row(List<Widget> children, ...);
// Column tut dasselbe, wie Row Vertikal
Column(List<Widget> children, ...);
```

___

## Zeit für Code

[Code-Pen](https://codepen.io/kiesman99/pen/jOqPgPZ)

___

## Verschachtelung ist Stichwort

___

```dart
Container(
    // Wir geben dem Container die Hintergrundfarbe rot
    decoration: BoxDecoration(
        color: Colors.red
    ),
    // Breite auf 100% setzen
    width: double.infinity,
    child: Column(
        // besondere Style-Angaben für Positionierung
        mainAxisAlignment: MainAxisAlignment.center,
        crossAxisAlignment: CrossAxisAlignment.center,
        children: [
            Text("Ich bin über dir!", 
            style: TextStyle(color: Colors.white)),
            // Dieser Text hat kein speziellen Style
            Text("Über wem?")
        ]
    ),
);
```

___

## Stateful vs. Stateless

| Stateful | Stateless |
| --- | --- |
| Haben State, der geupdatet werden kann | *Dumme*-Komponente, die keinen State haben, der geupdatet werden kann. Beispiel: Text()

___ 

# Live-Code!

___ 

Bei mehr Interesse:

- [Online Conference 12.08 - onAir](https://www.flutteronair.com/)
- [Online Conference 12.08 - Byteconf](https://www.papercall.io/byteconf-flutter-2020)
- [Docs Linksammlung](https://docs.google.com/document/d/1ArrV3yNjUG8YFN0DXtmbl4Z6kq-pmRYonu-pnVTdHeA/edit?usp=sharing)
___

# Danke euch 😊


