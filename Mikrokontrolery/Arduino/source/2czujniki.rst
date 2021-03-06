********
Czujniki
********

Informacje wstępne
==================

Arduino to platforma dla systemów wbudowanych, oparta w większości o 8-bitowe mikrokontrolery z rodziny AVR; jest to płytka drukowana z mikrokontrolerem i jego wyprowadzeniami zdolna obsługiwać urządzenia zewnętrzne np. czujniki, sterowniki silników, wyświetlacze itp.

Na płytce Arduino Uno znajdziemy 6 wejść analogowych, pozwalających obsługiwać wszelkiego rodzaju czujniki. 

Opisy przykładowych czujników zaczerpnięte zostały ze strony firmy `BOTLAND`_.

Obsługa wejść analogowych
=========================

W Arduino dostępnych jest kilka linii analogowych, z wykorzystaniem których można mierzyć analogowe sygnały, na przykład z czujników, w przedziale napięcia od :math:`0 V` do :math:`5 V` i z rozdzielczością 10 bitów, co oznacza, że mierzone napięcie będzie odczytywane wartościami od 0 do 1023. Dla :math:`5 V` daje to rozdzielczość :math:`\frac{5 V}{1023} = 0.0049 V = 4.9 mV`. Zakres rozdzielczości przetwornika można zmienić za pomocą funkcji ``analogReference()``. Pomiar wartości analogowej trwa około :math:`100 µs`. Konfiguruje się je, identycznie jak linie cyfrowe, za pomocą funkcji ``pinMode()``, ``digitalWrite()`` i ``digitalRead()``, z tym że parametr ``<pin>`` jest oznaczany za pomocą aliasów od A0 do A5. Analogowe linie również posiadają cyfrowo załączane rezystory podwyższające, które można włączyć z wykorzystaniem funkcji ``digitalWrite()``. Aby działało wejście analogowe mikrokontrolera musi ono być wcześniej ustawione jako wejście z wykorzystaniem funkcji ``pinMode()``. Należy również wyłączyć rezystor podwyższający. Do odczytu napięcia z linii analogowej mikrokontrolera służy funkcja ``analogRead(<pin>)``. Parametrem ``<pin>`` jest linia analogowa. Na przykład komenda 

.. code-block:: c++

	val = analogRead(A2); 
	//odczyt wartości sygnału z linii A2

powoduje odczyt wartości analogowej z linii A2 i przypisanie jej do zmiennej ``val``. Dostępna jest również funkcja ``analogReference(<type>)``, za pomocą której można zmienić parametry pracy przetwornika analogowo-cyfrowego mikrokontrolera. Parametr ``<type>`` określa napięcie odniesienia dla przetwornika. Dostępne są następujące opcje:

- DEFAULT: domyślna, napięcie odniesienia dla przetwornika jest napięciem zasilającym mikrokontroler, czyli :math:`5 V` lub :math:`3.3 V`,

- INTERNAL: wbudowane napięcie odniesienia równe :math:`1.1 V` dla ATmega168 (dla ATmega328 na Arduino Uno również),

- INTERNAL1V1: wbudowane napięcie odniesienia równe :math:`1.1 V` dla Arduino Mega,

- INTERNAL2V56: wbudowane napięcie odniesienia równe :math:`2.56 V` dla Arduino Mega,

- EXTERNAL: zewnętrzne napięcie odniesienia dołączone do linii AREF, mieszczące się w przedziale od :math:`0 V` do :math:`5 V`.

Możliwość zmiany napięcia odniesienia dla przetwornika A/C mikrokontrolera daje możliwość dostosowania się do wartości mierzonego sygnału analogowego z wymaganą rozdzielczością pomiaru.

Przykłady czujników
===================


Fototranzystor
--------------

**Fototranzystor TEFT4300:**

.. figure:: fototranzystor3.png
   :align: center

*Specyfikacja:*

- Maksymalna czułość dla fali o długości: :math:`925 nm`

- Filtr światła dziennego

- Szybki czas odpowiedzi

- Kąt odczytu: :math:`± 30°`

.. figure:: fototranzystor6.png
   :align: center
   :width: 600px

.. figure:: fototranzystor2.png
   :align: center

Fototranzystor w obudowie :math:`3 mm`. Soczewka zaciemniona.﻿

Poniższy rysunek przedstawia wykres czułości czujnika w funkcji długości fali:

.. figure:: fototranzystor.jpg
   :align: center


Szczegóły w `dokumentacji. <http://botland.com.pl/attachment.php?id_attachment=77>`_

