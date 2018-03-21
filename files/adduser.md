```
use scott
db.createUser(
  {
    user: "",
    pwd: "",
    roles: [
       { role: "readWrite", db: "scott" }
    ]
  }
)
```
https://docs.mongodb.com/v3.4/tutorial/create-users/index.html
## 注意：写配置时一定要切换到英文输入法，并且用sublime编辑
