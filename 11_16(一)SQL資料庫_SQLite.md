# 11/16(一)SQL資料庫_SQLite
###### tags: `龍哥`

## 資料庫
#### SQL注入
https://zhuanlan.zhihu.com/p/27131797

#### 資料庫伺服器
1. MySQL(PHP圈適用)，LAMP(linux Apache MySQL PHP) PHP圈子。免費開源
3. PostgreSQL(使用rails大推)
4. MSSQL
5. Oracle(要錢，有專業證照)

* 資料庫伺服器很多資料庫，資料庫裡面很多表格
* SQLlite不屬於資料庫伺服器，不支援true跟false，因此要透過adapter來轉譯語言

#### SQL(Structured Query Language)
* 特定領域的語言，設計來管理資料用

#### 資料庫型態
* Chart、VARCHAR
* 避免把圖片放在資料庫，可以放在AWS裡面的S3(專門放靜態頁面圖片)
* INT等同於INTEGER

###### CHAR與VARCHAR
* CHAR(10)，存放'abc'三個字，剩下7個填空白，適合用在固定長度
* VARCHAR(10)，存放'abc'三個字，就是存三個字再用1個byte存長度，適合用在存名字

#### 指令

##### <> 這個代表不等於

1. ###### Create
* 刪除資料庫 drop database awesome_db
* 刪除資料表 drop table
* 追加欄位 ALTER table heros ADD COLUMN super_power VARCHAR(10) 
上面等同於rail的 ADD COLUMN super_power VARCHAR(10)

2. ###### READ
* 檢視符合篩選條件的英雄 SELECT * from heroes WHERE hero_level = 'S';
* SELECT gender, age from heroes WHERE hero_level = upper('S') AND gender = 'F';
* 找出沒有填年齡的 SELECT * from heroes WHERE age = '' or age is NULL;
上面等同於rail的 Hero.where(age: nil)
* 找出符合關鍵字背心者 SELECT * from heroes WHERE name LIKE '%背心%';
上面等同於rail的 Hero.where("name like '%背心%'");
* 找出年齡區間 SELECT * from heroes WHERE age BETWEEN 10 AND 25 ;
* SELECT * from heroes WHERE hero_level = 'A' OR hero_level = 'S';
上面等同於rail的 Hero.where(hero_level: ['S', 'A'])
* SELECT * from heroes WHERE hero_level NOT in ('S');
上面等同於rail的 Hero.where.not(hero_level: ['S'])

3. ###### Update
* UPDATE heroes set age = 25 WHERE id = 10;
* UPDATE heroes SET hero_level = 'B', hero_rank = 101  where id = 35;

4. ###### Delete
* DELETE FROM heroes where hero_lavel = 's';
* SELECT count(*) FROM heroes WHERE hero_level = 'A';
--Hero.where(hero_level: 'A').count
--Hero.count(hero_level: 'A')
* SELECT avg(age) FROM heroes WHERE hero_level = 'S';
--Hero.where(hero_level: 'A').average(:age)
* ...MAX...

5. ###### 分組
* 依照篩選條件分組檢視
`SELECT hero_level,avg(age) FROM heroes WHERE age != '' GROUP by hero_level;`
* 挑出各類不同的類別
`SELECT DISTINCT danger_level FROM monsters;`

6. ###### 排序
* 依照某條件正向排序
```
SELECT * FROM heroes WHERE hero_level = 'S' ORDER by age;
```
--Hero.where(hero_level: 'S').order(:age)
* 依照某條件正向排序(只看三筆)
```
SELECT * FROM heroes WHERE hero_level = 'S' ORDER by age LIMIT 3;
```

* 依照某條件反向排序
```
SELECT * FROM heroes WHERE hero_level = 'S' ORDER by age DESC;
```

#### ER圖(entity Relationship)
* Primary Key與Forgien key為了維持資料的一致性
* primary key是某一個資料表的欄位，必須為獨一無二。不可重複、不可為NULL
* FK是某資料表的欄位，參照到另一個資料表的主鍵，用來確認該資料表的記錄跟被對照到的表格的資料是對得起來的

#### 交集

SELECT * FROM t1 LEFT join t2 on t1.username = t2.name;

#### 名詞定義

* DDL(Data Definition Language) 資料定義語言
* DDL(Data Manipulate Language) 資料操作語言
* DDL(Data Query Language) 資料查詢語言

### 11:54am