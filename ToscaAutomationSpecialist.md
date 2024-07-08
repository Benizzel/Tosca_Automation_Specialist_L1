# Tosca Automation Specialist

# Intro
- Exam am Montag
- SuT: [demowebshop.tricentis.com](https://demowebshop.tricentis.com/)

## Webshop Flow
1. Browser öffen
1. Click Category
    * Click Subcategory
    * Click Product
4. Edit Attributes if needed (Quantity, Size)
5. Click "Add to cart"
6. Click "Shopping Cart"
7. Agree AGB
8. Checkout
    * Checkout as Guest
1. Checkout Process durchspielen
    * ...
1. Confirm Order
1. Order Confirmation
1. Close Browser / Log-out

---
## Registerkarten und Actions in Tosca

*Workspace*:

Neuer Workspace -> Type of Repo -> Art der Database auswählen oder halt Singel User Workspace. Bei Multi-User können Testcase ein-und ausgechecked werden

TAMI ist normalerweise ein eigener Workspace, sprich eine eigene DB

*Modules*

Ein Modul ist eine Sammlung von Wiederverwendbaren Testschritten, die die Aktionen und Prüfungen darstellen, die auf einer bestimmten Anwendung durchgeführt werden sollen. Module werden in der Regel durch das Scannen der Anwendung erstellt und enthalten die technischen Informationen, die erforderlich sind, um mit der Anwendung zu interagieren.

*TestCases*

Ein Testfall (TestCase) besteht aus einer Sequenz von Testschritten, die auf Grundlage der Module erstellt werden. Testfälle werden genutzt, um konkrete Testszenarien zu definieren und auszuführen, indem sie verschiedene Module miteinander kombinieren und spezifische Werte und Bedingungen für die Tests festlegen.

*TestCaseDesign*

Variationen von Testcases. Zum Beispiel ein Testcase aber mit 5 Designs (z.B. für Äquivalenzklassen, EdgeCases)

*Configurations*
Zum Beispiel Konfigurationen für unterschiedliche Environments (DEV, EDU, ...)

*TestPlanning*

Testcases und deren Ausführung planen und zuteilen

*ScratchBook*

"Debug Mode" Ich bin im blauen Teil "TestCases" am Testcases entwickeln. Kann Teile davon ausführen. Mit ScratchBook sehe ich die Resultate instantly (ohne dass ich Executen muss)

*Import + Export Subset*

Testfälle von Workspace x exportieren und in Workspace y importieren. Weil alles zusammenhängt (Testcase-Module-....) kriege ich ziemlich viel raus

*Grauer Folder = Component Folder*

Für Repo bzw "Workspace organisation

==**Glossar**== Workspace + Projekt -> SameSame but different

*Hide DoNothing*

Die leeren TestSteps verschwinden. ACHTUNG! Ich sehe nicht, dass sie gehidet sind

*Other*

Mit Drag and Drop kann ich Register nach meinem Gusto anordnen

Fokus auf Element: Doppelclick -> Properties werden entsprechend angezeigt.

> API Testing: Auch möglich, lernen wir aber nicht

# First Steps
Viele Testtool: Nur Web 

USP Tosca: Alles mögliche

Tosca bzw. die Module sind eine Abstraktion

System - Module - 0..n Testcases

*Engines zum scannen*

HTML
UIA - Accessability Framework von Microsoft
WinX

für Avaloq wäre es .NET Engine

Beim Scannen - mit rechter Maustaste die verschachtelten Elemente aus dem HTML anzeigen

Skalierung auf 100% einstellen - von Browser und von Bildschirm!

# Scanning
The selcted item is not unique -> Identify by 
Tosca sagen, wie es das item erkennt

Identify by Properties: WICHTIG: Properties, die ich dafür auswähle müssen gleich bleiben!

![Identify by](image.png)

Controls können umbenannt werden

Best Practice: Ein Modul pro Section einer Webseite erstellen. Nicht die ganze Webseite als ein Modul

Identify by Anchor: Stabiler Anker (eindeutig identifizierbar) definieren und dann das Control finden, dass sich relativ vom Anchor befindet

Show content preview: Z.B. bei Tables sehr nützlich, weil es eine Vorschau zeigt

Für ein  Modul scanne ich die page und wähle die Controls, welche ich später in den Testcases nutzen möchte

ControlGroup: Ich kann zum Beispiel einzelne Registerkarten zusammenfassen in eine ControlGroup. Vor allem cool für readability

Ich kann bei den Name zur Identifizierung etc. auch Wildcards benutzen

> Bei Identify by Anchor: Wichtig ist als Anker ein Element zu wählen, das unique ist!

> Vorgehen: Element auswählen, kurz warten ob unique. Wenn nicht, mit Props und Anchor etc herumspielen, bis es unique ist zum identifyen

----

<mark>!!!!!!!!!!!!!!!INSERT HERE: Folie Best Practices</mark>

----

Wichtig davon: Nicht die Struktur von Tosca verwenden sonder bessser mit Component Folder (pro Projekct) und dort drin wiederum Modules, TestCases etc.

Module: Drei Folder: Completed, Ready for approval, in Work. Damit ich weiss, mit welchen ich arbeiten kann

# TestCase and TestSteps

## Struktur eines Testcases
1. Precondition
1. Process
1. Postcondition

Controls aus den Modulen kann ich mit Drag and Drop in den Testcase ziehent
Ctrl + T -> Fuzzy Search nach Modulname

==**Glossar**== TCP -> Testcase Configuration Parameter

Standardmodule: Von Tricentis vordefinierte Module, die etwas spezifisches machen, welche unabhängig sind vom SuT

Module: Feingranulare Sammlung von Controlls, welche ich ansteuern kann. Im Teststep nehme ich dann das Modul und steuere das an, was ich will

--> Siehe Aufgabe 3

## TestStepValues
Bei Values: "X" bedeutet, dass Tosca versucht technisch zu klicken. Während "Click" "den Mauszeiger bewegt" --> Besser: X, weil dann unabhängig von Browser und Screen Resolution und so

ControlGroup - Bei den Values cool, weil dann habe ich die Group und kann als DropDown den Value wählen
![alt text](image-1.png)

## Random Values, MATH, DATE
- {RND[5]}
- {RANDOMTEXT[10]} --> Irgendwelche Zeichen, inkl. Zahlen
- {RANDOMREGEX["[A-Z]{10}"]} --> 10 Zeichen mit nur A-Z
- {RANDOMREGEX["[A-Z][a-z]{10}"]}--> 10 Zeichen mit nur A-Z und a-z

- MATH gibt es auch, wo ich etwas berechnen kann

Format `{DATE[<Basedate>][<Offset>][<Format>]}`

- {DATE[][+4M][MM]} --> Today (weil erste Klammer leer) Plus 4 Monate im Format MM
- {DATE[][+3y][yyyy]} --> Today + 3 Jahre in Format yyyy
- {DATE[1.5.2024][+3y][yyyy]}


Wenn ich mit { bei Value beginne, bekomme ich eine Auswahl der Methoden

![alt text](image-2.png)

## Recap

- Buffer - zwischenspeicher (Variable)
- Insert - nonGui
- Input - default
- verify - boolean
- wainOn - auf Element warten
...

## Buffer

Syntax, um den Value aus dem Buffer in Value abzufüllen: `{B[<Buffername]}`
--> Translation (rechtsklick) ist auch möglich

Buffer == Variable

Tool -> Buffer Viewer --> Hier sehe ich die Buffers
Buffer werden überschrieben, wenn ich einen neuen Value zuordne

Buffer werden in einem json File gespeichert (das heisst TBox Buffer oder so)

Es gibt ein Modul "TBox Delete Buffer"

Bei reinen div Tags, die Controls sind (z.B. wenn ein Preis angezeigt wird): Ich muss bei Value das Property definieren, von welchem der Wert genommen werden soll. Zum Beispiel OuterText oder InnerText. Tosca macht daraus dann .OuterText was soviel bedeutet wie Price.OuterText - also vom Control Price das Property OuterText

![alt text](image-3.png) 
![alt text](image-4.png)

## Verify mit Table


![alt text](image-5.png)

![alt text](image-6.png)


Meine Lieblingsvariante, um Sub-Total etc. zu prüfen -> Ich gehe von Row zu Row

![alt text](image-8.png)

Ich könnte aber auch Column selektieren und dann prüfen

![alt text](image-7.png)


Weil "Message Order successful" ein Div Tag ist, welches einfach einen Text anzeigt, check ich mit dem Property "Visible", ob das Element vorhanden ist:

![alt text](image-9.png)

---

# Libraries

Ich kann Workflows in Libraries auslagern und sie dann in 0..n Testcases nutzen. Warten muss ich es dann nur in der Library anstatt in x Testcases

- Rechtsklick "Create TestCase Library"
- "Reusable TestStepBlock
- Ich kann aus einem TestCase einen Folder (z.B. Precondition) per Drag and Drop in einen Library Ordner ziehen und Zack, habe ich eine Library
- Um Reusable TestStepBlock in Tescase zu nutzen -> Drag and drop

# Rescan - Merge - ValueRange

## Rescan
1. Modul auswählen
2. Bei SuT auf richtigen Screen gehen
3. Auf Modul Rechtsklick und "Rescan"
4. Business as usual :-)

## Merge

- Zielmodul bleibt
- Source Modul verschwindet

![alt text](image-10.png)

## Value Range
Auf Modul bei einem Control
![alt text](image-11.png)

## Wait
Action Mode "WaitOn" -> Tosca wartet, bis Element da ist. WaitOn hat ein Timeout in den Tosca Settings definiert. Den Timeout kann ich aber auch in den Testcase Settings (dort, wo ich den Browser definiere) übersteuern.

## TCP - Test Configuration Parameter
Define on Testcase

![alt text](image-12.png)

mit `{CP[<TCP>]}` kann ich auf ihn referenzieren

![alt text](image-13.png)

![alt text](image-14.png)

## Business Parameters

Define in the Library. Value ist leer, weil ich definiere dann beim Testcase die Parameter, mit welchen ich den Testcase ausführen möchte.
![alt text](image-15.png)

Im TestCase selber sehe ich die Schritte nicht mehr. Aber ich kann die Parameter für die Ausführung definieren
![alt text](image-16.png)

## XBuffer
Damit kann ich Zeugs aus Elementen buffern, die dynamisch sind. Z B bei "Order Number: 123456" ist die 123456 immer unterschiedlich, je nach Order. 

Spannend beim zuweisen: ActionMode = Verify!! Und dann das Property (in diesem Fall .InnerText) einem Buffert zuweisen (`.InnerText==Order number: {XB[OrderNumber]}`) <- OrderNumber ist hier meine Erfindung für den Namen vom Buffer. "Order number:" Ist der Teil vom HTML String, der nicht dynamisch ist.

XBuffer definiert den dynamischen Teil eines Strings und speichert diesen dynamischen Teil auch gleich noch in einem Buffer (in meinem Fall im "OrderNumber")

![alt text](image-18.png)

![alt text](image-19.png)

## Parent ID, Dynamic ID, Dynamic Comparison
Um auf der Order Übersicht meinen letzten Order auszuwählen:
- Orderübersicht gescannt. Irgend ein Div mit einem Order genommen und dann aber die Properties dynamisch gemacht:
- Beim DIV vom Order: OuterText --> Hier ändern auf "Order Number: " und danach den XBuffer. So sucht Tosca dann den Order mit der Order Number, die ich gebuffert habe. Also den letzten
![alt text](image-21.png)

- Beim OrderTotal InnerText. <mark>ACHTUNG: Auch wenn InnerText leer ausschaut: auf die drei Punkte klicken, meist steht irgendwas drin</mark> - Dynamisch machen, indem Order Total:* -> also Wildcard, eingegeben wird
![alt text](image-20.png)



