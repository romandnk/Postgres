## Домашнее задание: Работа с уровнями изоляции транзакции в PostgreSQL

### Цель:
- Научиться управлять уровнем изоляции транзакции в PostgreSQL и понимать особенность работы уровней read committed и repeatable read.

### Описание/Пошаговая инструкция выполнения домашнего задания:
1. Создать новый проект в Google Cloud Platform, Яндекс облако или на любых ВМ, докере.
2. Создать инстанс виртуальной машины с дефолтными параметрами.
3. Добавить свой SSH ключ в metadata ВМ.
4. Зайти удаленным SSH (первая сессия), не забывайте про SSH-add.
5. Установить PostgreSQL.
6. Зайти вторым SSH (вторая сессия).
7. Запустить везде psql из под пользователя postgres.
8. Выключить автокоммит.
9. В первой сессии создать новую таблицу и наполнить ее данными:
   ```sql
   create table persons(id serial, first_name text, second_name text); 
   insert into persons(first_name, second_name) values('ivan', 'ivanov'); 
   insert into persons(first_name, second_name) values('petr', 'petrov');
10. посмотреть текущий уровень изоляции  
    ```sql 
    show transaction isolation level
11. начать новую транзакцию в обоих сессиях с дефолтным (не меняя) уровнем изоляции
12. в первой сессии добавить новую запись  
    ```sql 
    insert into persons(first_name, second_name) values('sergey', 'sergeev');
13. сделать  
    ```sql 
    select from persons во второй сессии
14. видите ли вы новую запись и если да то почему?
15. завершить первую транзакцию 
    ```sql 
     commit;
16. сделать  
    ```sql 
    select from persons во второй сессии
17. видите ли вы новую запись и если да то почему?
18. завершите транзакцию во второй сессии
19. начать новые но уже repeatable read транзакции 
    ```sql 
    set transaction isolation level repeatable read;
20. в первой сессии добавить новую запись  
    ```sql 
    insert into persons(first_name, second_name) values('sveta', 'svetova');
21. сделать  
    ```sql 
    select* from persons во второй сессии*
22. видите ли вы новую запись и если да то почему?
23. завершить первую транзакцию - commit;
24. сделать  
    ```sql 
    select from persons во второй сессии
25. видите ли вы новую запись и если да то почему?
26. завершить вторую транзакцию
27. сделать 
    ```sql
    select * from persons во второй сессии
28. видите ли вы новую запись и если да то почему?