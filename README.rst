======
Python
======

-----
Intro
-----

* Autor, Benevolent Dictator For Life je Guido Van Rossum
* 90-te roky: začiatky, 00-te: úspech, 10-te: Python 3
* Nedávno prešiel drastickou zmenou z Python 2 na Python 3,
  kde sa jazyk prečistil a prelomila sa kompatibilita 
* Interpretovaný bytekód (väčšinou)
* Existujú JIT implementácie (PyPy), kompilované napodobeniny (Cython, Genie)
* Pomalý, žerie veľa pamäti (10-20 krát pomalší ako C/C++, heavyweight objekty)

  - Program chrústajúci veľké dáta čisto v Pythone bude omnoho pomalší ako v Jave

* Rýchly, nenáročný na pamäť (jednoducho sa kombinuje s C/C++, všetky knižnice 
  sú v C/C++)

  - Program využívajúci C/C++ knižnice (štandardné, NumPy, Qt, Gtk) bude rýchlejší ako v Jave

* Čitateľnosť kódu a produktivita programátora má prednosť pred rýchlosťou
* Batteries included
* Veľmi dynamický:

  - Netreba deklarovať typy 
  - Kód je veľmi krátky, prehľadný
  - Do akeľkojvek funkcie/metódy sa dá napchať čokoľvek 
  - Metódy/premenné objektu sa dajú pridávať/mazať/meniť za behu
  - Ak napcháte do funkcie ktorá chce stringy číslo, vybuchne to až keď je tá funkcia zavolaná za behu - výnimky namiesto kompilačných chýb.

* OOP, funkcionálne/aspektové/meta prvky, ale nie je napr. funkcionálny
* Na všetko by mal existovať jeden správny a prehľadný - *Pythonický* spôsob, ako to spraviť.
* Dobrý na dynamické web stránky, GUI, náhrada bash skriptov, 
  skripty v 3D nástrojoch, hrách, numerické programovanie.
* Zlý na multithreading, ako základný jazyk veľkých projektov
* Beží na všetkom


-----
Setup
-----

* Inštalácia Python 3 na Linuxoch:

   ``sudo apt-get install python3``
   (alebo package manager vášho distra)

   Python 3 skript začína: 

   ``#!/usr/bin/python3``

   (Nezabudnúť na ``chmod +x blah.py``)

* Všade: webový Python 3 interpreter napr. na http://ideone.com/ 
  (Choose language -> Python 3)

`Tutoriál vrátane inštalácie na Windows <http://getpython3.com/diveintopython3/installing-python.html>`_

^^^^^^^^^^^
Hello world
^^^^^^^^^^^

.. code::

   print("Hello World")

Poznámka o číslach

Čísla v Pythone môžu byť akokoľvek dlhé, vo vnútri pracuje podľa potreby 
s hardwarovým intom a ekvivalentom BigIntu. Programátora to väčšinou nemusí 
zaujímať.

.. code:: 

   print(2 ** 256)

^^^^^^^^
Vetvenie
^^^^^^^^

.. code::

   if False or 0 or None or [] or "":
       print("Not gonna happen")
   elif True and 1 and "whatever":
       print("Hello World")
   
   if 5 > 6:
       pass 
   else: 
       print("Nope.")
   
`Dokumentácia if <http://docs.python.org/3/tutorial/controlflow.html#for-statements>`_
   
^^^^^
Cykly
^^^^^

.. code::

  for i in range(1000):
      print(i)

  for i in range(-1000, 1000):
      print(i)

  # preskakovanie
  for i in range(-1000, 1000, 2):
      print(i)

  for s in ["ho", "lee", "fuk"]:
      print(s)

  i = 0
  while True:
      print("Still alive")
      if(i == 42):
          break
      i += 1

`Dokumentácia for <http://docs.python.org/3/tutorial/controlflow.html#for-statements>`_

^^^^^
Listy
^^^^^

.. code::

  # môže obsahovať čokoľvek
  list = [1, 2, 3, 4, 5, 6, "Stalin", 8, [[[[["Combbbo breaker"]]]]]]

  # typ whatever sa mení
  for whatever in list:
      print(whatever)

  print(list[0])
  print(list[-1])
  print(list)
  print(list[1:])
  print(list[:-1])
  print(list[1:-1])

  # deletovanie
  del list[5]
  del list[1:5]

  # dĺžkla 
  print len(list)

  # List comphrehensions:

  squares = []
  for i in range(10):
      squares.append(i ** 2)

  # sa dá zapísať:
  squares = [i ** 2 for i in range(10)] 
  print(squares)
  
  # 2 for cykly + if:
  pairs = [(x, y) for x in [1,2,3] for y in [3,1,4] if x != y];
  print(pairs)

* BTW, string je list

`Dokumentácia listov <http://docs.python.org/3/tutorial/datastructures.html>`_
 

^^^^^^^
Funkcie
^^^^^^^

.. code::

   # jednoduchá funkcia 
   def count_upper(string):
       result = 0;
       for c in string:
           if c.isupper:
               result+=1
       return result

   print(count_upper("The Brian Fargo"))
  
   # viac návratových hodnôt
   def bifurcate(list):
       odd  = [list[x] for x in range(len(list)) if x % 2 == 1]
       even = [list[x] for x in range(len(list)) if x % 2 == 0]
       return (odd, even)

   numbers = [1, 9, 2, 8, 3, 7, 4, 6, 5]

   # tuple unpacking
   (part1, part2) = bifurcate(numbers)

   print(part1, part2)

   # Arguments can have default values
   def a_function_with_many_arguments(x, y, z, grist = 5, bifurcate = False, dead_unicorns = 5.1):
       print("whatever")

   # Arguments can be specified by name
   a_function_with_many_arguments(1, 3, 0, dead_unicorns = 8, bifurcate = True)

