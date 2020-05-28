
# SQL 实战

## 查询员工职能只有“开发”，没有测试的员工(eid，name)

**题目：**

员工表 employee：

|eid|name|
|:-:|:-:|
|1|u1|
|2|u2|
|3|u3|
|4|u4|
|5|u5|

职能表 role：

|did|department|
|:-:|:-:|
|1|开发|
|2|测试|

中间表 relations：

|id|e_id|d_id|
|:-:|:-:|:-:|
|1|1|1|
|2|2|1|
|3|3|1|
|4|1|2|
|5|2|2|
|6|4|2|

**参考答案（未经测试）：**

```sql
SELECT
	eid,
	`name` 
FROM
	employee e
	INNER JOIN relations c ON e.eid = c.e_id
	INNER JOIN role d ON c.d_id = d.did 
WHERE
	(
	d.department = '开发' 
	AND e_id NOT IN ( SELECT e_id FROM relations c INNER JOIN role d ON c.d_id = d.did WHERE d.department = '测试' ) 
	);
```