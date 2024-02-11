# Лабораторная работа №4
**Проектирование REST API**

## Документация по API

### get_reserved_mails
**метод:** GET

**описание:** получение записей о резервных почтах

**параметры запроса:** нет

**ответ:**
get_reserved_mails
- user_id: int (идентификатор пользователя)
- email: string (резервный email пользователя)


### get_user_results
**метод:** GET

**описание:** получение записей о всех результатах всех пользователей

**параметры запроса:** нет

**ответ:**
get_user_results
- user_id: int (идентификатор пользователя)
- result_id: int (идентификатор результата)


### user_extended_results
**метод:** GET

**описание:** получение результатов всех пользователей (с подробностями)

**параметры запроса:** нет

**ответ:**
user_extended_results
- result_text: string (сохранённый текст результата)
- result_colors: string | null (сохранённые выявленные цвета)
- result_shapes: strind | null (сохранённые выявленные формы)
- result_moods: string | null (сохранённые выявленные настроения)
- result_emotionality: string | null (сохранённая выявленная эмоциональность текста)


### add_mail
**метод:** POST

**описание:** создание записи о новой резервной почте пользователя

**параметры запроса:** 
ReservedMailEntity (объект, содержащий информацию о резервной почте пользователя)
- user_id: int (идентификатор пользователя)
- email: string (резервный email пользователя)

**ответ:**
DBReservedMail
- id: int (идентификатор записи)
- user_id: int (идентификатор пользователя)
- email: string (резервный email пользователя)


### add_user
**метод:** POST

**описание:** создание записи о пользователе

**параметры запроса:** 
UserEntity (объект, содержащий информацию о пользователе)
- login: string (логин пользователя)
- password: string (пароль пользователя)

**ответ:**
DBUser
- user_id: int (идентификатор пользователя)
- login: string (логин пользователя)
- password: string (пароль пользователя)


### add_result
**метод:** POST

**описание:** создание записи о новом результате

**параметры запроса:** 
ResultEntity (объект, содержащий информацию о результате)
- user_id: int (идентификатор пользователя)
- result_id: int (идентификатор результата)

**ответ:**
DBResult
- id: int (идентификатор записи)
- user_id: int (идентификатор пользователя)
- result_id: int (идентификатор результата)


### delete_reserved_mail
**метод:** DELETE

**описание:** удаление резервной почты пользователя

**параметры запроса:** 
ReservedMailEntity (объект, содержащий информацию о резервной почте пользователя)
- user_id: int (идентификатор пользователя)
- email: string (резервный email пользователя)

**ответ:**
DBReservedMail
- id: int (идентификатор записи)
- user_id: int (идентификатор пользователя)
- email: string (резервный email пользователя)


### delete_user
**метод:** DELETE

**описание:** удаление данных о пользователе

**параметры запроса:** 
UserEntity (объект, содержащий информацию о пользователе)
- login: string (логин пользователя)
- password: string (пароль пользователя)

**ответ:**
DBUser
- user_id: int (идентификатор пользователя)
- login: string (логин пользователя)
- password: string (пароль пользователя)


### put_password
**метод:** PUT
**описание:** смена пароля

**параметры запроса:** 
UserEntity (объект, содержащий информацию о пользователе)
- login: string (логин пользователя)
- password: string (пароль пользователя)

**ответ:**
DBUser
- user_id: int (идентификатор пользователя)
- login: string (логин пользователя)
- password: string (пароль пользователя)


## Тестирование при помощи Postman

### get_reserved_mails
**метод:** GET

**строка запроса:** http://127.0.0.1:5000/reserved_mails


