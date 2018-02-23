# Serverless with IBM Cloud Functions: Codelab

## Your first Action, Trigger, and Sequence

1. Create a new action named current-time.js

```
function main(params) {
    return {
        value: Math.floor(Math.random() * 900000),
        time: params.time
    };
}
```

2. Create a new action named random-number.js

```
function main(params) {
    return {
        value: Math.floor(Math.random() * 900000),
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

### Install the Cloud Functions Plugin

```
bx plugin install Cloud-Functions -r Bluemix
```
_if you don't already have the Bluemix CLI installed, get it [here] (https://console.bluemix.net/docs/cli/reference/bluemix_cli/download_cli.html)_

### Create an instance of Cloudant

1. Go to the [IBM Cloud catalog] (https://console.bluemix.net/catalog/)
2. Choose [Cloudant NoSQL DB] (https://console.bluemix.net/catalog/services/cloudant-nosql-db), give it a name and click create
3. Go to the service credentials tab and create a new set of credentials. Save those credentials, we'll need them soon.
4. Click on the launch button to go to the Cloudant dashboard
5. Create a new database, give it a name

### Create your CRUD operations

1. Clone or download this github repository

```
git clone https://github.com/aamine0/in5-serverless.git
```

2. Make sure you're in the directory of the clone repo

```
cd in5-serverless
```

3. Login to IBM Cloud

```
bx login -a api.ng.bluemix.net -o <YOUR_ORG_NAME> -s <YOUR_SPACE_NAME>
```

4. Create a new package

```
bx wsk package create summit
```

5. Bind your Cloudant instance's url and database name to it

```
bx wsk package bind /<YOUR_ORG_NAME>_<YOUR_SPACE_NAME>/summit cloudantdb --param dbname <YOUR_DATABASE_NAME> --param url <YOUR_CLOUDANT_URL>
```

6. Create your create action

```
bx wsk action create /<YOUR_ORG_NAME>_<YOUR_SPACE_NAME>/summit/create create.js
```

7. Create your read action

```
bx wsk action create /<YOUR_ORG_NAME>_<YOUR_SPACE_NAME>/summit/read read.js
```

8. Create your update action

```
bx wsk action create /<YOUR_ORG_NAME>_<YOUR_SPACE_NAME>/summit/update update.js
```

9. Create your delete action

```
bx wsk action create /<YOUR_ORG_NAME>_<YOUR_SPACE_NAME>/summit/delete delete.js
```

10. Test your actions

Required input for each:

- delete: docid, docrev
- create: doc
- read: docid
- update: doc

### Create your APIs
