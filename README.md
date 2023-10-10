# SQL_practice


## SELECT

film tablosunda bulunan title ve description sütunlarındaki verileri sıralayınız.
```
SELECT title, description from film;
```


## WHERE - AND - NOT

film tablosunda bulunan tüm sütunlardaki verileri film uzunluğu (length) 60 dan büyük VE 75 ten küçük olma koşullarıyla sıralayınız.
```
SELECT * FROM film WHERE length > 60 AND length < 75;
```

film tablosunda bulunan tüm sütunlardaki verileri rental_rate 0.99 VE replacement_cost 12.99 VEYA 28.99 olma koşullarıyla sıralayınız.
```
SELECT * FROM film WHERE rental_rate = 0.99 AND (replacement_cost = 12.99 OR replacement_cost = 28.99);
```

customer tablosunda bulunan first_name sütunundaki değeri 'Mary' olan müşterinin last_name sütunundaki değeri nedir?
```
SELECT last_name FROM Customer WHERE first_name = 'Mary';
```

film tablosundaki uzunluğu(length) 50 ten büyük OLMAYIP aynı zamanda rental_rate değeri 2.99 veya 4.99 OLMAYAN verileri sıralayınız.
```
SELECT * FROM film WHERE NOT length > 50 AND NOT (rental_rate = 2.99 OR rental_rate = 4.99);
```


## BETWEEN - IN

film tablosunda bulunan tüm sütunlardaki verileri replacement cost değeri 12.99 dan büyük eşit ve 16.99 küçük olma koşuluyla sıralayınız ( BETWEEN - AND yapısını kullanınız.)
```
select * from film where replacement_cost between 12.99 and 16.99;
```

actor tablosunda bulunan first_name ve last_name sütunlardaki verileri first_name 'Penelope' veya 'Nick' veya 'Ed' değerleri olması koşuluyla sıralayınız. ( IN operatörünü kullanınız.)
```
select first_name, last_name from actor where first_name in ('Penelope', 'Nick', 'Ed');
```

film tablosunda bulunan tüm sütunlardaki verileri rental_rate 0.99, 2.99, 4.99 VE replacement_cost 12.99, 15.99, 28.99 olma koşullarıyla sıralayınız. ( IN operatörünü kullanınız.)
```
select * from film where (rental_rate in (0.99,2.99,4.99)) and (replacement_cost in (12.99,15.99,28.99));
```


## LIKE - ILIKE

country tablosunda bulunan country sütunundaki ülke isimlerinden 'A' karakteri ile başlayıp 'a' karakteri ile sonlananları sıralayınız.
```
select country from country where country like 'A%a';
```

country tablosunda bulunan country sütunundaki ülke isimlerinden en az 6 karakterden oluşan ve sonu 'n' karakteri ile sonlananları sıralayınız.
```
select country from country where country like '%_____n';
```

film tablosunda bulunan title sütunundaki film isimlerinden en az 4 adet büyük ya da küçük harf farketmesizin 'T' karakteri içeren film isimlerini sıralayınız.
```
select title from film where title ilike '%t%t%t%t%';
```

film tablosunda bulunan tüm sütunlardaki verilerden title 'C' karakteri ile başlayan ve uzunluğu (length) 90 dan büyük olan ve rental_rate 2.99 olan verileri sıralayınız.
```
select * from film where (title like 'C%') and (length>90) and (rental_rate=2.99);
```


## DISTINCT - COUNT

film tablosunda bulunan replacement_cost sütununda bulunan birbirinden farklı değerleri sıralayınız.
```
select distinct replacement_cost from film;
```

film tablosunda bulunan replacement_cost sütununda birbirinden farklı kaç tane veri vardır?
```
select count (distinct replacement_cost) from film;
```

film tablosunda bulunan film isimlerinde (title) kaç tanesini T karakteri ile başlar ve aynı zamanda rating 'G' ye eşittir?
```
select count (*) from film where ((title like 'T%') and (rating ='G'));
```

country tablosunda bulunan ülke isimlerinden (country) kaç tanesi 5 karakterden oluşmaktadır?
```
select count (*) from country where country like '_____';
```

city tablosundaki şehir isimlerinin kaç tanesi 'R' veya r karakteri ile biter?
```
select count(*) from city where city ilike '%r';
```


## ORDER BY - LIMIT - OFFSET

