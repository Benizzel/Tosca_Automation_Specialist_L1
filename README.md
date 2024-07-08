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

Ctrl + B öffnet das Scratch Book. Mit Drag and Drop von Testcases oder Steps kann ich Sachen reinziehen, die dann ausgeführt werden.

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

![Identify by](/assets/image.png)

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
![alt text](/assets/image-1.png)

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

![alt text](/assets/image-2.png)

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

![alt text](/assets/image-3.png) 
![alt text](/assets/image-4.png)

## Verify mit Table


![alt text](/assets/image-5.png)

![alt text](/assets/image-6.png)


Meine Lieblingsvariante, um Sub-Total etc. zu prüfen -> Ich gehe von Row zu Row

![alt text](/assets/image-8.png)

Ich könnte aber auch Column selektieren und dann prüfen

![alt text](/assets/image-7.png)


Weil "Message Order successful" ein Div Tag ist, welches einfach einen Text anzeigt, check ich mit dem Property "Visible", ob das Element vorhanden ist:

![alt text](/assets/image-9.png)

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

![alt text](/assets/image-10.png)

## Value Range
Auf Modul bei einem Control
![alt text](/assets/image-11.png)

## Wait
Action Mode "WaitOn" -> Tosca wartet, bis Element da ist. WaitOn hat ein Timeout in den Tosca Settings definiert. Den Timeout kann ich aber auch in den Testcase Settings (dort, wo ich den Browser definiere) übersteuern.

## TCP - Test Configuration Parameter
Define on Testcase

![alt text](/assets/image-12.png)

mit `{CP[<TCP>]}` kann ich auf ihn referenzieren

![alt text](/assets/image-13.png)

![alt text](/assets/image-14.png)

## Business Parameters

Define in the Library. Value ist leer, weil ich definiere dann beim Testcase die Parameter, mit welchen ich den Testcase ausführen möchte.
![alt text](/assets/image-15.png)

Im TestCase selber sehe ich die Schritte nicht mehr. Aber ich kann die Parameter für die Ausführung definieren
![alt text](/assets/image-16.png)

## XBuffer
Damit kann ich Zeugs aus Elementen buffern, die dynamisch sind. Z B bei "Order Number: 123456" ist die 123456 immer unterschiedlich, je nach Order. 

Spannend beim zuweisen: ActionMode = Verify!! Und dann das Property (in diesem Fall .InnerText) einem Buffert zuweisen (`.InnerText==Order number: {XB[OrderNumber]}`) <- OrderNumber ist hier meine Erfindung für den Namen vom Buffer. "Order number:" Ist der Teil vom HTML String, der nicht dynamisch ist.

XBuffer definiert den dynamischen Teil eines Strings und speichert diesen dynamischen Teil auch gleich noch in einem Buffer (in meinem Fall im "OrderNumber")

![alt text](/assets/image-18.png)

![alt text](/assets/image-19.png)

## Parent ID, Dynamic ID, Dynamic Comparison
Um auf der Order Übersicht meinen letzten Order auszuwählen:
- Orderübersicht gescannt. Irgend ein Div mit einem Order genommen und dann aber die Properties dynamisch gemacht:
- Beim DIV vom Order: OuterText --> Hier ändern auf "Order Number: " und danach den XBuffer. So sucht Tosca dann den Order mit der Order Number, die ich gebuffert habe. Also den letzten
![alt text](/assets/image-21.png)

- Beim OrderTotal InnerText. <mark>ACHTUNG: Auch wenn InnerText leer ausschaut: auf die drei Punkte klicken, meist steht irgendwas drin</mark> - Dynamisch machen, indem Order Total:* -> also Wildcard, eingegeben wird
![alt text](/assets/image-20.png)

## ExplicitName + Index

> When elements do not have a unique identifier. ExplicitName allows Tosca to steer using the index, and take into account any dynamic changes.

> By default, XTestStepValue names cannot be changed. If the value of this property is true, you can edit the name of the referenced XTestStepValue. Instead of using True, you can also specify several values, separated from each other by semicolons. These values can be selected in the corresponding XTestStepValue.

Muss ich auf dem Control manuell hinzufügen. Tosca unterstützt mich nicht mit DropDown o.ä., obwohl Configs vordefiniert: https://documentation.tricentis.com/tosca/2320/en/content/tosca_commander/xmodules_properties.htm?Highlight=Properties%20for%20XModules


