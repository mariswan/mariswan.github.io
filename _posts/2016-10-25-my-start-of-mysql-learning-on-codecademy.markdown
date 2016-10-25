---
published: false
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

13. ／／


