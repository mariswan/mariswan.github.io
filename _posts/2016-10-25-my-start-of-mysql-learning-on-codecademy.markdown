---
published: true
title: My start of MySQL learning on Codecademy
layout: post
---
Why shall an Energy Engineering girl learn MySQL? It's not a complicated story to tell: I want to change, and taste the world of code to see if anything interesting.
So I'm just going to state what I learned from Codecademy.com, its quite easy to follow.

At the very first beginning, MySQL language is quite like normal talking that when u want to create a table, u just type CREATE TABLE, then follows the table name; when u want to get some information from the table, for example, 'age' from table 'information', u just type SELECT age FROM information, then u will see the thing u want.
Be careful about the BLOCK CHARACTERS, because it is said u will get fired if u type it in lowercase. I don't know, I don't have a job to get fired.
以下大写的语句都死MySQL的语言


lesson 1
1. ／显示表格information中的age信息／

   SELECT age FROM information;

2. ／创建一个表格celebs，三列分别是id, name, age,数据类型分别是INTEGER（整数），TEXT（文本）和INTEGER（整数）／

CREATE TABLE celebs (id INTEGER, name TEXT, age INTEGER); RUN, then u get:(wow how to insert a .jpg here)


3.／向上述建立的表格中输入数据／

INSERT INTO celebs (id, name, age) VALUES (1, 'Justin Bieber', 21);

/comments: the (1, 'Justin Bieber', 21), the first 1, is the index of this info row, so it cannot be repeated when u insert other information in this table celebs./

4. ／按照行输入信息，注意index不能重复／

INSERT INTO celebs (id, name, age) VALUES (2, 'Beyonce Knowles', 33); 

INSERT INTO celebs (id, name, age) VALUES (3, 'Jeremy Lin', 26); 

INSERT INTO celebs (id, name, age) VALUES (4, 'Taylor Swift', 26);

试了一下，index不接着从2开始，写3，4，5行不行，也是可以的，没有发现什么问题

5. /更新表格信息，把id是1的条目中的age更新为22，为什么都要换行呢，不是很明白，看看后面会不会清楚/

UPDATE celebs
SET age = 22
WHERE id = 1;

6.／在表格celebs中添加一列 twitter_handle, 格式为TEXT，在id, name, age,的右侧／

ALTER TABLE celebs ADD COLUMN twitter_handle TEXT; 

7. ／在上述添加的列 twitter_handle中添加信息，比如 在id为4的条目中，使其twitter_handle为 文本 @taylorswift13／

UPDATE celebs 
SET twitter_handle = '@taylorswift13' 
WHERE id = 4; 

8.／删掉 表格celebs中，twitter_handle值为空的条目／

DELETE FROM celebs WHERE twitter_handle IS NULL;

结果就是，除了twitter_handle有信息之外的行，都删掉了



lesson 2 表哥名字是movies

9.／选择多个列的信息，中间用逗号（comma）隔开即可／

SELECT name, imdb_rating FROM movies;

10.／显示genre中不重复的项，在关键字前面添加DISTINCT即可／

SELECT DISTINCT genre FROM movies;

11. ／表格movies中，显示imdb_rating大于8的信息，所有列，所以用＊表示／

 SELECT * FROM movies WHERE imdb_rating > 8;

comments: 符号用以下显示， =, !=, >, <, >=, <=

12.／显示所有信息中，名字name是Se_en形式的／

SELECT * FROM movies
WHERE name LIKE 'Se_en';

run的结果出来，name是Seven和Se7en的被过滤出来

13. ／过滤出name中含元素a或者man,注意单个字母和好几个字母的区别，单个‘％’，多个‘％ ％’／

SELECT * FROM movies
WHERE name LIKE 'a%';

SELECT * FROM movies
WHERE name LIKE '%man%';

14.／过滤出name从A开始到J之间的，首字母鉴于A和J之间的／

SELECT * FROM movies
WHERE name BETWEEN 'A' AND 'J';

／过滤year鉴于1990和2000之间的，含首尾数，数字INTEGER不用引号／
SELECT * FROM movies
WHERE year BETWEEN 1990 AND 2000;

／过滤出多重条件（交集）的，中间用AND连接，文本内容不要忘记加单引号‘’／
SELECT * FROM movies
WHERE year BETWEEN 1990 AND 2000
AND genre = 'comedy';

／过滤出并集，用OR连接／
SELECT * FROM movies
WHERE genre = 'comedy'
OR year < 1980;

15.／显示数据，用imdb_rating，降序DESC，升序ASC／

SELECT * FROM movies
ORDER BY imdb_rating DESC;

16. ／新添加LIMIT，LIMIT 3表示前三名，结果会显示3个／

SELECT * FROM movies
ORDER BY imdb_rating ASC
LIMIT 3;

Lesson 3 新换表格 fake_apps


17.／COUNT, 数一个表格一共有多少行／

SELECT COUNT(*) FROM fake_apps;


／数满足特定条件的行的数量，添加WHERE即可／

SELECT COUNT(*) FROM fake_apps
WHERE price = 0;


／按照price分组，查每组的数量／

SELECT price, COUNT(*) FROM fake_apps
GROUP BY price;



／添加一个附加条件／

SELECT price, COUNT(*) FROM fake_apps
WHERE downloads > 20000
GROUP BY price;

／算downloads的sum／

SELECT SUM(downloads) FROM fake_apps;



／通过category，算不同category的sum和／

SELECT category, SUM(downloads) FROM fake_apps
GROUP BY category;


／选择downloads中最大的数据，会呈现出一个数据，最大MAX，最小MIN／

SELECT MAX(downloads) FROM fake_apps;



／显示name, category, MAX(downloads), 按照category分类，显示各个category中最大值／

SELECT name, category, MAX(downloads) FROM fake_apps
GROUP BY category;


18.／计算downloads的平均值／

SELECT AVG(downloads) FROM
fake_apps;



／按照不同的price分类，计算平均值／


／得到的值，取两位小数／



／小数点后面保留0位，直接省略那个数／



lesson 4 multi-table
两个表格中，共通的是第一个的artist_id(是第一个表格的foreign key,而不是primary key,可以重复，第二个表格的id是primary key, 不可重复)

19.／看看 PRIMARY KEY怎么用／

CREATE TABLE artists(id INTEGER PRIMARY KEY, name TEXT);

20.／包含不同的两个表格的数据，结果显示是将两个表结合起来，不是一个可用的结果 ／

SELECT albums.name, albums.year, artists.name FROM albums, artists;



／有效结合数据，对应起来，JOIN语句和ON结合的使用，JOIN前面的是包含FOREIGN KEY的表格／
SELECT * FROM albums JOIN artists ON albums.artist_id = artists.id;



／LEFT JOIN ON的用法，把id对应不上的为NULL的也包含在新的表格里／
SELECT * FROM albums LEFT JOIN artists ON albums.artist_id = artists.id;


／新添加内容是，AS的使用方法：在新的列表里将原来筛选出来的数据重新命名列，要加text的单引号‘’／

SELECT
  albums.name AS 'Album',
  albums.year,
  artists.name AS 'Artist'
FROM
  albums
JOIN artists ON
  albums.artist_id = artists.id
WHERE
  albums.year > 1980;




end of the initial learning for free.
