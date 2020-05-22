# Week 3 — Asynchronous Programming

Asynchronous Code - The order in which events start may not be the order in which they finish

`setTimeout(function (x,y) {console.log(x-y); }, 3000);`

## Promise

```
let promise = new Promise(function(resolve, reject) {
  if (/* all good */) {
    resolve("All good");
  } else {
    reject(Error("Give me back my money!"));
  }
});

promise.then( (fromResolve) => {
  alert("Success :" + message);
|).catch( (fromReject) => {
  alert("Failed : " + error);
});

## Client & Servers

### Without AJAX
- Computer requests to server
- Server responds with HTML
- Page reloads
- Sidebar has 100s of thumbnails

### With AJAX
AJAX  = Asynchronous JavaScript and XML

XML = data format (usually html, json, text, xml)

### JQuery

Get
```
$.ajax( "some-url )
  .done(function(data) {
    alert("success");
  })
  .fail(function(error) {
    alert("error");
  })
```
 
Post
```
$.ajax({
  url: "some-url",
  method: 'POST',
  data: { key1: 'val1', key2: 'val2' }
  })
    .done(function(data) {
    alert("success");
  })
  .fail(function(error) {
    alert("error");
  })
  
### Connect to MySQL
```
const mysql = require('mysql2');
const pool = mysql.createPool({
                host: 'some-host-url',
                user: 'some-user-name',
                database: 'some-database-name',
                password: 'some-password'
              }).promise();
```

### Execute Queries
```
pool.execute('Select * from people')
  .then((data) => {
    let Data = data[0];
    for(let i=0; i < Data.length; i++) {
      console.log(Data[i].id);
      console.log(Data[i].name);
      console.log(Data[i].about);
      console.log(Data[i].imageURL);
    }
  })
  .catch((error) => console.log(error));
```

```
pool.execute('Select * from people')
  .then(([Data, Metadata]) => {
    for(let i=0; i < Data.length; i++) {
      console.log(Data[i].id);
      console.log(Data[i].name);
      console.log(Data[i].about);
      console.log(Data[i].imageURL);
    }
  })
  .catch((error) => console.log(error));
```