`Dokumentácia funkcií <http://docs.python.org/3/tutorial/controlflow.html#defining-functions>`_

^^^^^^^^^^
Operátory 
^^^^^^^^^^

* Podobné ako v C/Jave/C++

* Bez ++, --

* Rozdielne:

  ====== =============================================
  /      Reálne delenie (aj keď argumenty sú integery)
  //     Celočíselné delenie
  \*\*   Umocňovanie (aj s reálnym mocniteľom)
  in     Je v kolekcii
  and    Namiesto &&
  or     Namiesto || 
  not    Namiesto !
  ====== =============================================

* Preťažiteľné ( > pre stringy)

**Príklady**::

   # 2.5
   print(5 / 2)
   # 2
   print(5 // 2)
   # veľa
   print(1001 ** 1001)
   # netreba sqrt
   print(1001 ** 0.5)

   # True
   print(5 in (5, 6))
   # False
   print(5 in [4, 6, 7])

   # True
   print(True and 5 == 5.0);
   # False
   print(not True);

   # ==, <, >, atď sa dajú reťaziť
   # True
   print(1 == 1.0 > 0.0)
   # False
   print(1 == 1.0 > 1.0)


^^^^^^
Moduly
^^^^^^

.. code::

   import math 
   print(math.pi)

   from math import pi 
   print(pi)

   from math import *
   print(pi, e)

`Dokumentácia modulov <http://docs.python.org/3/tutorial/modules.html>`_


^^^^^^^^^^^^^^^^^^^^
Builtin dokumentácia
^^^^^^^^^^^^^^^^^^^^

.. code::

   # dokumentácia pre stringy
   help("str")
   # dokumentácia modulu math 
   help("math")
   # zoznam mien modulov pre help()
   help("modules")
   # zoznam mien článkov pre help()
   help("topics")
   # zoznam kľúčových slov pre help()
   help("keywords")

^^^^^^^
Výnimky
^^^^^^^

.. code:: 

   raise NameError('HiThere')

.. code::

   def divide(x, y):
      try:
          result = x / y
      except ZeroDivisionError:
          print("division by zero!")
      else:
          print("result is", result)
      finally:
          print("cleaning up")

Niektoré triedy tiež podporujú RAII cez *with* statement; 
súbor otvorený vo with sa zavrie pred koncom tohto with, bez ohľadu na chyby:

.. code::

   with open("myfile.txt") as f:
      for line in f:
          print(line, end="")

`Dokumentácia výnimiek <http://docs.python.org/3/tutorial/errors.html>`_

^^^^^^
Triedy
^^^^^^

Referencia na triedu vždy explicitná cez *self*.  Objekty v Pythone môžu byť za
behu menené; dajú sa pridávať, odoberať, meniť metódy/premenné každej inštancie
zvlášť. Existujú pseudo-privátne premenné/metódy (prefix ``__``), ale aj to sa
dá obísť.

.. code:: 

   class Entity:
      dead = False

   class SteveB(Entity):
      def __init__(self, chairs):
          # Polia/metódy nemusia byť v deklarované triede, môžu byť pridané 
          # kedykoľvek/kdekoľvek.
          self.chairs = chairs
          self.__developers = ["Developers", "Developers", "Developers"]

      def monkey_dance(self):
          if self.dead:
              return
          for i in self.__developers:
              print(i.upper() + "!!!")

      def attack(self):
          if self.dead:
              return
          if self.chairs == 0:
              print("out of ammo")
              return False
          self.chairs -= 1
          return True

      dry_shirt = False


   s = SteveB(1)
   s.monkey_dance()
   s.attack()
   print(s.dry_shirt)

   # Don't do this at home
   s.wtf = "a new field added on the run"
   print(s.wtf)

   s.attack = "BoggyB"
   print(s.attack)


^^^^
Štýl
^^^^

Python má jediný zaužívaný štýl:
`PEP 8 <http://www.python.org/dev/peps/pep-0008/>`_.


------------
Dokumentácia
------------

==================================================================================== =
`Dokumentácia <http://docs.python.org/3/>`_
`Dive into Python <http://www.diveinto.org/python3/>`_
`Wiki <https://wiki.python.org/moin/>`_
`ReStructuredText tutoriál <https://github.com/kiith-sa/RestructuredText-tutorial>`_
`Ďalšie tutoriály <https://wiki.python.org/moin/BeginnersGuide/Programmers>`_
==================================================================================== =

------------------------
Knižnice, web frameworky
------------------------

======================================================================== ===============================================================
`Tinkerer <http://tinkerer.me/>`_                                        Statický web framework založený na ReStructuredText
`Hyde <https://github.com/hyde/hyde>`_                                   Populárny statický web framework
`Flask <http://flask.pocoo.org/>`_                                       Minimalistický web framework
`Django <https://www.djangoproject.com/>`_                               Populárny web framework
`Pyramid <http://www.pylonsproject.org/projects/pyramid/about>`_         Ďalší web framework čo vyzerá dobre
`NumPy <http://www.numpy.org/>`_                                         Numerické rozšírenie Pythonu, základ pre rôzne vedecké knižnice
`PyGame <http://www.pygame.org/>`_                                       Knižnica na tvorbu hier založená na SDL
`PyQt <http://www.riverbankcomputing.co.uk/software/pyqt/intro>`_        Bindings pre Qt
======================================================================== ===============================================================