Fotorezystor
------------

**Fotorezystor 20 - 30 kΩ GL5537-1:**

.. figure:: fotorezystor.jpg
   :align: center

*Specyfikacja:*

- Symbol: GL5537-1

- Rezystancja jasna: :math:`20 kΩ - 30 kΩ`

- Rezystancja ciemna: :math:`2 MΩ`

- Napięcie maksymalne (DC): :math:`150 V`

- Moc maksymalna: :math:`100 mW`

- Rozmiar: 5 mm x 2 mm

- Temperatura pracy: od :math:`-30 °C` do :math:`+70 °C`

.. figure:: fotorezystor2.png
   :align: center

.. figure:: fotorezystor3.png
   :align: center

.. figure:: fotorezystor4.png
   :align: center
   :width: 600px


Szczegóły w `dokumentacji. <botland.com.pl/attachment.php?id_attachment=305>`_


Czujniki wilgotności
--------------------

**Czujnik wilgotności gleby:**

*Opis:*

Czujnik, służący do wyznaczania poziomu wilgotności gleby. Zasilany jest napięciem od :math:`3.3 V` do :math:`5 V`. Posiada wyjście cyfrowe oraz analogowe, co czyni go kompatybilnym z większością modułów uruchomieniowych, w tym Raspberry Pi i Arduino. Urządzenie może być stosowane np. do pomiaru wilgotności gleby w doniczce. 

*Obsługa czujnika:*

Urządzenie składa się z trzech części﻿: sondy pomiarowej, modułu detektora oraz przewodów. Sondy należy połączyć z modułem głównym przy pomocy przewodów i umieścić w glebie, której wilgotność będzie mierzona.

Czujnik posiada wyjście cyfrowe D0 sygnalizujące przekroczenie ustawionej za pomocą potencjometru wartości oraz analogowe A0, przy pomocy którego uzyskuje się dokładną wartość wilgotności. 
 
*Wyjście cyfrowe D0:*

Za pomocą potencjometru ustawiany jest próg, po którego przekroczeniu wyjście D0 przechodzi ze stanu wysokiego w stan niski. Wyprowadzenie D0 można połączyć bezpośrednio z mikrokontrolerem ﻿bądź zestawem uruchomieniowym, w tym Arduino ﻿lub np. z modułem buzzera, który będzie sygnalizował zbyt niski bądź wysoki poziom wilgotności.

*Wyjście analogowe A0:*

Czujnik posiada także wyjście analogowe A0, które należy podłączyć do wyprowadzenia przetwornika A/C (wejścia analogowego w Arduino﻿). Pozwoli to, mierząc proporcjonalny﻿ sygnał napięciowy, dokładniej określić poziom wilgotności.
 
*Zawartość zestawu:*

- Sonda pomiarowa

- Moduł główny

- 5 przewodów połączeniowych




Czujniki prądu
--------------

**Czujnik prądu ACS711KLCTR ± 25 A - SMD:**

.. figure:: prad3.png
   :align: center

*Specyfikacja:*

- Napięcia zasilania części logicznej: :math:`3 V - 5.5 V`

- Pobór prądu częsci logicznej: maks. :math:`5.5 mA`

- Zakres: :math:`± 25 A`

- Czułość: :math:`55 \frac{mV}{A}`

- Obudowa: SOIC8 (SMD)

.. figure:: prad.png
   :align: center

*Opis:*

Czujnik prądu, działający w zakresie :math:`± 25 A` na podstawie efektu Halla (`wiki <http://en.wikipedia.org/wiki/Hall_effect>`_). Wyjściem jest napięcie analogowe. 

.. figure:: czpradu.jpg
   :width: 600px
   :align: center

.. figure:: prad2.png
   :width: 600px
   :align: center

Pin FAULT, normalnie znajdujący sie w stanie wysokim, osiąga stan niski, gdy wartość mierzonego prądu przekroczy dopuszczalny zakres :math:`± 25 A`.

Szczegóły w `dokumentacji <botland.com.pl/attachment.php?id_attachment=147>`_


Czujniki ruchu
--------------

**Czujnik ruchu PIR HC-SR501:**

*Specyfikacja:*

- Napięcie zasilania DC﻿: :math:`4.5 V - 20 V`

- Pobór prądu w stanie czuwania: :math:`50 µA`

- Zakres pomiarowy: maks. :math:`7 m`

- Kąt widzenia: do :math:`100 °`

- Wyjście cyfrowe: 
		
	- Stan wysoki - obiekt wykryty

	- Stan niski - brak obiektu