![alt text](/assets/image-22.png)

## Resolve Reference

Wenn ich von Library einen Folder reinziehe, sind die verknüpft. D.h. Wenn ich einen Step lösche, ist es überall gelöscht. Wenn ich für einen Testcase zwar die Steps aus der Library wiederverwenden möchte, aber für diesen einen Testfall einen Step rauslöschen, kann ich die Referenz auflösen:

![alt text](/assets/image-23.png)


## ResultCount

1 ist Modul TBox Set Buffer (Tricentis Standard Modules>>Tbox Automation Tools>>Buffer Operations>>TBox Set Buffer). Hier definiere ich zwei Buffer, SUM und OrderNumber.

2 ist Modul von mir (Order Overview). Ich bin auf der Orderübersicht und nutze ResultCount, damit Tosca bei der Auführung des Testcases zählt, wie oft das Control (hier das DIV OrderInfo) auf der Page vorkommt. Die Anzahl wird in den Buffer NumberOfOrder gespeichert

![alt text](/assets/image-24.png)

Dann füge ich einen Teststep-Folder hinzu und definiere in den Properties, wie oft der Teststep durchgeführt werden soll ("Repetition"). Ich setzt den Wert auf den Buffer(Achtung: Mit geschweiften Klammern und so) NumberOfOrders.

![alt text](/assets/image-26.png)

## Repetition

- CountUp läuft so oft durch, wie ich NumberOfOrder (wegen Property "Repetition", dass ich auf TestStep Folder gesetzt habe).
- Dank #{Repetition} <- ExplicitName, weiss Tosca, dass es jetzt gem. Property "Repetition" durchläuft, also gem. NumberOfOrder und jedes Element in der Liste angeschaut werden soll.
- OrderTotal wird gebuffert und im Sum up dem Buffer SUM hinzugefügt. String vorne ist fix, hinten Order Number ist dynamisch. Darum XBuffer `Order Total: {XB[OrderTotal]}` -> der dynamische (rosarote) Teil wird in XBuffer gespeichert.
    ![alt text](/assets/image-27.png)
- OrderTotal -> `.InnerText==Order Total: {XB[OrderTotal]}`
- SUM -> `{MATH[{B[SUM]} + {B[OrderTotal]}]}`

![alt text](/assets/image-25.png)

Nachdem ich den Testcase ausgeführt habe, schaut es dann so aus:

![alt text](/assets/image-28.png)

Values im Buffer - Looks good 👍

![alt text](/assets/image-29.png)

# Requirements

- Anforderungen erfassen und gewichten
- Requirement Folder, Requirement Set, Requirement
- Frequency class -> Gewichtung, wie oft etwas benutzt wird (je höher, desto mehr)
- Damage class -> Auswirkung/Schaden, wenn Funktion nicht funktioniert (je höher, desto schlimmer)
- Weight 2^Frequency * 2^Damage = Weight
- Ich kann dann den Requirements die Testfälle zuweisen
- In der Coverage sehe ich dann, wieviel % der Requirements abgedeckt sind
- <mark> Achtung bei den Zahlen: Wenn es fachlich eigentlich zwei Testcases bräuchte, ich haber nur einen am Requirement habe, sagt Tosca "100% Abdeckung" obwohl es fachlich nur 50% sind.


> Bemerkung von mir selber: Ist eigentlich wie eine Nutzwertanalyse.

> Requirements --> Use Cases auf unterschiedlicher Flughöhe¨

-> Auf Requirement gehen und mit Ctrl + T Testcase suchen und hinzufügen (oder per Drag and Drop von Testcase Folder)
-> Nachdem Testcases hinzugefügt wurden, Rechtsklick auf Requirement Folder und "Update Values"

![alt text](/assets/image-30.png)


# ExecutionList

ExecutionList -> Execution Entry --> Element representing a linked Testcase. Können in Execution Entry Folders strukturiert werden.

ExecutionList kann mit Requirements und Testcases oder einzelnen Testcase-Folder zusammengestellt werden. So bin ich sehr flexibel, wie ich die Execution Lists organisiere.

Im Gegensatz zum Scratch-Book, werden bei den ExecutionList die Logs gespeichert

1 Testfall kann nur 1 mal in Execution List sein. Aber ich kann beim Testcase in der Execution List das Property "Repetition" auf 'n' setzen.

<mark> Do not forget to define Test configuration auf der ExecutionList. Das überschreibt die Konfiguration auf den Testcases.

