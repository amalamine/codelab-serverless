# Serverless with IBM Cloud Functions: Codelab

## Your first Action, Trigger, and Sequence

1. Create a new action named current-time.js

```
function main(params) {
    var date = new Date();
    return {
      message: "Invoked at: " + date.toLocaleString(),
	    time: date.toLocaleString()
	   };
}
```

2. Create a new action named random-number.js

```
function main(params) {
	 return {
     value: Math.floor(Math.random()*900000),
	   time: params.time
   };
}
```


3. Create a new action named message.js

```
function main(params) {
  return {
    message: 'Generated ' + params.value + ' at ' + params.time
  };
}
```

4. Create an enclosing sequence for all 3 actions

5. Create and connect a periodic trigger named every-5-seconds for your sequence

```
*/5 * * * * *
```

---

## Serverless HTTP REST Endpoints
