**Fibonacci-MLP vs Standard-MLP auf MNIST**



Dieser Code ist im Kurs Machine Learning, 2026 (Uni Regensburg) entstanden.

Es ist schlicht ein mehrschichtiges Perzeptron in NumPy implementiert.



Ausgangsfrage war, ob es etwas bringt, die Breite der Hidden Layers nach der Fibonacci-Folge zu wählen, statt sie wie üblich pro Schicht zu halbieren.



Daraus entstanden dann folgende Forschungsfragen:

1\. Ist ein Fibonacci-MLP bei gleicher Parameterzahl genauer als ein Standard-MLP?

2\. Erreicht ein kleineres Fibonacci-MLP eine vergleichbare Genauigkeit mit weniger Parametern?



**Aufbau:**

\- Daten: MNIST auf \[0,1] normalisiert, 80/20 Split

\- Training: 20 Epochen, Lernrate 0,1, Batchgröße 32, ReLu, Softmax, Kreuzentropie

\- Wiederholungen: 3 Seeds pro Konfiguration, berichtet als Mittelwert ± Standardabweichung

\- Tiefe: K=2,3,4 Hidden Layers



**Architekturen:**

\- standard: Breite halbiert sich ab 128

\- fib\_match: Fibonacci-Proportionen (absteigend), aber so skaliert, dass die Parameterzahl der von der standard Architektur möglichst nahe kommmt

\- fib\_small: Fibonacci-Proportionen mit festem Skalierungsfakor 4



**Ergebnisse:**



|K|Architektur|Parameter|Accuracy (± SD)|
|-|-|-|-|
|2|standard|109.386|0.9797 ± 0.0003|
|2|fib\_match|108.895|0.9806 ± 0.0008|
|2|fib\_small|3.210|0.8291 ± 0.0252|
|3|standard|111.146|0.9751 ± 0.0039|
|3 |fib\_match|111.583|0.9791 ± 0.0010|
|3|fib\_small|6.386|0.8870 ± 0.0053|
|4|standard|111.514|0.9762 ± 0.0019|
|4|fib\_match|112.268|0.9752 ± 0.0017|
|4|fib\_small|9.630|0.9281 ± 0.0025|



**Interpretation**



Zu Frage 1: bei gleicher Parameterzahl sieht man keinen durchgängigen Vorteil. Bei K = 2 und K = 3 liegt fib\_match leicht vorn, bei K = 4 leicht hinten.



Zu Frage 2: fib\_small bleibt deutlich hinter den anderen Netzen zurück, obwohl die Genauigkeit mit K stark ansteigt.



**Limitationen**



Dieser Test ist aus persönlichem Interesse heraus entstanden und lädt natürlich noch für einige Verbesserungen und Anpassungen ein. Man könnte als nächste Schritte in Betracht ziehen, schwerere Datensätze, ein kleines Standard-Netz mit derselben Parameterzahl wie fib\_small als Kontrollgruppe, ein größeres K oder mehr Seeds und einen einfachen Signifikanztest zu nutzen.

