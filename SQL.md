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



