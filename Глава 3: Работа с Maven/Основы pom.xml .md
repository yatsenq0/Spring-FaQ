## Основы pom.xml

Файл `pom.xml` (Project Object Model) является основным конфигурационным файлом в проектах, использующих Apache Maven. Он описывает структуру проекта, его зависимости, плагины и другие настройки, необходимые для сборки и управления проектом. В этой главе мы рассмотрим основные элементы и структуру файла `pom.xml`.

### Структура pom.xml

1. **Корневой элемент `<project>`**: 
   - Это основной элемент, который содержит всю информацию о проекте.
   - Внутри этого элемента указываются все остальные настройки.

   Пример:
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <project xmlns="http://maven.apache.org/POM/4.0.0"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
   ```

2. **Координаты проекта**:
   - **`<groupId>`**: Уникальный идентификатор группы (например, `com.example`).
   - **`<artifactId>`**: Уникальный идентификатор артефакта (например, `my-app`).
   - **`<version>`**: Версия проекта (например, `1.0-SNAPSHOT`).

   Пример:
   ```xml
   <groupId>com.example</groupId>
   <artifactId>my-app</artifactId>
   <version>1.0-SNAPSHOT</version>
   ```

3. **Тип упаковки**:
   - Указывает, как будет упакован проект (например, `jar`, `war`, `pom`).

   Пример:
   ```xml
   <packaging>jar</packaging>
   ```

4. **Зависимости**:
   - Определяет библиотеки и компоненты, необходимые для работы проекта.
   - Каждая зависимость описывается с помощью элементов `<dependency>`.

   Пример:
   ```xml
   <dependencies>
       <dependency>
           <groupId>org.springframework</groupId>
           <artifactId>spring-core</artifactId>
           <version>5.3.10</version>
       </dependency>
       <dependency>
           <groupId>junit</groupId>
           <artifactId>junit</artifactId>
           <version>4.13.2</version>
           <scope>test</scope>
       </dependency>
   </dependencies>
   ```

5. **Плагины**:
   - Позволяют добавлять функциональность к Maven, например, компиляцию кода или упаковку артефактов.
   - Указываются внутри элемента `<build>`.

   Пример:
   ```xml
   <build>
       <plugins>
           <plugin>
               <groupId>org.apache.maven.plugins</groupId>
               <artifactId>maven-compiler-plugin</artifactId>
               <version>3.8.1</version>
               <configuration>
                   <source>1.8</source>
                   <target>1.8</target>
               </configuration>
           </plugin>
       </plugins>
   </build>
   ```

6. **Профили**:
   - Позволяют создавать различные конфигурации для разных сред (например, разработка, тестирование, продакшен).
   
   Пример:
   ```xml
   <profiles>
       <profile>
           <id>dev</id>
           <properties>
               <database.url>jdbc:h2:mem:testdb</database.url>
           </properties>
       </profile>
       <profile>
           <id>prod</id>
           <properties>
               <database.url>jdbc:mysql://prod-db:3306/mydb</database.url>
           </properties>
       </profile>
   </profiles>
   ```

### Заключение

Файл `pom.xml` является центральным элементом в проектах на Maven, который описывает все аспекты проекта — от его координат до зависимостей и плагинов. Понимание структуры и основных элементов `pom.xml` позволяет эффективно управлять проектами и использовать возможности Maven для автоматизации сборки и управления зависимостями.

Citations:
[1] https://www.examclouds.com/ru/java/java-core-russian/pom-xml
[2] https://proselyte.net/tutorials/maven/pom/
[3] https://skillbox.ru/media/code/osnovy-maven-chto-eto-takoe-i-kak-rabotaet/
[4] https://javarush.com/quests/lectures/questservlets.level01.lecture01
[5] https://topjava.ru/blog/apache-maven-osnovy-1
[6] https://javarush.com/groups/posts/2523-chastjh-4osnovih-maven
[7] https://habr.com/ru/articles/77382/
[8] https://evmservice.ru/blog/apache-maven/

---
Answer from Perplexity: https://www.perplexity.ai/search/glava-iz-300-strok-chto-takoe-9WcTmuznQ.6R5kqMKVn1ng?utm_source=copy_output
