# mongodb
多条件查询
- `db.students.find({"name":"scott"})` `db.students.findOne({"name":"amandor","age":45})`
MongoDB提供了一组比较操作符：$lt/$lte/$gt/$gte/$ne，依次等价于</<=/>/>=/!=
- `db.students.find({"age":{"$gte":17, "$lte":99}})`
- `db.students.find({"name":{"$ne":"scott"}})`
- `db.students.find({"name":{"$in":["scott","amandor"]}})` //会检索出所有name为scott和amandor的用户
- `db.test.find({"name":{"$in":["stephen",123]}})` //$in 可以指定不同的数据类型
- `db.test.find({"name":{"$nin":["stephen2","stephen1"]}})` //$nin等同于SQL中的not in，同时也是$in的取反。如：
- `db.test.find({"$or": [{"name":"stephen1"}, {"age":35}]})`//$or等同于SQL中的or，$or所针对的条件被放到一个数组中，每个数组元素表示or的一个条件。--下面的示例等同于name = "stephen1" or age = 35
- `db.test.find({"$or": [{"name":{"$in":["stephen","stephen1"]}}, {"age":36}]})`//下面的示例演示了如何混合使用$or和$in。
- `$not表示取反，等同于SQL中的not`
