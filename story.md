     V8 Wüste    
=================
this is not the end
-------------------

Umgebung
---------

V8 JavaScript Engine von Google (weiter JavaScript Engines_)
ECMA-262_ das heißt Version 5.1 des Sprachstandards

Damit das Sandel auch spaß macht
```bash
git clone https://github.com/rrawrriw/v8-desert.git
cd v8-desert 
d8 // Ready to rumble
```

 Prolog
--------

Die Sonne scheint. Crock sitz in seinem Auto. Wind weht durch seine Barthaare und lässt sie im klang der Stille wild umher tanzen. "Manchmal ist es einfach gut nur zu 'Sein'!". Jedoch ist es *nicht* so gut, einfach hier zu 'Sein'. Sitzend, in seinem kaputten Auto, in der V8-Wüste_! Der Staub verklebt einem die Augen saugt jeden versuch der Befeuchtung auf wie ein kleines Kind die versteckte Schokolade. Jeder Wimpernschlag lässt 80er Schmirkelpapier über das Auge gleiten. Wobei die Nützlichkeit eines Wimbernschlags eines Echos gleichkommt, das erzeugt wurde durch einen einsamen Stein in einem leeren Raum, in dem Wände, Boden und fallender Stein taub sind. *aber es muss halt gemacht werden*. "'Sein' möchte ich wo anders sein".


Überlebens-Regel Nr.1 Erkunde die Umgebung (V8)
-----------------------------------------------

Überleben in der Wüste für Fortgeschrittene. Such die Spuren eines verwirrten Kamels. 

Lasst uns in die Wüste gehen und schauen was für große Abenteuer uns erwarten, oder halt auch nicht! Führe d8 auf der Konsole aus und tauche ab in das große Sandelabenteuer das weder feucht noch fröhlich ist.

```javascript
# d8
d8> load("desert.js");
```
  
Nehmen wir ein wenig Zeit zur erkundung der standard Umgebung.

```javascript
d8> for (o in desert) { print(o) };
print
write
read
readbuffer
readline
load
quit
version
enableProfiler
disableProfiler
ArrayBuffer
Int8Array
Uint8Array
Int16Array
Uint16Array
Int32Array
Uint32Array
Float32Array
Float64Array
Uint8ClampedArray
lol_is_enabled
os
arguments
sand
crown_cap
desert
grain_of_sand
sandcastle
spide
```

Wir laufen durch "desert" und lassen uns mit print alle Objekte ausgeben, die wir in desert finden.

Die ersten Objekte die wir finden werden von v8 erstellt. Die v8 Konsole enthält Objekte die man in einer Browser Umgebung nicht antrifft. Weil sie dort kein Sinn machen oder aus Sicherheitsaspekten äußerst bedenklich sind. 

Sandel, sandel.
```javascript
d8>  print("funky!") 
funky!
d8> * write("sandy!")d8> quit()
```

Befehle für Posix Kompatible Betriebsysteme.
* os.system
* os.chdir
* os.setenv
* os.unsetenv
* os.unmask
* os.mkdirp
* os.rmdir

Die unbeteiligte Stimme aus dem OFF kann sich vorstellen das, falls ihr noch nicht verdurstet seit, die folgende Frage schwer auf euren Schultern lasstet "Zur Hölle was macht eine Variable oder Objekt namens desert in der Standard Umgebung?". Das Objekt haben wir uns eingefangen als wir desert.js geladen hatten. desert enthältt eine Referenz auf das this Objekt.

```javascript
desert = this;
```

```javascript
# d8
d8> load("desert.js");

d8> beer
(d8):1: ReferenceError: beer is not defined
beer
^
ReferenceError: beer is not defined
    at (d8):1:1

d8> 
```

Was ist this, kein Bier?

```javascript
d8> for (e in this) { print(e) }
print
write
read
readbuffer
readline
load
quit
version
enableProfiler
disableProfiler
ArrayBuffer
Int8Array
Uint8Array
Int16Array
Uint16Array
Int32Array
Uint32Array
Float32Array
Float64Array
Uint8ClampedArray
lol_is_enabled
os
arguments
```

Verdammt, wirklich kein Bier?

```javascript
d8> this.hasOwnProperty("beer");
false
```

Jetzt mal mit Ernst!


Erlösen wir Crock lassen wir ihm ein Bier.

```javascript
d8> var beer = Object.create(Object, {
  status: {
    writeable: false,
    value: 'empty'
  }
});
d8> beer.status
empty 
```
*schluchz*

```javascript
d8> beer.status = "full"
full
d8> beer.status
empty
```

*so gemein*

Schmollend zeihen wir uns hinter die nächste Düne zurück.

```javascript
d8> var dune = {behind: {}}
d8> dune.behind = function () {
  this.beer.status
}
d8> dune.behind()
empty
```

Mach dir keine Hoffnungen!

Durch Panik getrieben rennen wir mit letzten Kräften richtung Nord. Norden bedeutet kälte, außer man befindet sich auf der unternhälfter der Südehalbkugel, oder ist zu Fuß in der Wüste unterwegs. Nach unglaublichen langen Sekunden brechen wir zusammen, überlassen uns wimmernt dem Tod, soll er doch kommen! Fieberträume bringen uns Bilder von schönen Frauen

```javascript
d8> dream = function ()
    print("beauty is cuddleing", this.me)
}

d8> beauty.cuddle()
beauty is cuddleing undefined
```

*Halt das ist mein Traum*

```javascript
d8> me = {
  me: "Crock"
}

d8> dream.apply(me)
beauty is cuddleing Crock
```
*Schon besser*

Doch bekanntlich holt einen die Realität schneller ein als gewünscht.

```javascript
realitiy = function (you) {
  print(you.me, "is fighting with camle spider")
}
Crock is fighting with camle spider
```

```javascript
d8> theSpider = {
    toxic: "100%",
    kills: function () {
      print("the spider kills "+ this.me +" to "+ this.toxic)
    }
}
d8> Spider = function () {
  return Object.create(theSpider)
}
d8> spider = new Spider()
d8> me.toxic = "0%, insted it gives him a beer"
d8> spider.kills.apply(me)
the spider kills Crock to 0%, insted it gives him a beer
```
Spinne am Arsch! Es lebe die Dynamik.

Wie von Blitz getroffen fällte es Crock ein hatte er nicht gelesen das Forscher herausgefunden hatten das die Spinne aller Spinnen die Urspinne einen Gendefekt hatte welcher dazu führt, berührt man die Spinne an der Achillesferse verwandelt sich die Spine in eine flasche Bier.

```javascript
d8> theSpider.achillesheel = function () {
  this.status = "tasty, full and cool beer!"
}
d8> spider.__proto__
d8> spider.achillesheel()
d8> spider.status
tasty, full and cool beer!
```

Gelernt ist gelernt! Das ist auch schon das verirrte Kamel

```javascript
d8> desert.lostCamel = {
  ride: function () {
    person = arguments[0];
    print("bring "+ person.me +" to perl land");
  }
}
d8> lostCamel.ride(me)
bring Crock to perl land
```

CYA

.. _V8-Wüste: http://code.google.com/p/v8/
.. _v8_commands: http://www.sandeepdatta.com/2011/10/using-v8-javascript-shell-d8.html
.. _Engines: http://en.wikipedia.org/wiki/List_of_ECMAScript_engines
.. _ES5: http://www.ecma-international.org/publications/standards/Ecma-262.htm