- Wymiary modułu: 32.5 mm x 24.5 mm

*Opis:*

Czujnik typu PIR (`wiki <http://en.wikipedia.org/wiki/Passive_infrared_sensor>`_) pozwala na wykrywanie ruchu. Wykorzystywany jest do wykrywania obecności człowieka w pomieszczeniach w systemach alarmowych i oświetleniowych. Sensor zasilany jest napięciem z zakresu od :math:`4.5 V` do :math:`20 V`, posiada zasięg do :math:`7 m`. Wykrycie obiektu sygnalizowane jest stanem wysokim. 

Cyfrowe wyjście umożliwia ﻿połączenie ﻿czujnika z dowolnym zestawem uruchomieniowym np. Arduino, STM32Discovery lub minikomputerem Raspberry Pi. 

Wyprowadzeniami są złącza goldpin (raster :math:`2.45 mm`) umożliwiające podłączenie sensora za pomocą ﻿przewodów. ﻿

*Sposób użycia:*

Zasilanie (od :math:`4.5 V` do :math:`20 V`) należy podłączyć ﻿do zewnętrznych wyprowadzeń oznaczonych odpowiednio symbolem VIN i GND. Wykrycie obiektu w polu widzenia czujnika sygnalizowane jest stanem wysokim, pojawiającym się na wyprowadzeniu OUT. 

*Dzięki potencjometrom ﻿użytkownik może regulować:*

- T1 - czas trwania stanu wysokiego po wykryciu obiektu 

- T2 - długość przerwy w pomiarach po zakończeniu ﻿występowania stanu wysokiego

*Za pomocą zworki wybierany jest tryb pracy z pośród dwóch dostępnych:*

- non-retriggering (zworka w pozycji L) - wyjście osiąga stan wysoki tylko raz po wykryciu obiektu, następnie przechodzi w stan niski niezależnie od tego, czy ruch dalej występuje

- retriggering (zworka w pozycji H)﻿ - wyjście osiąga stan wysoki po wykryciu obiektu i jest on utrzymywany przez cały czas wykrywania trwającego ruchu

.. figure:: czujnik-ruchu.jpg
   :align: center

Czujniki odbiciowe
------------------

**Czujnik transoptor odbiciowy CNY70:**

Transoptor (`wiki <http://en.wikipedia.org/wiki/Opto_isolator>`_) odbiciowy, stosowany np. do odróżniania krawędzi lub wykrywania linii. Wymiary obudowy to 7 mm x 7 mm x 6 mm, montaż przewlekany.

*Specyfikacja:*

- Napięcie zasilania diody: :math:`5 V`

- Maksymalny prąd diody: :math:`50 mA`

- Maksymalne napięcie kolektor-emiter: :math:`32 V`

- Maksymalny prąd kolektora: :math:`50 mA`

*Opis:*

Czujnik wysyła wiązkę promieniowania poprzez nadajnik podczerwieni, a następnie za pomocą fototranzystora mierzy natężenie światła odbitego. Wyjściem jest sygnał napięciowy, zależny od natężenia światła padającego na ten detektor. Im więcej światła się odbije i dotrze do fotodetektora, tym napięcie na wyjściu będzie miało wyższą wartość. Jako że promieniowanie świetlne lepiej odbija powierzchnia jasna (a ciemna pochłania), napięcie będzie wyższe na białym materiale.﻿

.. image:: czkoloru.jpg
   :width: 600px
   :align: center

*Zastosowanie:*

Czujniki są wykorzystywane przez konstruktorów robotów Line Follower (`wiki <http://en.wikipedia.org/wiki/Mobile_robot>`_) do detekcji linii oraz w konstrukcjach minisumo, gdzie służą do wykrywania krawędzi ringu. Jako że w tych przypadkach wykrywane są wartości skrajne (odróżnianie czarnego od białego - wartości pośrednie nie są istotne), czujnik może znajdować się wyżej nad powierzchnią niż wskazuje dokumentacja. 

W przemyśle układy można wykorzystać np. do detekcji krawędzi lub wykrywaniu obiektów z bliskiej odległości. 

Czujnik posiada łatwą w montażu obudowę przewlekaną. Dodatkowo zamontowano otoczkę ochroną, która nie pozwala na całkowite dociśnięcie detektora i nadajnika do podłoża. 

.. figure:: odbiciowy.png
   :width: 600px
   :align: center

*Przykład podłączenia:*

