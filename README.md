# SpaceRocket-Projekt-Informatik-von-Finn-Westphal-und-Robin-Wagner
## Projekt von Robin Wagner und Finn Westphal

##Inhaltsverzeichnis

##Einleitung: Anforderungen und Elemente des Spiels
Space Rocket ist ein Highscore-Spiel auf Greenfoot-Basis, in dem man mit einer Rakete, die sich am linken Bildschirmrand befindet und sich nur nach oben oder unten bewegen kann, versucht, Asteroiden, die nur von der rechten Bildschirmseite heranfliegen, in einem Asteroidenfeld auszuweichen. Jeder Asteroid verschwindet aus der Welt, wenn er den Rand der Welt erreicht. Man verliert, wenn man mit einem Asteroiden zusammenstößt.
 
###Umsetzung
Wir programmieren unser Projekt "SpaceRocket" in der Programmierumgebung "Greenfoot", die auf der obejktorientierten Programmiersprache *Java* basiert. welche Größe, welches Format und welche Auflösung unsere Welt haben soll. Unser Spiel soll über eine klassische Auflösung und ein klassischen Seitenverhälnis verfügen, damit es auf jedem Computer spielbar ist. Wir haben uns deswegen für das Seitenverhältis von 16/9 und eine Auflösung von 960 * 540 Pixeln entschieden. Diese Bildeigenschaften sind von den meisten aktuellen Displays umsetzbar. Wir haben in Greenfoot 
Greenfoot generiert beim erstellen eines Szenarios ein Zellen-Koordinatensystem, das deckungsgleich zur generierten Welt ist. Das Verhältnis zwischen Pixeln und Zellen ist variabel und durch einen Parameter definiert (In diesem Fall 1).

```javascript
public space_backround_1()
    {
        super(960, 540, 1, true);
        addObject(new rocket(), 150, 270);
        addObject(new counter(), 30, 510);
        addObject(new Asteroid(), 960, Greenfoot.getRandomNumber(540) - 0);
        addObject(new Asteroid(), Greenfoot.getRandomNumber(480) + 480, 1);
        addObject(new Asteroid(), Greenfoot.getRandomNumber(480) + 480, 960);
    }
```


Das Super ist einfach eine bestimmte Methode, die die Welt mit ihren Eigenschaften kreiert. Durch das true erreichen wir, dass die Asteroiden und auch die Rakete zunächst nicht aus der Welt verschwinden können, sondern am Rand der Welt festhängen. 
Danach haben wir in Greenfoot einen Hintergrund unserer Welt gesucht, der möglichst zum Spiel passen sollte. In unserem Fall der Weltraum-Hintergrund. Desweiteren haben wir uns überlegt, welche Actor-Klassen wir überhaupt benötigen. Wir benötigen in jedem Fall zunächst eine Raketen- und eine Asteroiden-Klasse. Andere Klassen, die wir für unser Spiel später auch brauchen, z.B. eine Score- oder gamve-over Klasse, haben wir zunächst vernachlässigt. Erst einmal wollten wir, dass jeweils vor Spielbeginn eine Rakete an einem festen Ort startet und verschiedene Asteroiden an immer anderen Punkten der Welt, allerdings nur in der rechten Hälfte der Welt, spawnen. Dazu haben wir, wie in dem obigen Befehl zu sehen, mithilfe von addObject eine Rakete hinzugefügt, die jedes Mal, wenn man das Spiel startet, an der Position X= 150 und Y= 270 startet. Diese Koordinaten haben wir so gewählt, dass die Rakete ziemlich weit links, aber nicht am Rand, startet und genau die Hälfte der Höhe besitzt. Weiterhin lassen wir Asteroiden Spawnen, die sich an immer anderen Positionen befinden können. Der erste Asteroid hat die X-Koordinate 960 und befindet sich genau am rechten Rand der Welt mit einer Y-Koordinate die von 0 bis 540, also von ganz unten bis ganz oben variieren kann. Dies erreichen wir durch den Befehl Greenfoot.getRandomNumber . Der 2. Asteroid kann zwischen den X-Koordinaten 480 und 480+480, also 960 entstehen. Das Bedeutet, dass er immer zufällig zwischen der Hälfte der Welt und dem rechten Ende spawnt. Die y-Koordinate beträgt 1, weshalb der Asteroid bei den genannten x- Koordinaten immer ganz unten entsteht. Der 3.Asteroid hat die gleichen X-Koordinaten, spawnt aber durch die festgelegte y-Koordinate immer ganz oben. Hinzuzufügen ist außerdem, dass Greenfoot bei einer zufälligen Zahl, also dem Befehl Greenfoot.getRandomNumber nur Zahlen aus dem Bereich von 0 bis zur natürlichen Zahl vor der gewollten Zahl nimmt, also bei z.B. 1 liegt diese "zufällige" Zahl immer bei 0. Der Counter hat in unserer Welt noch keine Bedeutung, da wir noch keine Counter-Klasse erstellt haben. 

Danach haben wir uns um die Rakete gekümmert. Diese soll sich zwar nicht nach links und rechts bewegen, da die Asteroiden auf die Rakete hingeflogen kommen sollen, aber sie soll sich nach oben und unten bewegen können. Zuerst haben wir ein Bild einer Rakete zur Actor-Klasse Rocket hinzugefügt und uns dann mit dem Code beschäftigt. Mithilfe von public void act konnten wir erstmal festlegen, dass die Rakete alles das tut, was wir ihr befehlen. Hier haben wir mit den Befehlen setRotation und setLocation gearbeitet. Mithilfe von setRotation können wir festlegen, ob die Rakete sich in einem bestimmten Winkel dreht oder eben nicht. Mit setLocation können wir der Rakete einen neuen Ort, also neue Koordinaten zuordnen. Da sich die Rakete in der Ausgangsposition nicht bewegen soll, haben wir erstmal setRotation=0 gesetzt. Und weil wir die Rakete steuern wollen, haben wir festgelegt, dass, wenn s oder alternativ die Pfeiltaste nach unten bewegt wird, die Rakete um 20 Grad nach unten rotiert und einen neuen Platz erhält. Dieser ist durch die  X-Koordinate, die gleich bleibt und die Y-Koordinate, die immer um 12 vergrößert wird, damit die Rakete sich auch bewegt, festgelegt.
Gleichzeitig soll die Rakete aber nie den unteren Bildschirmrand erreichen, weshalb wir gesagt haben, dass die Y-Koordinate immer noch kleiner sein soll als 540. Genau andersherum funktioniert es, wenn man die w Taste oder alternativ die Pfeiltaste nach oben drückt. Die Rakete bewegt sich um 20 Grad nach oben, erhält eine um 12 verringerte y- Koordinate (die X-Koordinate bleibt gleich), damit die Rakete nach oben rotiert und gleichzeitig durch den Befehl getY() > 0) aber nie den oberen Rand der Welt erreicht. Somit war die Programmierung der Rakete abgeschlossen, da das alles ist, was die Rakete können soll.

Anschließend haben wir uns um die Programmierung der Asteroiden gekümmert, in die wir bisher am meisten Zeit hineingesteckt haben. 

