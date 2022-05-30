# SQL
## Оглавление 
-[Простые запросы]

--------------------------------------------------------------------------------------------------------------------------------------------------------
##### Задания:
1. Вывести номер первые три цифры номера, если он идет в формате: ХХХ.ХХХ.ХХХХ
```SQL
SELECT first_name, phone_number, SUBSTR(phone_number, 1, 3)
FROM hr.employees
WHERE phone_number LIKE '___.___.____';
```
2. Получите список всех сотрудников, у которых последняя буква в имени равна 'm' и длина имени больше 5ти.
```sql
SELECT first_name
FROM hr.employees
WHERE LENGTH(first_name) >5 and first_name LIKE '%%%%%m';
```
3. Вывести дату след. пятницы
```sql
SELECT NEXT_DAY(sysdate, 6)
FROM dual;
```
4. Получите список всех сотрудников, которые работают в компании больше 12 лет и 6ти месяцев (150 месяцев)
```sql
SELECT first_name, hire_date, ADD_MONTHS(hire_date, 150)
FROM hr.employees;
```
5. Выведите телефонный номер, заменив в значении PHONE_NUMBER все '.' на '-'.
```sql
SELECT first_name, phone_number, replace(phone_number, '.', '-')
FROM hr.employees;
```
6. Выведите имя, email, job_id для всех работников в формате: STEVEN sking Ad_Pres
```sql
SELECT first_name, email, job_id, UPPER(first_name), LOWER(email), INITCAP(job_id)
FROM hr.employees;
```
7. Выведите информацию о имени работника и его з/п, не используя символ || , в таком виде: Steven24000
```sql
SELECT first_name, salary, CONCAT(first_name, salary) AS new
FROM hr.employees;
```
8. Выведите информацию о дате приёма сотрудника на работу, округлённой дате приёма на работу до месяца и первом дне года приёма на работу.
```sql
SELECT first_name, hire_date, ROUND(hire_date, 'mm'), TRUNC(hire_date, 'YYYY')
FROM hr.employees;
```
9. Выведите информацию о имени и фамилии всех работников. Имя должно состоять из 10 символов и если длина имени меньше 10, то дополняйте до 10 символов знаком $. Фамилия должна состоять из 15 символов и если длина фамилии меньше 15, то перед фамилией ставьте столько знаков ! сколько необходимо.
```SQL
SELECT first_name, last_name, RPAD(first_name, 10, '$'), LPAD(last_name, 15, '!')
FROM hr.employees;
```
10. Выведите имя сотрудника и позицию второй буквы ‘a’ в его имени
```sql
SELECT first_name, INSTR(first_name, 'a', 1, 2)
FROM hr.employees;
```
11. Выведите на экран текст '!!!HELLO!! MY FRIEND!!!!!!!!' и тот же текст, но без символа восклицательный знак в начале и конце текста.
```sql
SELECT  '!!!HELLO!! MY FRIEND!!!!!!!!', TRIM(BOTH '!' FROM '!!!HELLO!! MY FRIEND!!!!!!!!')
FROM dual;
```
12. 4.Выведите информацию о:  з/п работника,  з/п умноженной на коэффициент 3.1415 ,  округлённый до целого значения вариант увеличенной з/п-ты,  целое количество тысяч из увеличенной з/п
```sql
SELECT salary, salary*3.1415, ROUND(salary*3.1415), ROUND((salary*3.1415)/1000)
FROM hr.employees
```
13. Выведите информацию о:  дате приёма сотрудника на работу,  дате, которая была через пол года, после принятия сотрудника на работу,  дате последнего дня в месяце принятия сотрудника на работу.
```sql
SELECT hire_date, add_months(hire_date, 6), last_day(hire_date)
FROM hr.employees;
```
