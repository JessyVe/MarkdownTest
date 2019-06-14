# Lab Report - Vertiefende Gesamtwiederholung
> Abgabe 04
> Laura Gröttrup | Jessica Veit
>Repository: [https://github.com/LauraGroettrup/19-Abgabe04-Groettrup-Veit.git](https://github.com/LauraGroettrup/19-Abgabe04-Groettrup-Veit.git)
 
 

## VORGEHEN
### Vorbereitung 
-   Übertragen Angabe Taskliste in das Readme des Repositories (unter Verwendung von Markdown)
-   Einspielen des Queue Vorlageprojekts aus dem Repository:  
[https://github.com/michaelulm/software-configuration-management/tree/master/test-automation/Queue](https://github.com/michaelulm/software-configuration-management/tree/master/test-automation/Queue)


## Entwicklung und Konfiguration
#### Debugging des bestehenden Codes

Folgende Fehler wurden gefunden und behoben: 
 - bla bla
 - bla
---
#### Implementation der JUnit Tests
Im gegenständlichen Projekt befindet sich eine Test Klasse `StringQueueTest.cs`, welche die Funktionalitäten der Klasse `StringQueue.cs` auf ihre richtige Ausführung überprüft.  

In der `pom.xml` muss die Abhängigkeit zur JUnit Library für den Build Prozess definiert werden, diese geschieht über den Tag `<dependency>`: 
```xml
<dependencies>
	<!-- junit Dependencies -->
	<dependency>
		<groupId>junit</groupId>
		<artifactId>junit</artifactId>
		<version>4.12</version>
		<scope>test</scope>
	</dependency>	
	...
	
</dependencies>
```

![Screenshot - Manuell erstellte Maven Site](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png)

---
#### JavaDoc 
Jede Methode und Klasse wurde mit einem JavaDoc-Kommentar versehen, um anschließend um Maven Build Prozess eine API Dokumentation generieren zu lassen. 

Ein solches Kommentar hat grundlegend folgende Form: 
```Java
/**
 * This is a textual descritpion of the purpose/function 
 * of a method or class. 
 * 
 * Also block tags can be used: 
 * @author		name of the author of the class
 * @param 		defines parameter for calling the method
 * @return		defines the value which will be return by the method
 */
```
---
#### Log4j (Version 2) 
In jeder Methode des gegenständlichen **Queue** Projektes wurden Loggging-Messages implementiert um später den Workflow der Application über den die Log-Dateien nachvollziehen zu können. 

Eine solche Implementation sieht wie folgt aus: 
```java
 // Needed imports
 import org.apache.logging.log4j.LogManager;
 import org.apache.logging.log4j.Logger;
 ...
 
 // Create and initialize logging object
 private static final Logger LOG = LogManager.getLogger(StringQueue.class);
 ...
 
 // Create logging messages
 LOG.info("This is a informational log-message. ");
 LOG.error("This is a log-message documenting an error.");
```
Auch für Maven muss die Abhängigkeit zur Log4j Library bekannt gemacht werden. Zu diesem Zweck wird in die `pom.xml` um diese Dependency folgendermaßen ergänzt: 
```xml
<dependencies>
	<!-- Log4j Dependencies -->
	<dependency>
		<groupId>org.apache.logging.log4j</groupId>
		<artifactId>log4j-api</artifactId>
		<version>2.11.1</version>
	</dependency>
	...
</dependencies>
```
Weiters kann Log4J auf die Bedürfnisse des jeweiligen Projektes über eine `log4j2-test.properties` angepasst werden. 


---
### Maven Sites 
Anpassung im `pom.xml` des Projektes, damit die Dokumentation generiert werden kann:
```xml
	<build>
     <plugins>
	      ...
		 <plugin>
		     <groupId>org.apache.maven.plugins</groupId>
		     <artifactId>maven-site-plugin</artifactId>
		     <version>3.7.1</version>
		 </plugin>
	 </plugins>
    </build>
```
Durch die Ausführung des Befehls `mvn site` in der, im project-root geöffnten Kommandozeileneingabe, wird die API Dokumentation im Ordner `..\target\site` erstellt. Die Hauptseite ist definiert als `index.html`. 

<b>Manuelle Erstellung einer Seite</b>
Um eine auch manuell erstellte Seiten in die Dokumentation zu integrieren, muss der `src` um den folgende interne Struktur ergänzt werden: 

```
src 
│
└─── site
│   └─── apt
│       │   index.apt
│   
...
```
Hierbei kann die `index.apt` einen beliebigen Text beinhalten, welcher in **Markdown** verfasst sein sollte. 
> Im gegenständlichen Projekt wurde die Funktionsweise einer **Queue** in der Informatik beschrieben. 

Die manuell erstellte Seite ist auf der Hauptseite über den Menüpunkt **About** aufrufbar:


![Screenshot - Manuell erstellte Maven Site](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png)

## Github Flavor
> **Übung Github Flavor**: Erstellen Sie einen Codeblock im Dokument, welcher 3 Zeilen Python und 3 Zeilen Java Source Code korrekt darstellt.

```python 
# Python: Fibonacci series up to n
>>> def fib(n):
>>>     a, b = 0, 1
>>>     while a < n:
>>>         print(a, end=' ')
>>>         a, b = b, a+b
>>>     print()
>>> fib(1000)
```    

```java
// Java: Fibonacci series 
    private int fib(int i) {
        if (i <= 0) {
            return 0;
        } else if (i == 1) {
            return 1;
        } else {
            return fib(i - 2) + fib(i - 1);
        }
    }
```    


## LINKS / LITERATUR
### Maven Sites (manual creation of sites and content)
- [https://maven.apache.org/plugins/maven-site-plugin/examples/creating-content.html](https://maven.apache.org/plugins/maven-site-plugin/examples/creating-content.html)
- [https://maven.apache.org/doxia/references/apt-format.html](https://maven.apache.org/doxia/references/apt-format.html)
### Markup Tutorials, Tips and Editors
- [https://stackedit.io](https://stackedit.io/)
- [https://www.markdownguide.org/getting-started](https://www.markdownguide.org/getting-started)
- [https://en.support.wordpress.com/markdown-quick-reference/](https://en.support.wordpress.com/markdown-quick-reference/)
- [https://support.codebasehq.com/articles/tips-tricks/syntax-highlighting-in-markdown](https://support.codebasehq.com/articles/tips-tricks/syntax-highlighting-in-markdown)