# PostgresSQL
# Ödev 1
1:film tablosunda bulunan title ve description sütunlarındaki verileri sıralayınız.
```
select title, description from film order by title
```

Soru 2: film tablosunda bulunan tüm sütunlardaki verileri film uzunluğu (length) 60 dan büyük VE 75 ten küçük olma koşullarıyla sıralayınız.

```
select * from film where length>60 and length<75 
```

Soru 3: film tablosunda bulunan tüm sütunlardaki verileri rental_rate 0.99 VE replacement_cost 12.99 VEYA 28.99 olma koşullarıyla sıralayınız.

``` 
select * from film where rental_rate=0.99 and replacement_cost=12.99
```

Soru 4: customer tablosunda bulunan first_name sütunundaki değeri 'Mary' olan müşterinin last_name sütunundaki değeri nedir?
``` 
select last_name from customer where first_name='Mary'
``` 
Soru 5: film tablosundaki uzunluğu(length) 50 ten büyük OLMAYIP aynı zamanda rental_rate değeri 2.99 veya 4.99 OLMAYAN verileri sıralayınız.
``` 
SELECT *
FROM film
WHERE length <= 50
AND rental_rate NOT IN (2.99, 4.99)
``` 
# Ödev 2

Aşağıdaki sorgu senaryolarını dvdrental örnek veri tabanı üzerinden gerçekleştiriniz.

1.film tablosunda bulunan tüm sütunlardaki verileri replacement cost değeri 12.99 dan büyük eşit ve 16.99 küçük olma koşuluyla sıralayınız ( BETWEEN - AND yapısını kullanınız.)
   
      SELECT * FROM film WHERE replacement_cost BETWEEN 12.99 AND 16.99;
    
2.actor tablosunda bulunan first_name ve last_name sütunlardaki verileri first_name 'Penelope' veya 'Nick' veya 'Ed' değerleri olması koşuluyla sıralayınız. ( IN operatörünü kullanınız.)
   
     select first_name, last_name from actor where first_name IN ('Penelope', 'Nick' , 'Ed')
    
3.film tablosunda bulunan tüm sütunlardaki verileri rental_rate 0.99, 2.99, 4.99 VE replacement_cost 12.99, 15.99, 28.99 olma koşullarıyla sıralayınız. ( IN operatörünü kullanınız.)
   
     SELECT * FROM film WHERE rental_rate IN (0.99, 2.99, 4.99) AND replacement_cost IN (12.99, 15.99, 28.99)

# Ödev 3 

1.country tablosunda bulunan country sütunundaki ülke isimlerinden 'A' karakteri ile başlayıp 'a' karakteri ile sonlananları sıralayınız.
```
select country from country where country LIKE  'A%a'
```
2.country tablosunda bulunan country sütunundaki ülke isimlerinden en az 6 karakterden oluşan ve sonu 'n' karakteri ile sonlananları sıralayınız.
```
select country from country where country LIKE  '%_____n'
```
3.film tablosunda bulunan title sütunundaki film isimlerinden en az 4 adet büyük ya da küçük harf farketmesizin 'T' karakteri içeren film isimlerini sıralayınız.
```
select title from film where title ILIKE  '%____t'
```
4.film tablosunda bulunan tüm sütunlardaki verilerden title 'C' karakteri ile başlayan ve uzunluğu (length) 90 dan büyük olan ve rental_rate 2.99 olan verileri sıralayınız.
```
select * from film where title LIKE 'C%' and length > 90 and rental_rate=2.99
```

# Ödev 4
1.film tablosunda bulunan replacement_cost sütununda bulunan birbirinden farklı değerleri sıralayınız.
```
select DISTINCT replacement_cost from film
```
2.film tablosunda bulunan replacement_cost sütununda birbirinden farklı kaç tane veri vardır?
```
select count(DISTINCT replacement_cost) from film
```
3.film tablosunda bulunan film isimlerinde (title) kaç tanesini T karakteri ile başlar ve aynı zamanda rating 'G' ye eşittir?
```
select count(*) from film where title LIKE 'T%' and rating = 'G'
```
4.country tablosunda bulunan ülke isimlerinden (country) kaç tanesi 5 karakterden oluşmaktadır?
```
select country from country where length(country)= 5
```
5.city tablosundaki şehir isimlerinin kaç tanesi 'R' veya r karakteri ile biter?
```
select count(city) from city where city ILIKE '%R'
```

# Ödev 5
1.film tablosunda bulunan ve film ismi (title) 'n' karakteri ile biten en uzun (length) 5 filmi sıralayınız.
```
select title from film where title LIKE '%n'  ORDER BY length DESC  LIMIT 5;
```
2.film tablosunda bulunan ve film ismi (title) 'n' karakteri ile biten en kısa (length) ikinci(6,7,8,9,10) 5 filmi(6,7,8,9,10) sıralayınız.
```
SELECT title, length FROM film WHERE title LIKE '%n' ORDER BY length ASC LIMIT 5 OFFSET 5;

```
3.customer tablosunda bulunan last_name sütununa göre azalan yapılan sıralamada store_id 1 olmak koşuluyla ilk 4 veriyi sıralayınız.
```
SELECT * FROM customer WHERE store_id = 1 ORDER BY last_name DESC LIMIT 5;
```

# Ödev 6
1.film tablosunda bulunan rental_rate sütunundaki değerlerin ortalaması nedir?
```
select AVG(rental_rate) from film
```
2.film tablosunda bulunan filmlerden kaç tanesi 'C' karakteri ile başlar?
```
select count(title) from film where title LIKE 'C%'
```
3.film tablosunda bulunan filmlerden rental_rate değeri 0.99 a eşit olan en uzun (length) film kaç dakikadır?
```
select MAX(length) from film where rental_rate = 0.99
```
4.film tablosunda bulunan filmlerin uzunluğu 150 dakikadan büyük olanlarına ait kaç farklı replacement_cost değeri vardır?
```
select count(replacement_cost) from film where length>150
```

# Ödev 7
Aşağıdaki sorgu senaryolarını dvdrental örnek veri tabanı üzerinden gerçekleştiriniz.

1.film tablosunda bulunan filmleri rating değerlerine göre gruplayınız.
```
select rating from film group by rating 
```
2.film tablosunda bulunan filmleri replacement_cost sütununa göre grupladığımızda film sayısı 50 den fazla olan replacement_cost değerini ve karşılık gelen film sayısını sıralayınız.
```
SELECT replacement_cost, COUNT(*) AS film_count
FROM film
GROUP BY replacement_cost
HAVING COUNT(*) > 50;
```
3.customer tablosunda bulunan store_id değerlerine karşılık gelen müşteri sayılarını nelerdir? 
```
select store_id, count(customer_id) from customer group by store_id
```
4. city tablosunda bulunan şehir verilerini country_id sütununa göre gruplandırdıktan sonra en fazla şehir sayısı barındıran country_id bilgisini ve şehir sayısını paylaşınız. 
```
select country_id, count(*) as city_count, max(city) as sehir from city group by country_id order by city_count LIMIT 1
```
