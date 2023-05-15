## SQL
### 1.5&emsp;正規化
- 第1正規形　&emsp;&emsp;繰り返し現れる列がない
- 第2正規形　&emsp;&emsp;主キーとなる列の値が決まれば、ほかの列の値がおのず決まる
- 第3正規形　&emsp;&emsp;主キーとなる列以外の列の値によって、ほかの列の値が決まることではない（即在第二范式的基础上，消除了传递依赖。）
<br>
<br>

## 2.4.4&emsp;重複するデータの除外
### select DISTINCT xxx from xxx
<br>
<br>

## 3.1.5&emsp;剰余演算子
### select&emsp;name,amount,case amount,&emsp;amount % case amount &emsp;remain&emsp; FROM &emsp;  form1;
<br>

### Oracleでは、剰余演算を行う場合、MODという関数を使う。
### select&emsp; name,amount,case amount,&emsp;MOD(amount, case amount) &emsp;remain &emsp;FROM  form1;
<br>

### ACCESSでは
### select&emsp; name,amount,case amount,&emsp;amount&emsp; MOD&emsp; case amount &emsp;remain &emsp;FROM  form1;
<br>

## 3.3.5&emsp;NULL
- NULL値は、０ではない
- NULL値は、''(空白)ではない
- NULL値は、"(長さゼロの文字列)ではない
<br>
<br>

## 4.2&emsp;％ワイルドカード&emsp;&emsp;_ワイルドカード
### select * &emsp;FROM &emsp;form1 &emsp;WHERE &emsp; name &emsp; LIKE &emsp;'%E%' ;(模糊查找 百分号内字符无限制)

### select * &emsp;FROM &emsp;form1 &emsp;WHERE &emsp; name &emsp; LIKE &emsp;'E_'；(模糊查找 _代表任意一个字符)
- 可以使用多个_&emsp;　＇E＿＿＿y'&emsp;和&emsp;'E % y'&emsp;结果相同
- 也可以这样使用&emsp; 'E % y＿'

<br>
<br>

## 4.3&emsp; IN
- IN 操作符允许我们在 WHERE 子句中规定多个值。
### select * &emsp;FROM &emsp;form1 &emsp;WHERE &emsp; name  &emsp; IN &emsp;(TOM，JERRY，MIke)；
（相对于or比较简便）

<br>
<br>

## 4.4.2&emsp; INTERSECT

- 获取两个或多个查询的交集

select * &emsp;form1   
INTERSECT  
select * &emsp;form2;   
<br>
<br>

## 4.4.3&emsp; EXCEPT (Oracle里叫做MINUS)

- 用于从另一个结果集中减去一个结果集

select * &emsp;form1   
EXCEPT  
select * &emsp;form2;   
<br>
<br>

## 5.3.1&emsp;ABS関数 

- 用于从另一个结果集中减去一个结果集

select  &emsp;temperature, &emsp; ABS(temperature) &emsp; absolute value  
FROM form1;

<br>
<br>

## 5.3.2&emsp;CEIL関数&emsp;&&emsp;FLOOR関数
CEIL関数は、指定された数値以上の最小の整数を返す  
FLOOR関数は、指定された数値以下の最大の整数を返す　　
<br>
<br>

## 5.3.3&emsp;SIGN関数
SIGN関数は、指定された数値の正负の符号を調べる  
<br>
引数比0小的话返回-1，0的话返回0，比0大的话返回1  
Oracle是SIGN &emsp;&emsp;ACCESS是SGN 
<br>

### 正のデータだけを抜き出す
select  &emsp;temperature  
FROM form1;  
where &emsp;SIGN(temperature) = 1;
<br>
<br> 

## 6.3&emsp;ORDER BY
除了列名之外，列数也可以作为参数  
以下两句结果相同  
select &emsp;* &emsp; FROM form1; &emsp;ORDER BY&emsp;1;  
select &emsp;* &emsp; FROM form1; &emsp;ORDER BY&emsp;name;
<br> 
<br> 

- 默认以升序排列，如果想要降序排列的话  
select &emsp;* &emsp; FROM form1; &emsp;ORDER BY&emsp;name DESC;
<br>
<br> 

## 6.4&emsp;GROUP BY
GROUP BYを使うと、列の値に従って行をグループ化することができる。
GROUP BYは、指定された列の値が等しい行をまとめることによって、表をいくつかのグループに分ける。
<br>

select &emsp;sex,&emsp;sum(price) from&emsp; goods&emsp; group by&emsp; sex;
<br>

- GROUP BYに指定する列は、必ずしもselect句に指定する必要がない。
<br>
<br> 

## 6.5&emsp;HAVING
以下语句会报错  （WHEREの中で集計関数を使うことはできない）  
select &emsp;sex &emsp;AVG(price)  
FROM goods  
WHERE AVG(price) <200;  
GROUP BY sex;
<br>
<br> 

这时候就要用到HAVING  
select &emsp;sex &emsp;AVG(price)  
FROM goods  
GROUP BY sex
HAVING AVG(price) <200;  
<br>
<br> 

## 6.6&emsp;組み合わせ
FROMのあと、句の優先順位にしたがって、WHERE句、groupby句、HAVING句という順序で処理される。


SELECT NAME AVG(MIANJI/NUM)
FROM BIAGE
GROUP BY AREA
HAVING AVG(MIANJI/NUM) > 10;
<br>
<br> 

## 7.4&emsp;自己結合
### データの整合性をチェックするために役立つ
<br> 

select &emsp;F.ID, &emsp;F,NAME,  
&emsp;&emsp;&emsp;&emsp;S.ID,&emsp;S.NAME    
FROM &emsp;F,S  
WHERE &emsp;F.ID &emsp;=&emsp;S.ID  
&emsp;AND&emsp;F.NAME&emsp;<>&emsp;S.NAME;

<br>
<br> 

### 例：结合两表计算每个人的消费总量 按照总金额由高到低排序

select a.name,&emsp;sum(a.amount * b.price )orderprice  
 from goods.order as a,&emsp;goods.goods as b  
 where a.CODE = b.idgoods  
 group by a.name  
 order by orderprice desc


