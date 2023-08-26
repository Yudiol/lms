# lms
## Примерный дизайн 
https://www.figma.com/file/GoNQ6PeA0VtruUAWO1YlG1/LMS?type=design&mode=design&t=Ja79CpR8ynN0eVMP-1
## Мини-lms система для родителей, которые организуют семейное обучение детей дома
Первоначальный MVP не предусматривает регистрацию пользователей. 
Считаем что пользователь уже зарегистрирован. В таблице Users хранятся данные о пользователе: логин, пароль и токен. 
Для получения информации о пользователе необходимо сформировать запрос, передав в заголовке Authorization токен пользователя
(заглушка для будущей авторизации).  

## Эндпоинты (во всех нужно передавать заголовок Authorization):
GET /users - получение информации о пользователе (Имя, Фамилия, Ник, Дата рождения, Дата регистрации, Аватар)
PATCH /users - изменение информации о пользователе  

GET /users/lessons?from=2020-12-25&&to=2020-12-31- получение информации о запланированных пользователем уроках 
в заданном диапазоне, включая указанные даты. Если параметры не указаны - то возвращаются уроки за текущую неделю.  
Список параметров по каждому событию:  
- Дата
- Время начала
- Время окончания
- Название предмета
- Отметка о выполнении (выставляется при % выполнения 100 автоматически или вручную при любом % выполнения)

GET /users/lesson/{lessonId}- получение информации о конкретном уроке. Возвращаются данные:  
- Дата
- Время начала
- Время окончания
- Название предмета
- Ссылка на теорию (ссылка на файл, пока просто храним как строку)
- Ссылка на практическое задание (ссылка на файл, пока просто храним как строку)
- Ссылка на домашнюю рабооту (ссылка на файл, пока просто храним как строку)
- % выполнения (от 0 до 100%)
- Отметка о выполнении (выставляется при % выполнения 100 автоматически или вручную при любом % выполнения)

POST /users/lesson - создание нового урока, в теле данные урока  
PATCH /users/lesson/{lessonId} - изменение урока, в теле данные урока  
DELETE /users/lesson/{lessonId} - удаление урока

