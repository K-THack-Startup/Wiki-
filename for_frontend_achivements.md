# **\_\_ENDPOINTS\_\_**

### 



### ***1. Получить все ачивки:***

**GET /api/achievements**





### ***2. Получить ачивки пользователя по ID:***

**POST /api/achievement**

**Content-Type: application/json**



*{*
*"byType": "ID",*
*"value": "user123"*
*}*





### ***3. Получить пользователей с определенной ачивкой:***

**POST /api/user\_achievements**

**Content-Type: application/json**



*{*
*"byType": "achievement",*
*"value": "1"*
*}*





### ***4. Получить активность пользователя по ID:***

**POST /api/user\_activity**

**Content-Type: application/json**



*{*
*"byType": "ID",*
*"value": "user123"*
*}*





### ***5. Получить пользователей, отсортированных по посещениям:***

**POST /api/user\_activity**

**Content-Type: application/json**



*{*
*"byType": "visited\_hackathons",*
*}*





### ***6. Получить пользователей, отсортированных по баллам:***

**POST /api/user\_activity**

**Content-Type: application/json**



*{*
*"byType": "points",*
*}*





### ***7. Сбросить данные пользователя:***

**Пример:**

*DELETE /api/reset/user123*


### Хакатоны пользователя

**1. Создать запись об участии:**
```
POST /api/user-hackathons
Content-Type: application/json

{
    "userId": "user123",
    "hackathonId": "hackathon456",
    "hackathonName": "Spring Hackathon 2026"
}
```

**2. Подтвердить участие и выставить баллы (судья):**
```
PUT /api/user-hackathons/{id}/approve
Content-Type: application/json

{
    "points": 8,
    "placement": 2,
    "isWinner": true
}
```

**3. Отклонить участие:**
```
PUT /api/user-hackathons/{id}/reject
```

**4. Получить все хакатоны пользователя:**
```
GET /api/user-hackathons/user/{userId}
```

**5. Получить неподтвержденные участия (для судьи):**
```
GET /api/user-hackathons/pending
```

**Ответ при создании участия:**
```json
{
    "id": 1,
    "userId": "user123",
    "hackathonId": "hackathon456",
    "hackathonName": "Spring Hackathon 2026",
    "points": null,
    "placement": null,
    "isWinner": false,
    "isApproved": false,
    "processed": false,
    "createdAt": "2026-02-12T10:30:00",
    "approvedAt": null,
    "processedAt": null
}
```

**Ответ после approve:**
```json
{
    "id": 1,
    "userId": "user123",
    "hackathonId": "hackathon456",
    "hackathonName": "Spring Hackathon 2026",
    "points": 8,
    "placement": 2,
    "isWinner": true,
    "isApproved": true,
    "processed": false,
    "createdAt": "2026-02-12T10:30:00",
    "approvedAt": "2026-02-12T10:35:00",
    "processedAt": null
}
```