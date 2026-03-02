Извините за недопонимание! Вот файлы, адаптированные под ваше техническое задание по управлению командами:

---

## for\_frontend.md

# **ENDPOINTS**

## Команды

### ***1. Создать команду:***

**POST /api/teams**

**Content-Type: application/json**

```json
{
    "name": "Hackathon Masters",
    "description": "Команда профессионалов",
    "creatorId": "user123",
    "creatorName": "Иван Петров"
}
```

**Пример ответа:**

```json
{
    "id": 1,
    "name": "Hackathon Masters",
    "description": "Команда профессионалов",
    "creatorId": "user123",
    "creatorName": "Иван Петров",
    "createdAt": "2026-03-02T10:30:00"
}
```

---

### ***2. Получить команды пользователя:***

**GET /api/teams/user/{userId}**

**Пример:** `/api/teams/user/user123`

**Пример ответа:**

```json
\[
    {
        "id": 1,
        "name": "Hackathon Masters",
        "description": "Команда профессионалов",
        "creatorId": "user123",
        "creatorName": "Иван Петров",
        "createdAt": "2026-03-02T10:30:00"
    },
    {
        "id": 2,
        "name": "Code Warriors",
        "description": "Воины кода",
        "creatorId": "user456",
        "creatorName": "Петр Сидоров",
        "createdAt": "2026-03-01T15:20:00"
    }
]
```

---

### ***3. Получить информацию о команде:***

**GET /api/teams/{teamId}**

**Пример:** `/api/teams/1`

**Пример ответа:**

```json
{
    "id": 1,
    "name": "Hackathon Masters",
    "description": "Команда профессионалов",
    "creatorId": "user123",
    "creatorName": "Иван Петров",
    "createdAt": "2026-03-02T10:30:00"
}
```

---

### ***4. Получить участников команды:***

**GET /api/teams/{teamId}/members**

**Пример:** `/api/teams/1/members`

**Пример ответа:**

```json
\[
    {
        "id": 1,
        "userId": "user123",
        "userName": "Иван Петров",
        "joinedAt": "2026-03-02T10:30:00",
        "isCreator": true
    },
    {
        "id": 2,
        "userId": "user456",
        "userName": "Петр Сидоров",
        "joinedAt": "2026-03-02T11:15:00",
        "isCreator": false
    }
]
```

---

### ***5. Проверить, является ли пользователь создателем:***

**GET /api/teams/{teamId}/is-creator/{userId}**

**Пример:** `/api/teams/1/is-creator/user123`

**Пример ответа:**

```json
{
    "isCreator": true
}
```

---

## Заявки на вступление

### ***6. Отправить заявку на вступление:***

**POST /api/join-requests**

**Content-Type: application/json**

```json
{
    "teamId": 1,
    "userId": "user789",
    "userName": "Анна Иванова",
    "message": "Хочу присоединиться к вашей команде! Имею опыт в Java и Spring"
}
```

**Пример ответа:**

```json
{
    "id": 101,
    "team": {
        "id": 1,
        "name": "Hackathon Masters"
    },
    "userId": "user789",
    "userName": "Анна Иванова",
    "message": "Хочу присоединиться к вашей команде! Имею опыт в Java и Spring",
    "status": "PENDING",
    "createdAt": "2026-03-02T12:00:00",
    "processedAt": null
}
```

---

### ***7. Получить ожидающие заявки команды (только для создателя):***

**GET /api/join-requests/team/{teamId}/pending?userId={creatorId}**

**Пример:** `/api/join-requests/team/1/pending?userId=user123`

**Пример ответа:**

```json
\[
    {
        "id": 101,
        "team": {
            "id": 1,
            "name": "Hackathon Masters"
        },
        "userId": "user789",
        "userName": "Анна Иванова",
        "message": "Хочу присоединиться к вашей команде! Имею опыт в Java и Spring",
        "status": "PENDING",
        "createdAt": "2026-03-02T12:00:00",
        "processedAt": null
    },
    {
        "id": 102,
        "team": {
            "id": 1,
            "name": "Hackathon Masters"
        },
        "userId": "user999",
        "userName": "Сергей Козлов",
        "message": "Возьмете фронтенд-разработчика?",
        "status": "PENDING",
        "createdAt": "2026-03-02T12:30:00",
        "processedAt": null
    }
]
```

---

### ***8. Обработать заявку (одобрить/отклонить):***

**POST /api/join-requests/process**

**Content-Type: application/json**

```json
{
    "requestId": 101,
    "action": "approve"  // или "reject"
}
```

**Пример ответа (при одобрении):**

```json
{
    "id": 101,
    "team": {
        "id": 1,
        "name": "Hackathon Masters"
    },
    "userId": "user789",
    "userName": "Анна Иванова",
    "message": "Хочу присоединиться к вашей команде! Имею опыт в Java и Spring",
    "status": "APPROVED",
    "createdAt": "2026-03-02T12:00:00",
    "processedAt": "2026-03-02T13:15:00"
}
```

---

### ***9. Получить все заявки пользователя:***

**GET /api/join-requests/user/{userId}**

**Пример:** `/api/join-requests/user/user789`

**Пример ответа:**

```json
\[
    {
        "id": 101,
        "team": {
            "id": 1,
            "name": "Hackathon Masters"
        },
        "userId": "user789",
        "userName": "Анна Иванова",
        "message": "Хочу присоединиться к вашей команде! Имею опыт в Java и Spring",
        "status": "APPROVED",
        "createdAt": "2026-03-02T12:00:00",
        "processedAt": "2026-03-02T13:15:00"
    }
]
```

## Регистрация на хакатоны

### ***10. Зарегистрировать команду на хакатон (только создатель):***

**POST /api/hackathon-registrations**

**Content-Type: application/json**

```json
{
    "teamId": 1,
    "hackathonId": "hackathon456",
    "hackathonName": "Spring Hackathon 2026",
    "registeredBy": "user123"
}
```

**Пример ответа:**

```json
{
    "id": 1,
    "team": {
        "id": 1,
        "name": "Hackathon Masters"
    },
    "hackathonId": "hackathon456",
    "hackathonName": "Spring Hackathon 2026",
    "registeredBy": "user123",
    "registeredAt": "2026-03-02T14:00:00"
}
```

---

### ***11. Получить регистрации команды:***

**GET /api/hackathon-registrations/team/{teamId}**

**Пример:** `/api/hackathon-registrations/team/1`

**Пример ответа:**

```json
\[
    {
        "id": 1,
        "team": {
            "id": 1,
            "name": "Hackathon Masters"
        },
        "hackathonId": "hackathon456",
        "hackathonName": "Spring Hackathon 2026",
        "registeredBy": "user123",
        "registeredAt": "2026-03-02T14:00:00"
    }
]
```

---

### ***12. Получить все команды, зарегистрированные на хакатон:***

**GET /api/hackathon-registrations/hackathon/{hackathonId}**

**Пример:** `/api/hackathon-registrations/hackathon/hackathon456`

**Пример ответа:**

```json
\[
    {
        "id": 1,
        "team": {
            "id": 1,
            "name": "Hackathon Masters"
        },
        "hackathonId": "hackathon456",
        "hackathonName": "Spring Hackathon 2026",
        "registeredBy": "user123",
        "registeredAt": "2026-03-02T14:00:00"
    }
]
```

