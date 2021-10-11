Cloud functions run in a NodeJS virtual machine with modified global variables and methods. The connect function is designed to work with a Postgresql database.
To get a cloud database up and running quickly, try [ElephantSQL](https://elephantsql.com).

# Samples
```js
// Connect to database, make a query, then send a response.
connect(env.connectionString)
let rows = await sql("select now()")
send(rows[0].now + '<br>User Agent: ' + getHeader('user-agent'))

// Proxy
let req = await fetch(query.url, {method: method, body: JSON.stringify(json)})
let response = await req.text()
send(response)
```
# Global Variables
```js
method:String // http method
env:Object // environmental variable object
query:Object // request query string variables
json:Object || :Null // uploaded json body, request header must include header: {'Content-Type': 'application/json'}
```
# Global Methods
```js
connect(postgresqlConnection:String)
sql(sql:String, sqlVariables:Array)
status(httpCode:Number)
getHeader(header:String)
send(response:Any) // Objects will automatically send with JSON headers
fetch(url:String, options:Object) // Mirrors client JS fetch function
```