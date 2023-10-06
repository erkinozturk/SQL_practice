# SQL_practice

film tablosunda bulunan title ve description sütunlarındaki verileri sıralayınız.
```
SELECT title, description from film;
```

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

film tablosunda bulunan replacement_cost sütununda bulunan birbirinden farklı değerleri sıralayınız.
```
select distinct replacement_cost from film;
```

film tablosunda bulunan replacement_cost sütununda birbirinden farklı kaç tane veri vardır?
```
select count (replacement_cost) from film;
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
