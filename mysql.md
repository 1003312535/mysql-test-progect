开发工具： sqlLyog









## mysql服务器

启动服务器

```js
net start 服务名
net stop 服务名

计算机-->管理--->服务
```

登录

```js
mysql -h 主机名 -p 端口号 -u root -p密码
//密码和-p之间不能加空格 ，其他随意
```



##### 分组 group by

```js
SELECT *, COUNT(age) num FROM test WHERE id = 1 GROUP BY age
```



##### 排序order by

```js
#按哪个字段哪种方式来进行排序
#ASC 或 DESC 升/降
SELECT * FROM menu  ORDER BY id DESC
```



##### 量表查询 union  / union all

```js
#UNION 只会选取不同的值。
SELECT country FROM Websites
UNION ALL
SELECT country FROM apps
ORDER BY country;

#使用 UNION ALL 来选取重复的值！
```



##### like

使用 AND 或者 OR 指定一个或多个条件。

```js
'%a'     //以a结尾的数据
'a%'     //以a开头的数据
'%a%'    //含有a的数据
'_a_'    //三位且中间字母是a的
'_a'     //两位且结尾字母是a的
'a_'     //两位且开头字母是a的
SELECT * FROM table1 WHERE name LIKE '%ren%'
```



##### 插入数据

```js
INSEART INTO table1 
(name,age,gender)
VALUE
('ren',18, '男');
```



##### 查询条件区分大小写（默认不区分）： BINARY 

```js
SELECT * from runoob_tbl WHERE BINARY runoob_author='RUNOOB.COM';
```

##### update跟新

```js
#不加条件（跟新整个表数据）
#加条件（跟新表中的某条/些数据）
UPDATE talbe1 SET name="age";
```

##### 删除表数据

```js
#不加条件（跟新整个表数据）
DELETE FROM table1
#加条件（跟新表中的某条/些数据）
DELETE FROM table1 WHERE name="age"
```

##### 链接数据库

```js
mysql -u root -p root
```

##### 创建数据库/表

```js
CREATE DATABASE database1
CREATE TABLE IF NOT EXISTS `TABLE1` (`name` INT AUTO_INCREMENT)
```

##### 删除数据库/表

```js
drop DATABASE database1
drop TABLE table1
```

##### 查看test 库中的表

```js
show tables from test
```

查看表结构

```js
desc test
```

###### 查看自己在那个库

```js
select database()
```

##### 查看数据库版本

```js
select version()
#或
mysql --version
```

## 规范

1. 不区分大小写（建议关键字大写、表明列名小写）
2. 每条命令用分号结尾
3. 可换行或缩进
4. 注释
   1. 单行： #注释文字
   2. 单行： -- 空格 注释文字

## dql语言（data query select language）

1. ```js
   select 100;
   select 100*100;
   select 'asd';
   select version();
   ```

2. #起别名

   ```js
   select 100 as num;
   #或
   select 100 num;
   select 100 'select num' //加单双引号
   ```

3. #去重

   ```js
   select distinct department_id from employees;
   ```

4. #拼接concat()

   ```js
   select concat(last_name, first_name) as name from employees;
   ```

5. #ifnull(字段，代替值)

   ```js
   select ifnull(commission_pct, 0) from employees
   ```

##### 条件查询

1. #逻辑表达式

   ```js
   
   && || ！ and or not
   select salary, last_name from where not(salary>=90 and salary<=100) or salary>= 12000;
   ```

2. #模糊查询

   ```js
   
   like 修饰符 % _
   select last_name from employees where last_name like '_\_%'
   #或 escape
   select last_name from employees where last_name like '_!_%' escape '!'
   
   between and
   select last_name from employees where salary
   between 100 and 200;
   
   in 判断某字段是否属于in 列表中的某一项 等价于or
   select * from employees where jog_id in('it_prot')
   
   is null 判断字段为空的
   select * form employees where commission_pct is null;
   is not null 判断字段不为空的
   select * from employees where commission_pct
   is not null
   ```

3. ```sejs
   #排序查询 order by 多重排序
   select salary from employees order by salary desc,employees_id asc;
   #按表达式排序
   select salary*12*(ifnull(commission_pct,0)) 年薪 from employees order by 年薪 desc;
   
   length() 字段字符集长度 汉字暂三个字节
   select length(last_name) from employees
   ```

4. ```js
   #upper() lower()
   select concat(upper(last_name), lower(first_name)) from employees
   ```

5. ```js
   #substr() substring() 地三个参数为长度 下标从1开始
   select substr('123456',2) from employees
   select substr('123456',2, 2) from employees
   ```

6. ```js
   #instr() 返回子串第一次出现的位置，找不到返回 0
   select instr(12345,2)
   ```

7. ```js
   #trim()
   select length(trim('   aaa  '))
   # trim( a from )
   select trim('a' from 'aaaaabbbbaaa')
   ```

8. ```js
   #lpad() 用指定的字符填充成指定的长度 当长度小于 字段长度时 截断截断截断
   select lpad(字段, 长度,'*')
   #rpad() 右填充 小于时还是左截断 左截断
   select rpad(字段, 10,'*')
   
   ```

9. 数学函数

10. ```js
    #round() 四舍五入
    select round(-1.55) //-2
    #小数点后两位
    select round(1.546,2) 
    #ceil 向上取整
    select ceil(-1.01) // -1
    #floor 向下取整
    select floor(-1.1) // -2
    #truncate() 截断 保留小数点后几位
    select truncate(1.24324,1)
    #mod 取余
    select mod(-10,-5)
    a-a/b*b
    看被除数 被除数为正 值为正 被除数为负 值为负
    ```

    

11. ```js
    now()
    curdata()
    curtime()
    year(now())
    month(new())
    str_to_data() 将日期格式的字符转换成指定格式的日期
    ```

12. 

    

## dml语言的学习（data manipulation language）

## ddl语言(data define language)

## tcl语言（transaction control language）

## 注意

1. `` ` 着重号， 一般表示字段 

2. `+`只有一个功能：

3. ```js
   #运算符 没有字符串拼接,如果一方时数字一方时字符，能转换的话就装成数值运算，不能就将字符转换成 0 计算
   select '100' + 1; #101
   select 'ren' + 1; # 0
   #一方为null 结果为 null
   select null + 1 # null
   ```

4. escape 'a' 代表 a转义字符的意思

5.  = 或 <> 不能判断 null 值 ， 可通过 is null 或 is not null 判断 或 <=>

6. <=> 安全等于  什么都可以判断

7. 索引都是 从 1 开始的

