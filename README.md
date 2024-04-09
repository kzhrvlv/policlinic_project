# policlinic_project
Development of an information system for the polyclinic database using Python Flask and REST API

# Описание предметной области

Поликлиника состоит из множества врачей, пациентов, отделений и других сущностей. Для работы необходимо обеспечить такие возможности информационной системы, как:
- Авторизация/деавторизация
- Заполнение врачом карты пациента
- Просмотр расписания
- Создание и просмотр отчетов (для примера отчеты о посещаемости, отчеты о количестве заболеваний)
- Запись на прием к врачу для пациентов

## В информационной системе для поликлиники определено 5 видов конечных пользователей:
1. Врач – имеет доступ к заполнению карт пациентов.
2. Администратор – имеет доступ к расписанию, может выполнять запросы к расписанию.
3. Заведующий отделением – имеет доступ к работе с отчетами (может как создавать отчеты, так и просматривать их).
4. Главврач – имеет доступ только к просмотру отчетов.
5. Пациент – имеет возможность удаленно записываться на прием к врачу.
Все конечные пользователи должны пройти авторизацию для последующей работы с ИС.

## Вариант использования «Авторизация»
### Сценарий конечного пользователя:
#### Главный успешный сценарий:
1. Пользователь начинает авторизацию.
2. Система присылает форму для ввода логина и пароля.
3. Пользователь вводит свой логин и пароль и отправляет их системе.
4. Система создает для пользователя сессию с его группой доступа и перенаправляет его в главное меню.
#### Исключения:
a. Неверный формат ввода параметров. Система снова присылает форму для ввода логина и пароля с сообщением об ошибке ввода.
б. Пользователь с таким логином и паролем не найден в системе. Система снова присылает форму для ввода логина и пароля с сообщением о неуспешной авторизации.

## Вариант использования «Выполнение запроса»
### Сценарий конечного пользователя:
#### Главный успешный сценарий:
1. Пользователь начинает работу с запросом.
2. Система присылает форму для ввода параметров запроса.
3. Пользователь вводит параметры и отправляет их системе.
4. Система присылает результат выполнения запроса.
#### Исключения:
4.a Пустой ввод параметров. Система снова присылает форму для ввода параметров запроса с сообщением об ошибке ввода.
4.б Результатом запроса оказался пустой result_set. Система снова присылает форму для ввода параметров запроса с сообщением об отсутствии результатов предыдущего запроса.

## Вариант использования «Работа с отчетами»
### Сценарий конечного пользователя:
#### Главный успешный сценарий:
1. Пользователь начинает работу с отчетами.
2. Система присылает страницу для работы с отчетами: соответствующими кнопками «создать» и «просмотр».
3. Пользовать выбирает функцию создания необходимого ему отчета.
4. Система присылает форму для ввода необходимых параметров: отчетного периода, по работе которого будет создаваться отчет.
5. Пользователь вводит параметры и отправляет их системе.
6. Система присылает страницу с сообщением об успешном создании отчета и предложением вернуться в меню отчетов.
7. Пользователь возвращается в меню отчетов и выбирает функцию просмотра необходимого ему отчета.
8. Система присылает форму для ввода параметров отчетного периода.
9. Пользователь вводит параметры и отправляет их системе.
10. Система присылает динамический шаблон с визуализацией отчета и предложением вернуться в меню отчетов.
#### Исключения:
4.a,
8.a Не введен отчетный период. Система снова присылает форму для ввода параметров отчетного периода с сообщением об ошибке ввода.
4.б Отчет за указанный отчетный период уже существует в БД. Система снова присылает форму для ввода параметров отчетного периода с соответствующим сообщением.
4.в Данные для отчета за указанный отчетный период отсутствуют в БД. Система снова присылает форму для ввода параметров отчетного периода с соответствующим сообщением.
8.б Отчет за указанный отчетный период отсутствует в системе. Система снова присылает форму для ввода параметров отчетного периода с соответствующим сообщением.

## Вариант использования «Запись на прием к врачу»
### Сценарий конечного пользователя:
#### Главный успешный сценарий:
1. Пользователь заходит на страницу записи на прием.
2. Система выдает страницу со списком доступных окон для записи.
3. Пользователь вводит номер своей карты и нажимает кнопку «Записаться».
4. Система присылает страницу со списком доступных окон для записи с информационным сообщением о том, что запись на прием добавлена в список.
5. Пользователь нажимает кнопку «Перейти к подтверждению записей».
6. Система присылает страницу для отображения выбранных пациентом записей в списке (аналог «корзины»).
7. Пользователь нажимает кнопку «Очистить список приемов».
8. Система присылает страницу со списком доступных окон для записи с информационным сообщением, что список очищен.
9. Пользователь нажимает кнопку «Подтвердить запись».
10. Система возвращается на страницу с выбором окон для записи к врачу.
#### Исключения:
3.а Пользователь ничего не ввел в поле «Пациент». Система выводит сообщение об ошибке «Пустой ввод».
