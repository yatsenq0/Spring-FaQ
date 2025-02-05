## Практическое задание: создание REST-сервиса

В этом практическом задании мы создадим простой RESTful сервис на Spring Boot, который будет реализовывать операции CRUD (Create, Read, Update, Delete) для управления сущностью "Клиент". Мы пройдем через все этапы создания проекта, настройки и тестирования.

### 1. Создание проекта

#### 1.1. Использование Spring Initializr

Для начала создайте новый проект с помощью [Spring Initializr](https://start.spring.io/):

1. Выберите тип проекта **Maven**.
2. Укажите Group (например, `com.example`) и Artifact (например, `client-service`).
3. Выберите версию Spring Boot.
4. Добавьте зависимость **Spring Web**.
5. Нажмите **Generate** для скачивания ZIP-архива с проектом.

#### 1.2. Импорт проекта в IDE

Распакуйте загруженный архив и импортируйте проект в вашу IDE (например, IntelliJ IDEA или Eclipse).

### 2. Настройка структуры проекта

После импорта проекта структура должна выглядеть следующим образом:

```
client-service
|-- src
|   |-- main
|   |   |-- java
|   |   |   `-- com
|   |   |       `-- example
|   |   |           `-- clients
|   |   |               |-- Client.java
|   |   |               |-- ClientController.java
|   |   |               `-- ClientService.java
|   |   `-- resources
|   |       `-- application.properties
|-- pom.xml
```

### 3. Создание сущности "Клиент"

Создайте класс `Client` в пакете `com.example.clients`:

```java
package com.example.clients;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class Client {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String email;
    private String phone;

    // Геттеры и сеттеры
}
```

### 4. Создание репозитория

Создайте интерфейс репозитория для доступа к данным:

```java
package com.example.clients;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface ClientRepository extends JpaRepository<Client, Long> {
}
```

### 5. Создание сервиса

Создайте сервисный класс для обработки бизнес-логики:

```java
package com.example.clients;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class ClientService {

    private final ClientRepository clientRepository;

    @Autowired
    public ClientService(ClientRepository clientRepository) {
        this.clientRepository = clientRepository;
    }

    public List<Client> findAll() {
        return clientRepository.findAll();
    }

    public Client save(Client client) {
        return clientRepository.save(client);
    }

    public void deleteById(Long id) {
        clientRepository.deleteById(id);
    }
}
```

### 6. Создание контроллера

Создайте контроллер для обработки HTTP-запросов:

```java
package com.example.clients;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/clients")
public class ClientController {

    private final ClientService clientService;

    @Autowired
    public ClientController(ClientService clientService) {
        this.clientService = clientService;
    }

    @GetMapping
    public List<Client> getAllClients() {
        return clientService.findAll();
    }

    @PostMapping
    public ResponseEntity<Client> createClient(@RequestBody Client client) {
        Client savedClient = clientService.save(client);
        return new ResponseEntity<>(savedClient, HttpStatus.CREATED);
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteClient(@PathVariable Long id) {
        clientService.deleteById(id);
        return new ResponseEntity<>(HttpStatus.NO_CONTENT);
    }
}
```

### 7. Настройка базы данных

Добавьте настройки подключения к базе данных в файл `application.properties`. Например, для H2 базы данных:

```properties
spring.datasource.url=jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.h2.console.enabled=true
spring.jpa.hibernate.ddl-auto=update
```

### 8. Запуск приложения

Чтобы запустить приложение, выполните команду:

```bash
mvn spring-boot:run
```

Теперь ваше приложение будет доступно по адресу `http://localhost:8080/clients`.

### 9. Тестирование REST-сервиса

Для тестирования вашего RESTful сервиса используйте Postman или другой инструмент для отправки HTTP-запросов.

#### 9.1. Проверка GET запроса

Отправьте GET запрос на адрес:

```
http://localhost:8080/clients
```

#### 9.2. Проверка POST запроса

Отправьте POST запрос на тот же адрес с телом запроса в формате JSON:

```json
{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "phone": "+123456789"
}
```

#### 9.3. Проверка DELETE запроса

Для удаления клиента выполните DELETE запрос по адресу:

```
http://localhost:8080/clients/{id}
```

Замените `{id}` на идентификатор клиента.

### 10. Заключение

В этом практическом задании мы создали простой RESTful сервис на Spring Boot, который реализует CRUD операции для управления клиентами. Теперь вы обладаете базовыми знаниями о том, как разрабатывать RESTful API с использованием Spring Boot.

### 11. Рекомендации по дальнейшему изучению

- Изучите возможности Spring Security для защиты вашего API.
- Ознакомьтесь с документацией по Swagger для автоматической генерации документации вашего API.
- Попробуйте реализовать пагинацию и фильтрацию в вашем API.
- Исследуйте возможности тестирования RESTful сервисов с использованием JUnit и Mockito.

Следуя этим рекомендациям, вы сможете углубить свои знания о создании RESTful сервисов на Spring Boot и улучшить свои навыки разработки Java-приложений, что приведет к более эффективному созданию качественного программного обеспечения.

Citations:
[1] https://javarush.com/groups/posts/2488-obzor-rest-chastjh-3-sozdanie-restful-servisa-na-spring-boot
[2] https://sysout.ru/spring-boot-rest-api/
[3] https://habr.com/ru/articles/435144/
[4] https://habr.com/ru/articles/343364/
[5] https://devmark.ru/article/spring-boot-resful-service
[6] https://ru.hexlet.io/courses/java-spring-boot/lessons/rest-api/theory_unit
[7] https://amplicode.ru/blog/sozdaem-crud-rest-api-v-spring-boot/

---
Answer from Perplexity: https://www.perplexity.ai/search/glava-iz-300-strok-chto-takoe-9WcTmuznQ.6R5kqMKVn1ng?utm_source=copy_output
