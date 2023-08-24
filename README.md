Selenium библиотека подключение к JAVA

Нам понадобятся:
установленная среда разработки Intellij IDEA.
установленные Java (jdk/openjdk) и Maven, прописанные в системные окружения ОС.
браузер Chrome и chromedriver — программа для передачи команд браузеру.

Создание проекта:
Запустим Intellij IDEA, —  выберем параметры по умолчанию.
В последнем шаге в окне выберем пункт "Create New Project", в нем тип проекта Maven. 
Maven — это инструмент сборки Java проектов.
Project SDK — версия Java, которая установлена на компьютере.
Create from archetype — это возможность создавать проект с определенным архетипом (на данном этапе данный чекбокс отмечать не нужно).
Нажмем Next =>

Groupid и Artifactid — идентификаторы проекта в Maven. Существуют определенные правила заполнения этих пунктов:
Groupid — название организации или подразделения занимающихся разработкой проекта. 
В этом пункте действует тоже правило как и в именовании пакетов Java: доменное имя организации записанное задом наперед. Если у Вас нет своего доменного имени, то можно использовать свой э-мейл, например com.email.email.
Artifactid — название проекта.
Version — версия проекта.
Нажмем Finish => IDE автоматически откроет файл pom.xml:

Pom.xml — это файл который описывает проект. 
В нем уже появилась информация о проекте, внесенная на предыдущем шаге: 
Groupid, Artefiactid, Version.
Pom-файл хранит список всех библиотек (зависимостей), которые используются в проекте.

Для этого автотеста необходимо добавить две библиотеки: Selenium Java и Junit. 
Перейдем на центральный репозиторий Maven mvnrepository.com, вобьем в строку поиска Selenium Java и зайдем в раздел библиотеки:
Выберем нужную версию (в примере будет использована версия 4.9.0). Откроется страница:

Копируем содержимое блока «Maven» и вставим в файл pom.xml в блок

<dependency>
       <groupId>org.seleniumhq.selenium</groupId>
       <artifactId>selenium-java</artifactId>
       <version>4.9.0</version>
</dependency>

Таким образом библиотека будет включена в проект и ее можно будет использовать. 

Аналогично сделаем с библиотекой Junit (будем использовать версию 4.13.2).

<dependency>
       <groupId>junit</groupId>
       <artifactId>junit</artifactId>
       <version>4.13.2</version>
       <scope>test</scope>
</dependency>

Итоговый pom-файл:

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <repositories>
        <repository>
            <id>my-repo</id>
            <name>https://mvnrepository.com</name>
            <url>https://mvnrepository.com</url>
        </repository>
    </repositories>

    <groupId>org.example</groupId>
    <artifactId>TestJU1</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>

        <dependency>
            <groupId>org.seleniumhq.selenium</groupId>
            <artifactId>selenium-java</artifactId>
            <version>4.9.0</version>
        </dependency>

        <dependency>
            <groupId>commons-io</groupId>
            <artifactId>commons-io</artifactId>
            <version>2.6</version>
        </dependency>
    </dependencies>

    <properties>
        <maven.compiler.source>19</maven.compiler.source>
        <maven.compiler.target>19</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

</project>


Создание пакета и класса

Раскроем структуру проекта. 
Директория src содержит в себе две директории: «main» и «test». 
Для тестов используется, соответственно, директория «test». 
Откроем директорию «test», кликом правой клавиши мыши по директории «java» выберем пункт «New», а затем пункт «Package». 
В открывшемся диалоговом окне необходимо ввести название пакета. 
Имя базового пакета должно носить тоже имя, что и Groupid — «org.example».

Следующий шаг — создание класса Java, в котором пишется код автотеста.
Кликом правой клавиши мыши по названию пакета выберем пункт «New», а затем пункт «Java Class».
В открывшемся диалоговом окне необходимо ввести имя Java класса, например, TestIvi (название класса в Java всегда должно начинаться с большой буквы). В IDE откроется окно тестового класса:


Настройка IDE

Версия драйвера и версия selenium должны быть корректны
https://sites.google.com/chromium.org/driver/?pli=1
браузер откроется если selenium нашел драйвер на компьютере
В корневой директории создать new Directory => drivers => положить в нее драйвер браузера
Этот фаил нужно указать в системном свойстве System.setProperty("chromedriver", "drivers"); далее в тестовом окружении
