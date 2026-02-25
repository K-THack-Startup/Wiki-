## Админ-панель

Базовый URL: `http://localhost:8081/api/admin`

### **1. Управление хакатонами**

#### **1.1 Получить все хакатоны**

**GET** `/events`

**Ответ:**
\[
{
"id": 1,
"title": "Spring Hackathon 2026",
"description": "Ежегодный хакатон по Spring Boot",
"techStack": "Java, Spring Boot, PostgreSQL",
"eventCard": "https://example.com/card.jpg",
"startDate": "2026-03-15T10:00:00",
"endDate": "2026-03-17T18:00:00",
"location": "Москва, Технопарк",
"maxParticipants": 100
}
]

#### **1.2 Получить хакатон по ID**

**GET** `/events/{id}`

**Ответ:**
{
"id": 1,
"title": "Spring Hackathon 2026",
"description": "Ежегодный хакатон по Spring Boot",
"techStack": "Java, Spring Boot, PostgreSQL",
"eventCard": "https://example.com/card.jpg",
"startDate": "2026-03-15T10:00:00",
"endDate": "2026-03-17T18:00:00",
"location": "Москва, Технопарк",
"maxParticipants": 100
}

#### **1.3 Создать хакатон**

**POST** `/events`

**Content-Type:** `application/json`

**Тело запроса:**
{
"title": "Spring Hackathon 2026",
"description": "Ежегодный хакатон по Spring Boot",
"techStack": "Java, Spring Boot, PostgreSQL",
"eventCard": "https://example.com/card.jpg",
"startDate": "2026-03-15T10:00:00",
"endDate": "2026-03-17T18:00:00",
"location": "Москва, Технопарк",
"maxParticipants": 100
}

**Ответ:** созданный хакатон (как в п.1.2)



#### **1.4 Обновить хакатон**

**PUT** `/events/{id}`

**Content-Type:** `application/json`

**Тело запроса:** (те же поля, что и при создании)

**Ответ:** обновленный хакатон



#### **1.5 Удалить хакатон**

**DELETE** `/events/{id}`

**Ответ:**
{
"message": "Хакатон успешно удален",
"status": "success"
}



#### **1.6 Получить предстоящие хакатоны**

**GET** `/events/upcoming`

**Ответ:** массив предстоящих хакатонов (сортировка по дате)



### **2. Управление пользователями**

#### **2.1 Получить всех пользователей**

**GET** `/users`

**Ответ:**
\[
{
"id": "user123",
"email": "ivan@example.com",
"firstName": "Иван",
"lastName": "Петров",
"phone": "+79991234567",
"city": "Москва",
"profileImage": "https://example.com/avatar.jpg",
"bio": "Java-разработчик",
"techStack": "Java, Spring, PostgreSQL",
"github": "https://github.com/ivan",
"linkedin": "https://linkedin.com/in/ivan",
"isActive": true
}
]



#### **2.2 Получить пользователя по ID**

**GET** `/users/{id}`

**Ответ:** объект пользователя (как в п.2.1)



#### **2.3 Обновить пользователя**

**PUT** `/users/{id}`

**Content-Type:** `application/json`

**Тело запроса:**
{
"email": "ivan@example.com",
"firstName": "Иван",
"lastName": "Петров",
"phone": "+79991234567",
"city": "Москва",
"profileImage": "https://example.com/avatar.jpg",
"bio": "Java-разработчик",
"techStack": "Java, Spring, PostgreSQL",
"github": "https://github.com/ivan",
"linkedin": "https://linkedin.com/in/ivan",
"isActive": true
}

**Ответ:** обновленный пользователь



#### **2.4 Удалить пользователя**

**DELETE** `/users/{id}`

**Ответ:**
{
"message": "Пользователь успешно удален",
"status": "success"
}



#### **2.5 Поиск пользователей**

**GET** `/users/search?query={текст}`

**Пример:** `/users/search?query=Иван`

**Ответ:** массив пользователей, у которых имя или фамилия содержит запрос



#### **2.6 Получить активных пользователей**

**GET** `/users/active`

**Ответ:** массив активных пользователей (`isActive = true`)



### **3. Управление командами**

#### **3.1 Получить все команды**

**GET** `/teams`

**Ответ:**
\[
{
"id": "team456",
"name": "DevStars",
"description": "Команда опытных разработчиков",
"projectName": "AI Assistant",
"projectDescription": "Умный помощник на базе ИИ",
"teamLeadId": "user123",
"memberIds": \["user123", "user456", "user789"],
"isActive": true
}
]



#### **3.2 Получить команду по ID**

**GET** `/teams/{id}`

**Ответ:** объект команды (как в п.3.1)



#### **3.3 Обновить команду**

**PUT** `/teams/{id}`

**Content-Type:** `application/json`

**Тело запроса:**
{
"name": "DevStars",
"description": "Команда опытных разработчиков",
"projectName": "AI Assistant",
"projectDescription": "Умный помощник на базе ИИ",
"teamLeadId": "user123",
"memberIds": \["user123", "user456", "user789"],
"isActive": true
}

**Ответ:** обновленная команда



#### **3.4 Удалить команду**

**DELETE** `/teams/{id}`

**Ответ:**
{
"message": "Команда успешно удалена",
"status": "success"
}

#### **3.5 Поиск команд**

**GET** `/teams/search?query={текст}`

**Пример:** `/teams/search?query=Dev`

**Ответ:** массив команд, название которых содержит запрос



#### **3.6 Получить команды пользователя**

**GET** `/teams/user/{userId}`

**Пример:** `/teams/user/user123`

**Ответ:** массив команд, в которых состоит пользователь



#### **3.7 Получить активные команды**

**GET** `/teams/active`

**Ответ:** массив активных команд (`isActive = true`)



### **4. Коды ответов**

|Код|Описание|
|-|-|
|200|Успешный запрос (GET, PUT)|
|201|Успешное создание (POST)|
|400|Ошибка в запросе (неверные данные)|
|404|Ресурс не найден|
|500|Внутренняя ошибка сервера|



