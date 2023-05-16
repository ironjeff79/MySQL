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
<br>
<br> 
<br>

## 8.1.3&emsp;結果が一つに定まらないサブクエリー
### 错误❌例
### この場合には、LIKE述語という、曖昧な検索のための条件を使ったため、サブクエリーの結果が一つ定まらず、そのためにエラーが起こる。　　
### **通常、サブクエリーの結果は、一つ定まるように設定しなきゃいけない**
<br> 
<br>

select &emsp;*  
FROM &emsp;form1  
WHERE &emsp;code &emsp;=&emsp;  
&emsp;&emsp;(SELECT&emsp;code  
&emsp;&emsp;FROM&emsp;form2  
&emsp;&emsp;WHERE name LIKE '%xxx');
<br> 
<br>

### 正确✔例
select &emsp;*  
FROM &emsp;form1  
WHERE &emsp;code &emsp;IN&emsp;  
&emsp;&emsp;(SELECT&emsp;code  
&emsp;&emsp;FROM&emsp;form2  
&emsp;&emsp;WHERE name LIKE '%xxx');
<br>

### &emsp;＝演算子ではなくIN述語を使って値を比較すれば、エラーを避けることができる。
<br> 
<br>

## 8.2.2&emsp;サブクエリーのネスト
### 例 平均受注額を超える受注のあった得意先を検索する
<br>

select &emsp;T.client,&emsp;t.address,&emsp;t.phoneNum  
FROM &emsp;Client as T  
WHERE &emsp;T.client &emsp;IN&emsp;  
&emsp;&emsp;(SELECT&emsp;J.client  
&emsp;&emsp;FROM&emsp;order as J,&emsp;goods S  
&emsp;&emsp;WHERE J.code = S.code  
&emsp;&emsp;&emsp;AND  
&emsp;&emsp;&emsp;J.amount * S.price >  
&emsp;&emsp;&emsp;&emsp;(SELECT　AVG(J.amount * S.price)  
&emsp;&emsp;&emsp;&emsp;FROM&emsp;order as J,&emsp;goods S  
&emsp;&emsp;&emsp;&emsp;WHERE J.code = S.code ));

<br>
<br>

## 8.2.3&emsp;GROUP BY句和HAVING句的使用
### 例 全体の平均より平均受注数量が多い得意先を検索する
<br>

select &emsp;name,&emsp;AVG(amount)   
FROM &emsp;order  
GRUOP BY&emsp;name  
HAVING&emsp;AVG(amount)　＞　　  
&emsp;&emsp;(SELECT&emsp;AVG(amount)  
&emsp;&emsp;FROM&emsp;order);
<br>
<br>

## 8.3&emsp;相関サブクエリー(correlated subqueries)
### 相関サブクエリーは、特殊な性格を持つサブクエリーである。
### 相関サブクエリーでは、サブクエリーの外部の、本体のクエリーの要素をサブクエリーの中で使うことができる。そのため、相関サブクエリーを単独で実行することはできない。
<br>
<br>

### SQL---关联子查询（correlated subquery）
关联子查询和普通子查询的区别在于：
1. 关联子查询引用了外部查询的列。
2. 执行顺序不同。对于普通子查询，先执行普通子查询，再执行外层查询；而对于关联子查询，先执行外层查询，然后对所有通过过滤条件的记录执行内层查询。
3. 关联子查询不能单独运行
<br>
<br>

### 相関サブクエリーを使って、dressに対する受注を選び出す
<br>


select *  
from goods.order&emsp; B  
where 'dress'&emsp; =    
&emsp;&emsp;(select goodsname   
&emsp;&emsp;from goods.goods &emsp;as&emsp; A  
&emsp;&emsp;where A.idgoods&emsp; = &emsp;B.code)
<br>
<br>

## 8.4&emsp;EXISTS,ANY,ALL
### 8.4.1 EXISTS
### __existsの対象となるサブクエリーでは、「SELECT　*」を使っていること__
#### 通常のサブクエリーを扱う場合、EXISTSは、結果が存在するかどうかを一度しか評価しないが、相関サブクエリーを扱う場合は、それぞれの行について評価する。
<br>

### NOT  EXISTS
#### 例 没有被订购过的物品（NOT EXISTS & CORRELATED SUBQUERY）
<br>


select *  
from goods.goods&emsp; B  
where &emsp; NOT EXISTS    
&emsp;&emsp;(select *   
&emsp;&emsp;from goods.order &emsp;as&emsp; A  
&emsp;&emsp;where  B.idgoods&emsp; = &emsp;A.code);
<br>
<br>

### 8.4.2 ANY
### ANYは、比較演算子に従ってそれぞれの値を列の値と比較し、いずれかの値が条件を満たせば、全体の条件が成立したものとしてTRUEを返す

<br>

#### (ANY AND SUBQUERY)
select *    
from goods.order  
where date = ANY  
&emsp;&emsp;(select date  
&emsp;&emsp;from goods.order  
&emsp;&emsp;where name = 'TOM')

运行结果  
2021-10-01&emsp;&emsp;TOM&emsp;&emsp;3&emsp;&emsp;3  
2021-10-01&emsp;&emsp;BOB&emsp;&emsp; 6&emsp;&emsp;2  
2022-03-01&emsp;&emsp;TOM&emsp;&emsp;1&emsp;&emsp;5
<br>

*このようなanyの機能は、IN述語によく似ている  
しかし、IN述語は、複数の＝演算子のように機能するが、＝演算子以外の比較演算子の機能を持つことはできない。ANYでは、ほかの比較演算子を使うこともできる  
SOMEは、ANYとまったく同じ機能を持つキーワードである。ANYと同様に、いろいろな比較演算子を使うことができる*
<br>
<br>

### 8.4.3 ALL
### 选择的是除了TOM下订单的日期以外的所有日期
#### (<>ALL AND SUBQUERY)
select&emsp;*    
from &emsp;goods.order   
where date <> all  
&emsp;&emsp;(select&emsp;date  
&emsp;&emsp;from&emsp;goods.order   
&emsp;&emsp;where name = 'TOM')  
&emsp;&emsp;order by date

运行结果  
2022-04-15&emsp;&emsp;JEFF&emsp;&emsp;&emsp;5&emsp;&emsp;1  
2022-03-15&emsp;&emsp;ALICE&emsp;&emsp; 4&emsp;&emsp;1  
2022-01-01&emsp;&emsp;JEFF&emsp;&emsp;&emsp;2&emsp;&emsp;4
<br>


