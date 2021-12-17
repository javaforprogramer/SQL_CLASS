# SQL_CLASS
drop table kakeibo;

create table kakeibo(
 hiduke  date,
 himoku  varchar(20),
 memo    varchar(100),
 nyukin  integer,
 syukkin integer
);

insert into kakeibo values
('2018-02-03','食費','コーヒーを購入',0,380),
('2018-02-10','給料','1月の給料',280000,0),
('2018-02-11','教養娯楽費','書籍を購入',0,2800),
('2018-02-14','交際費','同期会の会費',0,5000),
('2018-02-18','水道光熱費','1月の電気代',0,7560);

3-1一円以上の出金があった行をすべて削除宇する------------------------------
delete from kakeibo where syukkin > 0;

3-2 正しいNULLの判定方法---------------------------------------------------
update kakeibo
	set syukkin = null
	where hiduke = '2018-02-10';
	
	

select * 
from kakeibo
	where syukkin is null;

update kakeibo
	set syukkin = 0
	where hiduke = '2018-02-10';

3-3 一月に関連する行を取得するselect文--------------------------------------

select * from kakeibo
	where memo like '%1%';
	11月がデータベースに存在すると参照してしまう
	
select * from kakeibo
	where memo like '_1';
Empty set (0.00 sec)
山田%（山田から始まる）
〇山田始
〇山田
×尾山田

山田_（山田の後に一文字必要）
〇山田一
×山田
×山田太郎

_ _ 山田　_ _

〇
２組 山田 13

3-4 100～3000円の出費を取得するSELECT文-----------------------------------------------------

select * from kakeibo
	where syukkin >= 100 and syukkin <= 3000;
	

select * from kakeibo
	where syukkin > 100 and syukkin < 3000;
	
3-5IN -----------------------------------------------------------------------------------------

select * from kakeibo
	where himoku in ('食費','交際費');

select * from kakeibo
	where himoku = '食費' or himoku = '交際費';
	
select * from kakeibo
	 where himoku not in ('食費','交際費');
	 
3-7 AND-----------------------------------------------------------------------------------------
create table minato_shopping(
 category varchar(10),
 name     varchar(50),
 shop     char(1),
 price    integer
);

insert into minato_shopping values
('ゲーム','スッキリ勇者クエスト','B',7140),
('ゲーム','スッキリ勇者クエスト','Y',6850),
('書籍','魔王征伐日記','A',1200),
('DVD','スッキリわかるマンモスの倒し方','A',5250),
('DVD','スッキリわかるマンモスの倒し方','B',7140);


update minato_shopping
	set price = 6100
	where name = 'スッキリ勇者クエスト'
	and shop = 'b';


update minato_shopping
	set price = 6100
	where name like '%勇者%'
	and shop = 'b';
	
3-8論理演算優先度---------------------------------------------------------------------------------------
select * from minato_shopping
	where shop = 'A'
	or shop = 'B'
	and category = 'ゲーム'
	or category = 'DVD';
	
3-9論理演算かっこ----------------------------------------------------------------------------------------
select * from minato_shopping
	where shop = 'A'
	or shop = 'B'
	and category = 'ゲーム'
	or category = 'DVD';
	
select * from minato_shopping
	where (shop = 'A'
	or shop = 'B')
	and (category = 'ゲーム'
	or category = 'DVD');