film tablosunda bulunan ve film ismi (title) 'n' karakteri ile biten en uzun (length) 5 filmi sıralayınız.
```
select title from film where title like '%n' order by length limit 5;
```

film tablosunda bulunan ve film ismi (title) 'n' karakteri ile biten en kısa (length) ikinci(6,7,8,9,10) 5 filmi sıralayınız.
```
select title from film where title like '%n' order by length desc offset 5 limit 5;
```

customer tablosunda bulunan last_name sütununa göre azalan yapılan sıralamada store_id 1 olmak koşuluyla ilk 4 veriyi sıralayınız.
```
select * from customer where store_id=1 order by last_name desc limit 4; 
```


## Aggregate Function - MIN, MAX, SUM, AVG

film tablosunda bulunan rental_rate sütunundaki değerlerin ortalaması nedir?
```
select avg(rental_rate) from film;
```

film tablosunda bulunan filmlerden kaç tanesi 'C' karakteri ile başlar?
```
select count(title) from film where title like 'C%';
```

film tablosunda bulunan filmlerden rental_rate değeri 0.99 a eşit olan en uzun (length) film kaç dakikadır?
```
select max(length) from film where rental_rate=0.99;
```

film tablosunda bulunan filmlerin uzunluğu 150 dakikadan büyük olanlarına ait kaç farklı replacement_cost değeri vardır?
```
select count(distinct replacement_cost) from film where length>150;
```


## GROUP BY - HAVING

film tablosunda bulunan filmleri rating değerlerine göre gruplayınız.
```
select rating from film group by rating;
```

film tablosunda bulunan filmleri replacement_cost sütununa göre grupladığımızda film sayısı 50 den fazla olan replacement_cost değerini ve karşılık gelen film sayısını sıralayınız.
```
select replacement_cost, count(*) from film group by replacement_cost having count(*) > 50 order by replacement_cost;
```

customer tablosunda bulunan store_id değerlerine karşılık gelen müşteri sayılarını nelerdir? 
```
select store_id, count(*) from customer group by store_id order by store_id;
```

city tablosunda bulunan şehir verilerini country_id sütununa göre gruplandırdıktan sonra en fazla şehir sayısı barındıran country_id bilgisini ve şehir sayısını paylaşınız.
```
select country_id, count(city) from city group by country_id order by count(city) desc limit 1;
```


## CREATE - UPDATE - DELETE

test veritabanınızda employee isimli sütun bilgileri id(INTEGER), name VARCHAR(50), birthday DATE, email VARCHAR(100) olan bir tablo oluşturalım.
```
create table employee (id serial primary key, name varchar(50) not null, birthday date, email varchar(100));
```

Oluşturduğumuz employee tablosuna 'Mockaroo' servisini kullanarak 50 adet veri ekleyelim.
```
https://www.mockaroo.com/
```

Sütunların her birine göre diğer sütunları güncelleyecek 3 adet UPDATE işlemi yapalım.
```
update employee set name = 'Updated' where email like 'w%' returning *;
```
```
update employee set birthday = '2000-01-01' where email is null returning *;
```
```
update employee set email = 'Default' where birthday ='2000-01-01' returning *;
```

Sütunların her birine göre ilgili satırı silecek 3 adet DELETE işlemi yapalım.
```
delete from employee where birthday < '1920-01-01' returning *;
```
```
delete from employee where birthday is null returning *;
```
```
delete from employee where name ilike 'je%' returning *;
```


## INNER JOIN

city tablosu ile country tablosunda bulunan şehir (city) ve ülke (country) isimlerini birlikte görebileceğimiz INNER JOIN sorgusunu yazınız.
```
select city.city, country.country from city inner join country on city.city_id = country.country_id;
```

customer tablosu ile payment tablosunda bulunan payment_id ile customer tablosundaki first_name ve last_name isimlerini birlikte görebileceğimiz INNER JOIN sorgusunu yazınız.
```
select payment.payment_id, customer.first_name, customer.last_name from customer inner join payment on payment.customer_id = customer.customer_id;
```

customer tablosu ile rental tablosunda bulunan rental_id ile customer tablosundaki first_name ve last_name isimlerini birlikte görebileceğimiz INNER JOIN sorgusunu yazınız.
```
select rental.rental_id, customer.first_name, customer.last_name from customer inner join rental on customer.customer_id = rental.customer_id;
```
