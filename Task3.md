1. Покажите фамилию и имя клиентов из города Прага? 
```sql
SELECT FirstName, LastName 
    FROM customers 
    WHERE City = "Prague"
```
2. Покажите фамилию и имя клиентов у которых имя начинается букву M? Содержит символ "ch"?
```sql
SELECT FirstName, LastName 
    FROM customers 
    WHERE FirstName like 'M%'
SELECT FirstName, LastName 
    FROM customers 
    WHERE FirstName like '%ch%'
```
3. Покажите название и размер музыкальных треков в Мегабайтах?
```sql
SELECT Name, bytes / 1048576.0 as MB
    FROM tracks
```
4. Покажите фамилию и имя сотрудников кампании нанятых в 2002 году из города Калгари?
```sql
SELECT LastName, FirstName 
    FROM employees 
    WHERE city = "Calgary" 
    and HireDate >= date('2002-01-01')
	and HireDate < date('2003-01-01')
```
5. Покажите фамилию и имя сотрудников кампании нанятых в возрасте 40 лет и выше?
````sql
SELECT LastName, FirstName 
    FROM employees 
    WHERE date(HireDate, "-40 year") > date(BirthDate)
````
6. Покажите покупателей-американцев без факса?
```sql
SELECT * 
    FROM customers  
    WHERE Country = "USA"
    and Fax is NULL
```
7. Покажите канадские города в которые сделаны продажи в августе и сентябре месяце?
```sql
SELECT ShipCity 
    FROM sales  
    WHERE ShipCountry = "Canada" 
	and strftime("%m", SalesDate) in ("08", "09")
```
8. Покажите почтовые адреса клиентов из домена gmail.com?
```sql
SELECT Email   
    FROM customers 
    WHERE Email like "%gmail.com%"
```
9. Покажите сотрудников которые работают в кампании уже 18 лет и более?
```sql
SELECT *
    FROM employees 
    WHERE date("now", "-18 year") > date(HireDate)
```
10. Покажите в алфавитном порядке все должности в кампании?
```sql
SELECT DISTINCT Title 
    FROM employees 
    ORDER BY Title
```
11. Покажите в алфавитном порядке Фамилию, Имя и год рождения покупателей?
```sql
SELECT LastName, FirstName, Age 
    FROM customers 
    ORDER BY LastName, FirstName, Age
```
12. Сколько секунд длится самая короткая песня?
```sql
SELECT min(milliseconds)/1000.0 as Seconds
    FROM tracks
```
13. Покажите название и длительность в секундах самой короткой песни?
```sql
SELECT Name, min(milliseconds)/1000.0 as Seconds
    FROM tracks
```
14. Покажите средний возраст клиента для каждой страны?
```sql
SELECT Country, avg(Age) 
    FROM customers 
    GROUP BY Country
```
15. Покажите Фамилии работников нанятых в октябре?
```sql
SELECT LastName 
    FROM employees 
    WHERE strftime("%m", HireDate) = "10"
```
16. Покажите фамилию самого старого по стажу сотрудника в кампании?
```sql
SELECT LastName FROM employees 
    WHERE HireDate = (SELECT min(HireDate) FROM employees)
```