Czujnik składa się z dwóch głównych części: detektora w postaci fototranzystora oraz nadajnika, którym jest dioda podczerwona. Aby nadajnik nie uległ zniszczeniu należy ograniczyć jego prąd (maks. :math:`50 mA`), a co za tym idzie moc promieniowania podczerwonego. Wykonuje się to stosując rezystor włączony szeregowo (R3). Dla poprawnego działania fototranzystora niezbędny jest rezystor podwyższający. Odpowiednie wartości należy dobrać posługując się dokumentacją. 

.. figure:: czodbiciowy.jpg
   :width: 600px
   :align: center

Szczegóły w `dokumentacji <botland.com.pl/attachment.php?id_attachment=8>`_

Czujniki nacisku
----------------

Czujniki ugięcia
^^^^^^^^^^^^^^^^

**Czujnik ugięcia 55 mm x 6.3 mm - SparkFun:**

*Specyfikacja:*

- Długość całkowita: :math:`73.66 mm`

- Długość użyteczna czujnika: :math:`55.37 mm`

- Szerokość: :math:`6.35 mm`

.. figure:: ugiecia.jpg
   :align: center

*Opis:*

Podczas zaginania, czujnik zwieksza swoją rezystancję. Wyprowadzenia mają popularny raster :math:`2,54 mm` (:math:`0.1"`), dzięki czemu czujnik można wpiąć w płytkę stykową bądź połączyć przy pomocy przewodów. ﻿

*Zastosowanie:*

Może zostać użyty do wykrywania ruchów dłoni np. zaciskania pięści. Czujniki tego typu są wykorzystywane w interaktywnych rękawicach, służących do sterowania robotami, np. w Nintendo Power Glove (`wiki <http://en.wikipedia.org/wiki/Power_Glove>`_)﻿.

*Uwaga:*

Nie należy zginać czujnika w części, gdzie nie występują metalowe blaszki. Użyteczna część czujnika może być zaginana w dopuszczalnym zakresie. 

Szczegóły w `dokumentacji <botland.com.pl/attachment.php?id_attachment=367>`_


Czujniki siły nacisku
^^^^^^^^^^^^^^^^^^^^^

