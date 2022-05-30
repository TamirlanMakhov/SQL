# SQL
## Оглавление 
-[hw_1 Simple](https://github.com/TamirlanMakhov/SQL#HW_1)

-[hw_2 Simple](https://github.com/TamirlanMakhov/SQL#HW_1)

-[hw_3 Group functions](https://github.com/TamirlanMakhov/SQL#HW_3-Grou-functions)

-[hw_4 Joins](https://github.com/TamirlanMakhov/SQL#HW_4-Join)

-[hw_5 Subqueries]((https://github.com/TamirlanMakhov/SQL#HW_5-Subqueries)


--------------------------------------------------------------------------------------------------------------------------------------------------------
### HW_1:

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
------------------------------------------------------------------------------------------------------------------------------------------------------
### HW_2
1. Используя функции, получите список всех сотрудников у которых в имени есть буква 'b' (без учета регистра).
```sql
SELECT first_name
FROM hr.employees
WHERE LOWER(first_name) LIKE '%b%';
```

2. Используя функции, получите список всех сотрудников у которых в имени содержатся минимум 2 буквы 'a'.
```sql
SELECT first_name
FROM hr.employees
WHERE LOWER(first_name) LIKE '%a%a%';
```

3. Получите первое слово из имени департамента, для тех департаментов, у которых название состоит больше, чем из одного слова.
```sql
SELECT department_name, SUBSTR(department_name, 1, INSTR(department_name, ' '))
FROM hr.departments
WHERE INSTR(department_name, ' ') > 0;
```

4. Получите имена сотрудников без первой и последней буквы в имени
```sql
SELECT first_name, SUBSTR(first_name, 2, LENGTH(first_name)-2) AS without_first_last
FROM hr.employees;
```

5. Получите список всех сотрудников, у которых в значении job_id после знака ' _ ' как минимум 3 символа, но при этом это значение после ' _ ' не равно 'CLERK'.
```sql
SELECT first_name, job_id
FROM hr.employees
WHERE LENGTH(SUBSTR(job_id, 3)) >= 3
AND INSTR(job_id, 'CLERK') != 4;
```

6. Получите список всех сотрудников, которые пришли на работу в первый день любого месяца.
```sql
SELECT first_name, hire_date
FROM hr.employees
WHERE TO_CHAR(hire_date, 'fmdd') = 1;
```

7. Получите список всех сотрудников, которые пришли на работу в 2008ом году.
```sql
SELECT first_name, hire_date
FROM hr.employees
WHERE TO_CHAR(hire_date, 'yyyy') = 2008;
```

8. Покажите завтрашнюю дату в формате: Tomorrow is Second day of January
```sql
SELECT sysdate+1, 'Tomorrow is'||TO_CHAR(sysdate+1, ' ddthSP "day of" Month') AS next_day
FROM dual;
```

9. Выведите имя сотрудника и дату его прихода на работу в формате: 21st of June, 2007
```sql
SELECT first_name, hire_date, TO_CHAR(hire_date, 'ddth "of" fmMonth, yyyy')
FROM hr.employees; 
```

10. Получите список работников с увеличенными зарплатами на 20%. Зарплату показать в формате: $28,800.00
```sql
SELECT first_name, salary, TO_CHAR(salary*1.20, '$99,999.99')
FROM hr.employees; 
```

11. Выведите актуальную дату (нынешнюю), + секунда, + минута, + час, + день, + месяц, + год. (Всё это по отдельности прибавляется к актуальной дате).
```sql

```

12. Выведите имя сотрудника, его з/п и новую з/п, которая равна старой плюс это значение текста «$12,345.55».
```sql
SELECT first_name, salary, salary + TO_NUMBER('$12,345.55', '$99,999.99') AS new_salary
FROM hr.employees; 
```

13. Выведите имя сотрудника, день его трудоустройства, а также количество месяцев между днём его трудоустройства и датой, которую необходимо получить из текста «SEP, 18:45:00 18 2009».
```sql
SELECT first_name, hire_date, TO_DATE('SEP, 18:45:00 18 2009', 'MON, HH24:mi:ss dd yyyy'),  
ROUND(MONTHS_BETWEEN(TO_DATE('SEP, 18:45:00 18 2009', 'MON, HH24:mi:ss dd yyyy'), hire_date))
FROM hr.employees
ORDER BY hire_date;
```

14. Выведите имя сотрудника, его з/п, а также полную з/п (salary + commission_pct(%)) в формате: $24,000.00.
```sql
SELECT first_name, salary, commission_pct, TO_CHAR(salary+ NVL(commission_pct, 0), '$99,999.99')
FROM hr.employees;
```

15. Выведите имя сотрудника, его фамилию, а также выражение «different length», если длина имени не равна длине фамилии или выражение «same length», если длина имени равна длине фамилии. Не используйте conditional functions.
```sql
SELECT first_name, last_name, 
NVL2(NULLIF(LENGTH(first_name), LENGTH(last_name)),'different length', 'same length')
FROM hr.employees;
```

16. Выведите имя сотрудника, его комиссионные, а также информацию о наличии бонусов к зарплате – есть ли у него комиссионные (Yes/No).
```sql
SELECT first_name, commission_pct, NVL2(commission_pct, 'YES', 'NO')
FROM hr.employees;
```

17. *Выведите имя сотрудника и значение, которое его будет характеризовать: значение комиссионных, если присутствует, если нет, то id его менеджера, если и оно отсутствует, то его з/п.*
```sql
SELECT first_name, commission_pct, manager_id, salary,
NVL(NVL2(commission_pct, commission_pct, manager_id), salary)
FROM hr.employees;
```

18. Выведите имя сотрудника, его з/п, а также уровень зарплаты каждого сотрудника: Меньше 5000 считается Low level, Больше или равно 5000 и меньше 10000 считается Normal level, Больше или равно 10000 считается High level.
```sql
SELECT first_name, salary, 
CASE
WHEN salary < 5000 THEN 'LOW LEVEl'
WHEN salary >= 5000 and salary < 10000 THEN 'NORMAL LEVEL'
WHEN salary >= 10000 THEN 'HIGH LEVEL'
END
FROM hr.employees; 
```

19. Для каждой страны показать регион, в котором она находится: 1- Europe, 2-America, 3-Asia, 4-Africa . Выполнить данное задание, не используя функционал JOIN. Используйте DECODE.
```sql
SELECT country_name, region_id, 
DECODE(region_id, 1, 'Europe', 2, 'America', 3, 'Asia', 4, 'Africa')
FROM hr.countries; 
```

20. Задачу №19 решите используя CASE
```sql
SELECT country_name, region_id, 
CASE
WHEN region_id = 1 THEN 'Europe'
WHEN region_id = 2 THEN 'America'
WHEN region_id = 3 THEN 'Asia'
WHEN region_id = 4 THEN 'Africa'
END
AS country
FROM hr.countries; 
```

21. Выведите имя сотрудника, его з/п, а также уровень того, насколько у сотрудника хорошие условия :  BAD: з/п меньше 10000 и отсутствие комиссионных;  NORMAL: з/п между 10000 и 15000 или, если присутствуют комиссионные;  GOOD: з/п больше или равна 15000.
```sql
SELECT first_name, salary, 
CASE
WHEN (salary < 10000) and (commission_pct IS NULL) THEN 'Bad'
WHEN (salary > 10000 and salary < 15000) OR (commission_pct IS NOT NULL) THEN 'Normal'
WHEN salary >= 15000 THEN 'Good'
END
AS grade
FROM hr.employees;
```

------------------------------------------------------------------------------------------------------------------------------------------------------
### HW_3 Group functions
1. Получить репорт по department_id с минимальной и максимальной зарплатой, с самой ранней и самой поздней датой прихода на работу и с количеством сотрудников. Сортировать по количеству сотрудников (по убыванию).
```sql
SELECT department_id, MIN(SALARY), MAX(SALARY), MIN(hire_date), MAX(hire_date), COUNT(*)
FROM hr.employees
GROUP BY department_id
ORDER BY COUNT(*) DESC;
```

2. Выведите информацию о первой букве имени сотрудника и количество имён, которые начинаются с этой буквы. Выводить строки для букв, где количество имён, начинающихся с неё больше 1. Сортировать по количеству.
```sql
SELECT SUBSTR(first_name, 1, 1) AS first, 
COUNT(SUBSTR(first_name, 1, 1))
FROM hr.employees
HAVING COUNT(SUBSTR(first_name, 1, 1)) > 1
GROUP BY SUBSTR(first_name, 1, 1);
```

3. Выведите id департамента, з/п и количество сотрудников, которые работают в одном и том же департаменте и получают одинаковую зарплату
```SQL
SELECT department_id, salary, COUNT(*)
FROM hr.employees
GROUP BY department_id, salary
ORDER BY department_id;
```

4. Выведите день недели и количество сотрудников, которых приняли на работу в этот день
```sql
SELECT COUNT(*), TO_CHAR(hire_date, 'day') AS day
FROM hr.employees
GROUP BY  TO_CHAR(hire_date, 'day')
ORDER BY 1;
```

5. Выведите id департаментов, в которых работает больше 30 сотрудников и сумма их з/п-т больше 300000.
```sql
SELECT department_id, COUNT(*), SUM(SALARY)
FROM hr.employees
GROUP BY department_id
HAVING COUNT(*) > 30 AND SUM(salary) > 300000;
```

6. Из таблицы countries вывести все region_id, для которых сумма всех букв их стран больше 50ти.
```sql
SELECT region_id, COUNT(*)
FROM hr.countries
GROUP BY region_id
HAVING SUM(LENGTH(country_name)) > 50;
```

7. Выведите информацию о job_id и округленную среднюю зарплату работников для каждого job_id.
```sql
SELECT job_id, AVG(salary), COUNT(*)
FROM hr.employees
GROUP BY job_id;
```

8. Получить список id департаментов, в которых работают сотрудники нескольких (>1) job_id.
```sql
SELECT department_id, COUNT(job_id)
FROM hr.employees
GROUP BY department_id
HAVING COUNT(DISTINCT job_id) > 1;
```

9. Выведите информацию о department, job_id, максимальную и минимальную з/п для всех сочетаний department_id - job_id, где средняя з/п больше 10000.
```sql
SELECT department_id, job_id, MAX(SALARY), MIN(SALARY), COUNT(*)
FROM hr.employees
GROUP BY department_id, job_id
HAVING AVG(SALARY) > 10000;
```

10. Получить список manager_id, у которых средняя зарплата всех его подчиненных, не имеющих комиссионные, находится в промежутке от 6000 до 9000.
```sql
SELECT manager_id, AVG(salary)
FROM hr.employees
WHERE commission_pct IS NULL
GROUP BY manager_id
HAVING (AVG(SALARY) > 6000 AND AVG(SALARY) < 9000);
```

11. Выведите округлённую до тысяч (не тысячных) максимальную зарплату среди всех средних зарплат по департаментам.
```SQL
SELECT ROUND(MAX(AVG(salary)), -3)
FROM hr.employees
GROUP BY department_id;

---------------------------------------------------------------------------------------------------------------------------------------------------------
### HW_4 Join
1. Выведите информацию о регионах и количестве сотрудников в каждом регионе.

```sql
SELECT region_name, COUNT(*)
FROM hr.employees e
JOIN hr.departments d
    ON (hr.e.department_id = hr.d.department_id)
JOIN hr.locations l
    ON (hr.d.location_id = hr.l.location_id)
JOIN hr.countries c
    ON (hr.l.country_id = hr.c.country_id)
JOIN hr.regions r
    ON (c.region_id = r.region_id)
GROUP BY region_name;
```

2. Выведите детальную информацию о каждом сотруднике: имя, фамилия, название департамента, job_id, адрес, страна и регион
```sql
SELECT first_name, last_name, d.department_name, j.job_id, l.street_address, c.country_name, r.region_name
FROM hr.employees e
JOIN hr.departments d
    ON (e.department_id = d.department_id)
JOIN hr.locations l
    ON (d.location_id = l.location_id)
JOIN hr.countries c
    ON (l.country_id = c.country_id)
JOIN hr.regions r
    ON (c.region_id = r.region_id);
    
```

3. Выведите информацию о имени менеджеров которые имеют в подчинении больше 6 сотрудников, а также выведите количество сотрудников, которые им подчиняются
```SQL
SELECT emp2.first_name AS manager_name, COUNT(*)
FROM hr.employees emp1
JOIN hr.employees emp2
    ON (emp1.manager_id = emp2.employee_id)
   
GROUP BY emp2.first_name
HAVING COUNT(*) > 6
ORDER BY COUNT(*);
```


4. Выведите информацию о названии всех департаментов и о количестве работников, если в департаменте работают больше 30ти сотрудников. Используйте технологию «USING» для объединения по id департамента
```sql
SELECT department_id, COUNT(*)
FROM hr.employees e
JOIN hr.departments d
	USING (department_id)
GROUP BY department_id
HAVING COUNT(*) > 30;
```

5. Выведите названия всех департаментов, в которых нет ни одного сотрудника.
```sql
SELECT *
FROM hr.departments d
LEFT OUTER JOIN hr.employees e
ON (e.department_id = d.department_id)
WHERE e.department_id IS NULL;
```

6. Выведите всю информацию о сотрудниках, менеджеры которых устроились на работу в 2005ом году, но при это сами работники устроились на работу до 2005 года.
```sql
SELECT e1.first_name, e1.last_name, e1.employee_id, e1.manager_id
FROM hr.employees e1 /*employee */
JOIN hr.employees e2 /*manager */
ON (e1.employee_id = e2.manager_id)
WHERE TO_CHAR(e2.hire_date, 'fmyyyy') = '2005' 
AND e1.hire_date < TO_DATE('01-01-2005', 'DD-MM-YYYY')
ORDER BY first_name;

```

7. Выведите название страны и название региона этой страны, используя natural join.
```sql
SELECT *
FROM hr.regions
NATURAL JOIN hr.countries;
```

8. Выведите имена, фамилии и з/п сотрудников, которые получают меньше, чем (минимальная з/п по их специальности + 1000).
```sql
SELECT first_name, last_name, salary
FROM hr.employees e
JOIN hr.jobs j
	ON (e.job_id j.job_id AND salary < min_salary+1000);
```


9. Выведите уникальные имена и фамилии сотрудников, названия стран, в которых они работают. Также выведите информацию о сотрудниках, о странах которых нет информации. А также выведите все страны, в которых нет сотрудников компании.
```sql

SELECT DISTINCT first_name, last_name, c.country_name
FROM hr.employees e
FULL OUTER JOIN departments d ON (e.department_id = d.department_id)
FULL OUTER JOIN locations l ON (d.location_id = l.location_id)
FULL OUTER JOIN counties c ON (l.country_id = c.country_id);
```

10. Выведите имена и фамилии всех сотрудников, а также названия стран, которые мы получаем при объединении работников со всеми странами без какой-либо логики
```sql
SELECT first_name, last_name, country_name
FROM hr.employees
CROSS JOIN hr.countries;
```

11. Решите задачу № 1, используя Oracle Join синтаксис.
```sql
SELECT region_name, COUNT(*)
FROM hr.employees e, hr.departments d, hr.locations l, hr.countries c, hr.regions r
    WHERE hr.e.department_id = hr.d.department_id, 
    hr.d.location_id = hr.l.location_id
    hr.l.country_id = hr.c.country_id
    c.region_id = r.region_id
GROUP BY region_name;
```

--------------------------------------------------------------------------------------------------------------------------------------------------------
### HW_5 Subqueries
1. Выведите всю информацию о сотрудниках, с самым длинным именем.
```sql
SELECT *
FROM hr.employees e
where LENGTH(e.first_name) IN (select max(length(first_name)) from hr.employees);
```

2. Выведите всю информацию о сотрудниках, с зарплатой большей средней зарплаты всех сотрудников.
```sql
SELECT *
FROM hr.employees e
WHERE salary > (select avg(salary) from hr.employees)
ORDER BY salary;
```

3. Получить город/города, где сотрудники в сумме зарабатывают меньше всего
```sql
SELECT city, sum(salary)
FROM hr.employees emp 
JOIN hr.departments d ON emp.department_id=d.department_id 
JOIN hr.locations l ON d.location_id=l.location_id 
GROUP BY city
HAVING SUM(salary) IN 
                  ( select MIN(SUM(salary)) from hr.employees emp 
                  JOIN hr.departments d ON emp.department_id=d.department_id 
                  JOIN hr.locations l ON d.location_id=l.location_id 
                  group by city);
```

4. Выведите всю информацию о сотрудниках, у которых менеджер получает зарплату больше 15000.
```sql
SELECT *
FROM hr.employees
WHERE manager_id IN (SELECT employee_id FROM hr.employees WHERE salary > 15000);
```

5. Выведите всю информацию о департаментах, в которых нет ни одного сотрудника.
```sql
SELECT *
FROM hr.departments
WHERE department_id NOT IN (SELECT DISTINCT department_id FROM hr.employees WHERE department_id IS NOT NULL);
```


6. Выведите всю информацию о сотрудниках, которые не являются менеджерами.
   ```sql
SELECT first_name, last_name, manager_id
FROM hr.employees 
WHERE employee_id IN (SELECT employee_id FROM hr.employees where manager_id IS NULL);
```

7.  Выведите всю информацию о менеджерах, которые имеют в подчинении больше 6ти сотрудников.
```sql
SELECT *
FROM hr.employees
		(select count(*) from hr.employees )
```

8. Выведите всю информацию о сотрудниках, которые работают в департаменте с названием IT .
```sql
SELECT *
FROM hr.employees e
JOIN hr.departments d on e.department_id=d.department_id
WHERE d.department_name IN 'IT';
```

9. Выведите всю информацию о сотрудниках, менеджеры которых устроились на работу в 2005ом году, но при это сами работники устроились на работу до 2005 года.
```sql
SELECT *
FROM hr.employees
WHERE manager_id IN (SELECT employee_id from hr.employees
					 WHERE TO_CHAR(hire_date, 'yyyy') = '2005')
	AND hire_date < TO_DATE('01-01-2005', 'DD-MM-YYYY');
```

10. Выведите всю информацию о сотрудниках, менеджеры которых устроились на работу в январе любого года, и длина job_title этих сотрудников больше 15ти символов.
```sql
SELECT *
FROM hr.employees e
JOIN hr.jobs j ON (e.job_id=j.job_id)
WHERE manager_id IN (SELECT employee_id from hr.employees
					 WHERE TO_CHAR(hire_date, 'fmMonth') = 'January')
	AND LENGTH(j.job_title) > 15;
```
---------------------------------------------------------------------------------------------------------------------------------------------------------
### HW_6 Set operator
