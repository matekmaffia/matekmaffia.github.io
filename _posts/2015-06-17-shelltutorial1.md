---
title: I. Shell tutorial
layout: blog
tags: ["bash", "shell", "unix", "linux"]
---

Sziasztok!

Gondoltam ilyen is kellene, ezért belevágtam :) Akinek esetleg nem ismerős a shell, az [itt](https://hu.wikipedia.org/wiki/Unix_rendszerh%C3%A9j) kutakodhat. Az alapabb parancsokhoz elég lesz a [jslinux emulátor](http://bellard.org/jslinux). De előnyösebb ha saját rendszert, vagy liveCD-t használtok. Na de csapjunk is bele a lecsóba. Maga tutorial kisebb egységekbe van zárva, melyek többé-kevésbé függetlenek. Ha esetleg valamilyen parancs még nem érthető, akkor az majd a következő részben tisztázásra kerül, úgyhogy nem kell elkeseredni.

##Szemantika
Jelentés.
##Szintaktika
Forma, szerkezet.
##Szintaktika és szemantika kapcsolata
Egy programozási nyelv esetében éppen annyira van szükség formális, mind jelentésbeli tartalomra, mint egy valóságosban.
>Hiábavaló az a szó, mely beszél: szépen a semmiről vagy visszataszítóan a szépről! 
>-- @mraron

Vagy gondoljunk bele, hogy van 2-féle sós mogyoró márka, egyik nagyon finom ízű (szemantikája), viszont a marketingje (szintaktikája) nagyon rossz. A másik olyan ízű mint a csatornalé, de nagyon jó marketingje van. Egyik sem lehet sikeres, mert az első esetben nincsen vásárlóközönsége a mogyorónak, a másikban pedig lenne, de akik megkóstolják rögtön betiltatják a terméket.
Egy jó dologhoz mindig kell megfelelő belső és külső is. 
##Fájlrendszer
Az a hely, ahol mappáink és fájljaink tárolódnak. 
##Könyvtárstruktúra
Hierarchikus felépítése a mappáinknak és fájljainknak. Lényegében egy irányított gráf. 
##Escape Karakter (feloldójel stb.)
Olyan karakter, ami az utána következő karakterek értelmezését megváltoztatja. Például ilyen karakter a ```\``` shell-ben.
####Használat

 - Egy karakter speciális jelentésének feloldása
	 - Példa, echo-val kiszeretnénk írni egy macskakörmöt. Naívan beírjuk ezt a parancsot: ```$ echo """``` Ez viszont egy hibás kifejezés. Gondoljunk bele! A shell megtalálja az első macskakörmöt, feljegyzi magának, hogy itt kérem szépen, egy szöveg kezdődik. Jó, megy tovább. Látja, hogy itt van még egy macskaköröm, de mivel előzőleg felírta magának, hogy egy szövegben van, ezért tudja, hogy most ez a karakter annak befejezését jelzi. Jó, megy tovább. Lát még egy macskakörmöt, jó: szöveg kezdődik, megy tovább. Aztán hirtelen vége a sornak. De a shell észreveszi, hogy még egy szövegnek nincs vége és ezért hibát jelez. A kifejezés helyesen pedig ```$ echo "\""```, így megszűnik a második macskaköröm speciális jelentése, és ezzel már minden macskakörömnek van párja, és így a kifejezés helyes lesz.
 - Egy karakternek speciális jelentés adományozása
	 - ```\n```  újsor
	 - ```\t``` tabulátor

####Példák
```
$ printf "\n"

$ printf "\ta"
	a
$ echo "\""
"
```


##Komment
A shell ha lát egy ```#```-t, akkor az utána található karaktereket _kommentnek_ tekinti, tehát _nem veszi figyelembe_ őket, ez olyan mintha nem is írtuk volna le ezeket. Ez az állapot egészen a következő sorig tart.
#### Példa
```
$ # echo"test" 
$ echo # "test"

$ echo "test"
test
```
##Parancs
Egy parancs két részből áll:

 - Parancsnév
 - Argumentumok

Minden parancsnak, egy neve van és korlátlan számú argumentuma lehet. Felépítésileg először a parancsnevet írjuk, majd szóközzel elválasztva az argumentumokat. 
####Példa
```
$ echo -n jaj
```

 - Parancs: echo -n jaj
	 - Parancsnév: echo
	 - Argumentumok:
		 1.  -n
		 2.  jaj 

##Szöveg
Szövegnek tekintünk egy véges hosszú karakterekből álló sorozatot. Ha szövegben szóközök is vannak, akkor macskakörmök közé kell pakoljuk, ha nem akkor nem szükséges ilyet tenni.
####Példa
```
jasdfsafd
"jasd fsafd"
"jasdfsafd"
```
##Kapcsolók
Kapcsolóknak nevezzük azokat a argumentumokat, amelyek "-"-szal kezdődnek. Általában a többi argumentum elé kerülnek, ha nem akkor az fel van tüntetve.

##Útvonalak
Kétféle útvonalat különböztetünk meg:

 - Abszolút
 - Relatív

Abszolútnak tekintünk minden olyan útvonalat, amely "/"-rel kezdődik, relatívnak amik meg nem.

Példának képzeljünk el egy olyan fájlrendszert amiben 2 mappa van "a" és "b", mindkettejükben van még egy "c" mappa is. Képzeljünk továbbá el egy elég kínos szituációt: egyik reggel bekapcsoltuk gépünket, majd elmentünk reggelizni, reggeli utánra pedig elfelejtettük, hogy éppen melyik mappában álltunk, csak azt tudjuk, hogy "/a/c"-be szeretnénk eljutni.

Ekkor ha beírjuk azt a parancsot, hogy "cd c/", akkor az "/a/c"-ben is vagy a "/b/c"-ben is kiköthetünk, attól függ, hogy előzőleg az "a"-ban vagy a "b"-ben álltunk. De ha azt írjuk, hogy "cd /a/c", akkor egyértelműen megmondjuk a shellnek, hogy arra "c"-re gondolunk, amely "a"-ban van. (nem pedig a másikra)

Így tehát a "cd c/" relatív, mert eredménye attól függ, hogy előzőleg milyen mappában álltunk és a "cd /a/c" abszolút, mert nem függ az előző helyzetünktől.


folyt. köv.

_@mraron_