**Czujnik siły nacisku okrągły 5mm (0.2"):**
	
*Specyfikacja:*

- Wymiary zewnętrzne: 7.6 mm x 7.6 mm x 0.4 mm﻿

- Masa: 0.15 g

*Opis:*

Czujnik siły zmniejsza swoją rezystancje, gdy siła przyłożona do okrągłej końcówki narasta. Dzięki temu zjawisku oraz wykorzystaniu mikrokontrolera z przetwornikiem analogowo-cyfrowym, można skonstruować czujnik mierzący siłę nacisku. Pomiar może być wyświetlany np. na wyświetlaczu LCD.

Przy braku działania siły na sensor, rezystancja wynosi około :math:`1 MΩ`. Podczas przykładania palca z różną siłą miernik wskazywał od :math:`100 kΩ` do kilkuset :math:`Ω`.

Szczegóły w `dokumentacji <botland.com.pl/attachment.php?id_attachment=116>`_

Czujniki koloru
---------------

**Czujnik koloru TCS3200D:**

Czujnik, przetwarzający natężenie światła wybranego koloru na mierzalną częstotliwość (np. poprzez zastosowanie mikrokontrolera).

.. figure:: koloru.jpg
   :align: center

*Specyfikacja:*

- Napięcie zasilania: :math:`2.7 V - 5.5 V`

- Programowalny wybór koloru

- Błąd nieliniowości na poziome :math:`0.2%` przy :math:`50 kHz`

- Prosta komunikacja z mikrokontrolerem (odczyt częstotliwości)

.. figure:: czkoloru.jpg
   :width: 600px
   :align: center

Szczegóły w `dokumentacji <botland.com.pl/attachment.php?id_attachment=185>`_

Czujniki gazu
-------------

**Czujnik tlenku węgla MQ-7:**

Czujnik tlenku węgla z wyjściem analogowym.

.. figure:: co3.jpg
   :width: 600px
   :align: center

*Specyfikacja:*

- Zasilanie: :math:`5 V`

- Pobór prądu: :math:`150 mA`

- Zakres pomiarowy: :math:`10 ppm` do :math:`10^{4} ppm`

- Temperatura pracy: od :math:`-10 °C` do :math:`50 °C`

.. figure:: co.png
   :align: center

*Opis:*

Czujnik wykrywa stężenie CO w powietrzu. Wynik można uzyskać z pomiaru napięcia na wyjściu analogowym. Dzięki temu urządzeniu można stworzyć system ostrzegania przed bardzo niebezpiecznym gazem, jakim jest tlenek węgla. Do obsługi sensora można wykorzystać np. moduł Arduino bądź płytkę z rodziny STM32 Discovery.﻿

.. figure:: co2.png
   :width: 600px
   :align: center

Szczegóły w `dokumentacji <botland.com.pl/attachment.php?id_attachment=40>`_

Czujniki ciśnienia
------------------

**Cyfrowy barometr MPL115A2 - 115 kPa:**

Cyfrowy czujnik ciśnienia firmy Freescale. Obudowa LGA.

*Specyfikacja:*

- Zakres pomiarowy: :math:`50 kPa - 115 kPa`

- Napięcie zasilania: :math:`2.375 V - 5.5 V`

- Komunikacja: I2C

- Wbudowany czujnik temperatury

- Obudowa: LGA

.. figure:: barometr.png
   :width: 600px
   :align: center

*Przykłady zastosowania:*

- Rozbudowane nawigacje GPS

- Urządzenia dla sportowców

- Stacje pogodowe

Szczegóły w `dokumentacji <botland.com.pl/attachment.php?id_attachment=159>`_

Magnetometry
------------

*Magnetometr* – przyrząd do pomiaru wielkości, kierunku oraz zmian pola magnetycznego.


**Magnetometr 3-osiowy, cyfrowy MAG3110:**

3-osiowy magnetometr w małej obudowie DFN. Zakres pomiarowy: :math:`± 1000 µT`. Czułość na poziomie :math:`0.1 µT`. Interfejs komunikacyjny to magistrala I2C.

.. figure:: magnetometr.png
   :width: 600px
   :align: center
	
*Specyfikacja:*

- Zasilanie: :math:`1.95 V - 3.6 V`

- 3-osie: XYZ

- Zakres pomiarowy: :math:`± 1000 µT`

- Czułość: :math:`0.1 µT`

- Interfejs komunikacyjny: I2C (Fast mode :math:`400 kHz`)

- Tryb niskiego poboru prądu

- Obudowa: DFN 10-pin (2 mm x 2 mm x 0.85 mm)

Do poprawanego działania układu niezbędne są kondensatory filtrujące oraz rezystory podwyższające linie magistrali I2C.

.. figure:: magnetometr.jpg
   :width: 600px
   :align: center

Szczegóły w `dokumentacji <botland.com.pl/attachment.php?id_attachment=164>`_


Akcelerometry
-------------

*Przyspieszeniomierz, akcelerometr, akceleromierz, przetwornik przyspieszenia* – przyrząd do pomiaru przyspieszeń liniowych lub kątowych. Przyspieszeniomierz, w przeciwieństwie do urządzeń bazujących na teledetekcji, mierzy własny ruch.

**Akcelerometr 3-osiowy, cyfrowy LIS35DE:**

.. figure:: akcelerometr.png
   :align: center

*Specyfikacja:*

- Zasilanie: :math:`2.16 V - 3.6 V`

- 3-osie: XYZ

- Zakres pomiarowy: :math:`±2 g/±8 g`

- Możliwość programowego generowania przerwań

- Interfejs komunikacyjny: I2C / SPI

- Tryb niskiego poboru prądu

- Obudowa: LGA 14 (3 mm x 5 mm x 0.9 mm)

.. figure:: akcelerometr2.png
   :width: 600px
   :align: center

*Zastosowanie:*

Układy tego typu wykorzystywane są między innymi w kontrolerach gier, interaktywnych interfejsach czy smartfonach.

.. figure:: akcelerometr3.png
   :width: 600px
   :align: center

Szczegóły w `dokumentacji <botland.com.pl/attachment.php?id_attachment=166>`_



.. _BOTLAND: http://botland.com.pl/
.. _GSM.h: http://arduino.cc/en/Reference/GSM
.. _HttpClient.h: https://github.com/amcewen/HttpClient
.. _Xively.h: https://github.com/xively/xively_arduino
.. _OneWire.h: http://www.pjrc.com/teensy/td_libs_OneWire.html
.. _Temperature.h: https://github.com/comoyo/BeachSensor/tree/master/Temperature
.. _zespół M2M: http://comoyo.github.io/blog/2013/08/01/m2m_adventures/
.. _Buildr example: http://bildr.org/2011/07/ds18b20-arduino/
.. _autora: http://milesburton.com/
.. _Xively: https://xively.com/
.. _Źródło.: http://tomczak.org.pl/
.. _GitHubie: http://comoyo.github.io/blog/2013/08/01/m2m_adventures/