---
EXKURS - TQL - Tosca Query Language

![alt text](/assets/image-33.png)
---

Execution List mit Testcases erstellt und zu Requirements hinzugefügt. Ich muss es zu den Requirements hinzufügen, damit die Testcases dort als "Passed" markiert werden, wenn sie in der verlinkten ExecutionList "Passed" sind.

![alt text](/assets/image-31.png)

![alt text](/assets/image-32.png)

# Loops and Conditions

- WHILE - Before run condition is checked 
- DO - After run condition is checked
- IF

Es wird immer eine Condition geprüft

> Man sollte möglichst wenig Loops und Conditions benutzen. Wir machen keine Prozess-Automation, sondern Testcases! Evtl. macht es bei Recovery Szenarien sinn.

"Condition": Bedeutung - Wenn Teststeps in Condition = passed, dann wird "Then" ausgeführt, sonst nichts oder "Else"

EXKURS: Achtung bei Tables - Row + Column: #1 = 1. Reihe mit Header gilt als Reihe. $1 - 1. Reihe ohne Header

Der folgende Loop guckt, ob im Warenkorb die Produkttabelle vorhanden ist. Wenn ja, wird von jedem Eintrag in der Tabelle die Remove-Checkbox auf True gesetzt und mit click auf Update Shopping Cart wird der Eintrag gelöscht (diesen Loop durchläuft Tosca, solange es Produkte im Warenkorb hat, bzw. solange "TableExists==True")

![alt text](/assets/image-40.png)

![alt text](/assets/image-41.png)

# Recovery Scenarios & CleanUp

Recovery Scenarios are used to enable Tosca to react to certain common errors, e.g. an unexpected pop-up that appears randomly, on any page in your application, at any time during test execution.

Recovery Scenario kann ich auf Höhe Testcase, Testfolder, Teststep, whatever, definieren
Wenn ich sowohl auf dem Testcase wie auch auf dem Testfolder ein Recovery Scenario habe, fängt er "unten" an, und wenn das nicht funktioniert, geht Tosca ein Level höher.

![alt text](/assets/image-42.png)

Settings richtig setzen!
![alt text](/assets/image-43.png)

Beispiel:
In folgendem Testcase, wenn Testcase nicht funktioniert, wendet Tosca Recovery Scenario an (löscht alles aus dem Warenkorb) und beginnt den Testcase nochmals von vorne.

![alt text](/assets/image-44.png)

CleanUp Scenario -> Läuft, wenn alle Recoveries Scenarios versagt haben und Testfall nicht weiterläuft.

Auf Hierarchy achten!!

![alt text](/assets/image-45.png)

![alt text](/assets/image-44.png)

![alt text](/assets/image-47.png)

# Additional Topics
## Constraint

-> Ist ein ActionMode wie Buffer, Verify...

Wird in Tabellen benutzt, um eine bestimmte Row oder Column zu wählen

Nützlich wenn: 
- ich die Reihenfolge von Elementen in einer Tabelle nicht kenne

Mit Constraint kann ich dann sagen: Gib mir das Element, wo in "Columnname-X" BLA drin hat und in Columnname-Y BLUB 

![alt text](/assets/constraint.png)

## Fireevent
- Irgendwas mit JavaScript habe ich noch aufgeschnappt. Sind aber innerhalb 20 Sekunden durch das Thema und die Übung funktioniert nicht :-)

## Multiuser Environment
- Wenn mit mehreren User: Module etc müssen ausgechecked werden, bevor ich sie bearbeiten kann.
- Die anderen User sehen dann einen roten Balken und wissen: aha - ausgechecked
- Ausgecheckede Module kann ich trotzdem in einen Testcase ziehen.

- DB ist irgendwo auf einem Server - auf meinem Compi ist eine gesamte lokale Kopie. -> Performance ist ein Problem...

- um zu Arbeiten, muss ich ein- und auschecken


## TestCase Design

- TestDesign Specialist Kurs
- Testsheet mit Attributen
- TestSheet -> Völlig frei von Modulen. Ich kann einfach Designen, frei Attribute definieren, Instanzen machen etc.
- Testcase nehmen und dann "Convert to Template" -> Dann ist es eine Vorlage und ich kann die Werte aus dem Testsheet als Platzhalter ins "Value" reinnahmen. Aus dem Testcase Template kann ich dann gem. TestSheet Testcases instanzieren.






