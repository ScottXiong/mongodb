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
https://docs.mongodb.com/v3.4/tutorial/create-users/index.html
