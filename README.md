# SQL
## Тут информация по базовым вопросам SQL

вопросы по JOIN 
пояснение LEFT OUTER JOIN (и все остальные JOINы) пишут без OUTER.

- INNER JOIN пишут как JOIN.
```bash
SELECT spendings.*, users.name FROM spendings JOIN users ON users.user_id = spending.id
```
- JOIN тут является INNER JOIN

self JOIN
Это когда сравнение происходит в самой таблице (Пример: Таблица сотрудников и кто кому подчиняется там же указано как id этой же таблицы)

left JOIN
Поиск связей и вывод всех данных даже без связи с параметром NULL из левой таблицы

right JOIN
Поиск связей и вывод всех данных даже без связи с параметром NULL из правой таблицы

inner JOIN он же JOIN
Поиск связей и вывод только связные данные из двух таблиц

full JOIN
Поиск связей и вывод всех данных с параметром NULL если у тех нет связей

cross JOIN
Поиск с множеством связей (Не использовал на практике)

вопросы по FINAL
Обработка только финальной версии записи. Некоторые базы данных такие как ClickHouse могут 
хранить несколько экземпляров записи одного поля и может вернуть по запросу "устаревшие" данные.

вопрос по IN
Используется как упрощенный(латентный) JOIN (ускоряет запрос)

## БАЗОВЫЕ ЗАПРОСЫ

Запрос
 ```bash
INSERT INTO users (name, age) VALUES ('name', 22);
```

Запрос
```bash
UPDATE users SET name = 'NewName', age = 33 WHERE id = 11;
```

Запрос
```bash
DELETE FROM users WHERE id = 11;
```

Запрос
```bash
SELECT * FROM users WHERE id = 11 OR id = 1;
```

## АГРЕГАТНЫЕ ФУНКЦИИ 

SUM(price) суммирование данных
```bash
SELECT SUM(price) FROM spendings;
```

так же стоит добавить метод GROUP BY для разделения полей и получения суммы конкретного направления (user)
```bash
SELECT SUM(price) FROM spendings GROUP BY user_id;
```
тут уже мы получим сумму относящуюся к конкретному пользователю, в результате все пользователи с своей суммой. Получаем финальные данные.

HAVING это метод замена для WHERE(не может принимать агрегатные функции типа sum() ) который может принимать агрегатные функция как условие сравнения.
HAVING может быть только вконце запроса, после GROUP BY.

результат:
```bash
SELECT users.*, SUM(spendings.price) 
FROM users 
JOIN spendings ON users.id = spendings.user_id 
GROUP_BY users.id, spendings.user_id 
HAVING SUM(spendinsts.price) > 10000;
```