**передаваемые заголовки и параметры:** 
![image](https://github.com/U-2745/software_architecture/assets/78296925/d718afe0-ea0b-4aa2-b972-ecc9421a0f90)
![image](https://github.com/U-2745/software_architecture/assets/78296925/48a43c53-d232-4967-9b54-f438ab09bafb)
![image](https://github.com/U-2745/software_architecture/assets/78296925/697cd815-67f4-4984-ab47-f056ab74cffb)
![image](https://github.com/U-2745/software_architecture/assets/78296925/e4848133-224b-4d82-bca8-6f3e8e9c3139)

**полученный от Postman ответ:** 
- body
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Резервные почты</title>
</head>

<body>
    <h1>Резервные почты:</h1>
    <table>
        <tr>
            <td><a href='/'>ГЛАВНАЯ</a></td>
            <td><a href='/reserved_mails'>Все резервные почты</a></td>
            <td><a href='/add_user'>Добавить пользователя</a></td>
            <td><a href='/add_mail'>Добавить резервную почту</a></td>
        </tr>
    </table>
    <table>
        <thead>
            <tr>
                <th>Пользователь (id)</th>
                <th>Резервная почта</th>
            </tr>
        </thead>
        <tbody>

            <tr>
                <td>1</td>
                <td>kittinka@mail.mi</td>
            </tr>

            <tr>
                <td>2</td>
                <td>KITY@mail.com</td>
            </tr>

            <tr>
                <td>3</td>
                <td>cat@cat</td>
            </tr>

        </tbody>
    </table>
</body>


</html>
```

- headers
![image](https://github.com/U-2745/software_architecture/assets/78296925/0c789b27-0003-4dd4-bf4e-7353cc9a72a4)

**Код автотестов:** 

```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
pm.test("Body contains data", function () {
    pm.expect(pm.response.text()).to.include("kittinka@mail.mi");
});
```

**Результат автотестов:** 
![image](https://github.com/U-2745/software_architecture/assets/78296925/1020ba1c-d259-4d82-9ea5-49821a4730dd)


### get_user_results
**метод:** GET

**строка запроса:** http://127.0.0.1:5000/user_results


**передаваемые заголовки и параметры:** 
![image](https://github.com/U-2745/software_architecture/assets/78296925/a07386cd-ec38-4535-970e-654a89bbedc7)
![image](https://github.com/U-2745/software_architecture/assets/78296925/5818e4f4-053d-4430-ac0f-04377c1215ef)
![image](https://github.com/U-2745/software_architecture/assets/78296925/65d184c4-0d4e-4ba7-8e3e-976c645ba357)
![image](https://github.com/U-2745/software_architecture/assets/78296925/014f7b48-ca32-4e40-99c7-09068dbefdca)


**полученный от Postman ответ:** 

- body
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Сохранённые результаты</title>
</head>

<body>
    <h1>Сохранённые результаты:</h1>
    <table>
        <tr>
            <td><a href='/'>ГЛАВНАЯ</a></td>
            <td><a href='/user_results'>Все сохранённые результаты</a></td>
            <td><a href='/user_extended_results'>Все результаты (подробно)</a></td>
            <td><a href='/add_result'>Добавить результат</a></td>
        </tr>
    </table>
    <table>
        <thead>
            <tr>
                <th>Пользователь (id)</th>
                <th>Результат (id)</th>
            </tr>
        </thead>
        <tbody>

            <tr>
                <td>1</td>
                <td>1</td>
            </tr>

        </tbody>
    </table>
</body>

</html>
```

- headers
![image](https://github.com/U-2745/software_architecture/assets/78296925/52b14f05-bd32-407d-b99c-31652856f44d)


**Код автотестов:** 

```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
pm.test("Body contains data", function () {
    pm.expect(pm.response.text()).to.include("<td>1</td>");
});
```

**Результат автотестов:** 
![image](https://github.com/U-2745/software_architecture/assets/78296925/09cf4746-11ca-4df1-8510-ac51044cdc00)


### get_user_extended_results
**метод:** GET

**строка запроса:** http://127.0.0.1:5000/user_extended_results


**передаваемые заголовки и параметры:** 
![image](https://github.com/U-2745/software_architecture/assets/78296925/934995e0-598f-4eb6-8d81-efee326f785e)
![image](https://github.com/U-2745/software_architecture/assets/78296925/11752436-6742-4f3c-a444-6b2259f8e3e0)
![image](https://github.com/U-2745/software_architecture/assets/78296925/3e106849-7342-4519-8fa9-fed13172277b)
![image](https://github.com/U-2745/software_architecture/assets/78296925/4e814c8c-1ca2-47b9-b7d1-5057ea94af1c)


**полученный от Postman ответ:** 

- body
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Сохранённые результаты (подробно)</title>
</head>

<body>
    <h1>Сохранённые результаты (подробно):</h1>
    <table>
        <tr>
            <td><a href='/'>ГЛАВНАЯ</a></td>
            <td><a href='/user_extended_results'>Все результаты (подробно)</a></td>
        </tr>
    </table>
    <table>
        <thead>
            <tr>
                <th>id результата</th>
                <th>Цвета</th>
                <th>Формы</th>
                <th>Настроения</th>
                <th>Эмоциональность</th>
            </tr>
        </thead>
        <tbody>

            <tr>
                <td></td>
                <td>blue</td>
                <td>triangle</td>
                <td>positive, anticipation, joy</td>
                <td>0.63</td>
            </tr>

        </tbody>
    </table>
</body>

</html>
```

- headers
![image](https://github.com/U-2745/software_architecture/assets/78296925/8329edaa-f6a0-45d6-adfd-10b5f7917c3f)


**Код автотестов:** 
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
pm.test("Body contains data", function () {
    pm.expect(pm.response.text()).to.include("positive, anticipation, joy");
});
```

**Результат автотестов:** 
![image](https://github.com/U-2745/software_architecture/assets/78296925/2663e822-c3e6-437f-b059-b488ce5a6132)


### add_user
**метод:** POST

**строка запроса:** http://127.0.0.1:5000/add_user?login=postman_login&password=postman_password


**передаваемые заголовки и параметры:** 
![image](https://github.com/U-2745/software_architecture/assets/78296925/9e9b005d-5b36-410b-94b3-24d10701312e)
![image](https://github.com/U-2745/software_architecture/assets/78296925/2ab3fd91-8c4d-4b53-a3bd-8da7d8865855)
![image](https://github.com/U-2745/software_architecture/assets/78296925/372de6e4-8fb7-4a45-a917-cd6197c7b190)
![image](https://github.com/U-2745/software_architecture/assets/78296925/66296120-1f4d-46c8-8b36-f488364517b6)


**полученный от Postman ответ:** 

- body
```
{"login":"postman_login","password":"postman_password","user_id":8}
```

- headers
![image](https://github.com/U-2745/software_architecture/assets/78296925/cc59212b-338f-4d97-91a0-a83ee0761908)


**Код автотестов:** 

```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
pm.test("Body contains data", function () {
    pm.expect(pm.response.text()).to.include("postman_login");
});
```

**Результат автотестов:** 
![image](https://github.com/U-2745/software_architecture/assets/78296925/8b8728de-ee1a-460b-86fc-963e81b5a4d8)


### add_mail
**метод:** POST

**строка запроса:** http://127.0.0.1:5000/add_mail?email=cat_lover@cat.com&user_id=1


**передаваемые заголовки и параметры:** 
![image](https://github.com/U-2745/software_architecture/assets/78296925/f3b1d2d2-dd0a-4227-92d6-8848246a7986)
![image](https://github.com/U-2745/software_architecture/assets/78296925/9bb7a7c5-7ba4-4205-8e95-caec0df16882)
![image](https://github.com/U-2745/software_architecture/assets/78296925/83dea2d1-33b1-435c-95d3-3df29f521d87)
![image](https://github.com/U-2745/software_architecture/assets/78296925/63151e30-c64c-4e68-b765-b8c0ffd72d7f)



**полученный от Postman ответ:** 

- body
```
{"email":"cat_lover@cat.com","id":5,"user_id":1}
```

- headers
![image](https://github.com/U-2745/software_architecture/assets/78296925/d7fc9101-e2d1-4521-a94d-1276b7269029)


**Код автотестов:** 

```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
pm.test("Body contains data", function () {
    pm.expect(pm.response.text()).to.include("cat_lover");
});
```

**Результат автотестов:** 
![image](https://github.com/U-2745/software_architecture/assets/78296925/55941129-9d1c-4a4b-83e5-0994aa6d96c9)



### add_result
**метод:** POST

**строка запроса:** http://127.0.0.1:5000/add_result?result_id=7&user_id=2


**передаваемые заголовки и параметры:** 
![image](https://github.com/U-2745/software_architecture/assets/78296925/8e1683b2-4c8a-4aa4-b3ca-d392d2948c82)
![image](https://github.com/U-2745/software_architecture/assets/78296925/7634fcb2-bb9a-4b96-8efc-c1f3da659df7)
![image](https://github.com/U-2745/software_architecture/assets/78296925/e420b852-c07b-4e7e-b6bc-8cb2fc8f2550)
![image](https://github.com/U-2745/software_architecture/assets/78296925/1a4d050f-5de7-472c-9fcc-70001cd1a1e1)



**полученный от Postman ответ:** 

- body
```
{"id":4,"result_id":7,"user_id":2}
```

- headers
![image](https://github.com/U-2745/software_architecture/assets/78296925/d6dbe726-18b1-4a46-b86f-e90dfa54ae47)


**Код автотестов:** 

```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
pm.test("Body contains data", function () {
    pm.expect(pm.response.text()).to.include("7");
});
```

**Результат автотестов:** 
![image](https://github.com/U-2745/software_architecture/assets/78296925/cce93662-c325-41db-bc33-d941eac67c42)
