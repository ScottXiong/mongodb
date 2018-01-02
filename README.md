# mongodb
多条件查询
- `db.students.find({"name":"scott"})`  `db.getCollection('students').find({})`
 `db.students.findOne({"name":"amandor","age":45})`
MongoDB提供了一组比较操作符：$lt/$lte/$gt/$gte/$ne，依次等价于</<=/>/>=/!=
- `db.students.find({"age":{"$gte":17, "$lte":99}})`
- `db.students.find({"name":{"$ne":"scott"}})`
- `db.students.find({"name":{"$in":["scott","amandor"]}})` //会检索出所有name为scott和amandor的用户
- `db.test.find({"name":{"$in":["stephen",123]}})` //$in 可以指定不同的数据类型
- `db.test.find({"name":{"$nin":["stephen2","stephen1"]}})` //$nin等同于SQL中的not in，同时也是$in的取反。如：
- `db.test.find({"$or": [{"name":"stephen1"}, {"age":35}]})`//$or等同于SQL中的or，$or所针对的条件被放到一个数组中，每个数组元素表示or的一个条件。--下面的示例等同于name = "stephen1" or age = 35
- `db.test.find({"$or": [{"name":{"$in":["stephen","stephen1"]}}, {"age":36}]})`//下面的示例演示了如何混合使用$or和$in。
- `db.test.find({"name": {"$not": {"$in":["stephen2","stephen1"]}}})` $not表示取反，等同于SQL中的not。

### null数据查询
- `db.test.find({"x":null})`  `db.students.find({"age":null})`
- ` db.test.find({"x": {"$in": [null], "$exists":true}})`//需要将null作为数组中的一个元素进行相等性判断，即便这个数组中只有一个元素。
    --再有就是通过$exists判断指定键是否存在。

### 正则
- db.students.find() //查询所有
- db.students.find({"name":/Scott/i}) //忽略大小写

### 数组查询
-  db.getCollection('students').find() 
-  db.getCollection('students').find({'like':'apple'}) //数组中所有包含banana的文档都会被检索出来
检索数组中需要包含多个元素的情况，这里使用$all。下面的示例中，数组中必须同时包含apple和banana，但是他们的顺序无关紧要。
-  `db.test.find({"fruit": {"$all": ["banana","apple"]}})` `db.getCollection('students').find({'like':{"$all":['apple','banana']}})`
下面的示例表示精确匹配，即被检索出来的文档，fruit值中的数组数据必须和查询条件完全匹配，即不能多，也不能少，顺序也必须保持一致。
- db.test.find({"fruit":["apple","banana","peach"]})
面的示例将匹配数组中指定下标元素的值。数组的起始下标是0。
- db.test.find({"fruit.2":"peach"})
可以通过$size获取数组的长度，但是$size不能和比较操作符联合使用
- db.test.find({"fruit": {$size : 3}})
如果需要检索size > n的结果，不能直接使用$size，只能是添加一个额外的键表示数据中的元素数据，在操作数据中的元素时，需要同时更新size键的值。

### [reference](http://blog.csdn.net/cw2004100021124/article/details/50150425)
