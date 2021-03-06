# NativeScript Temporary Key Storage

I wrote this simple plugin for my own use, and it works well for what it's intended for. It temporarily stores a key in an SQLCipher database. This database uses a random encryption key that is changed in a predefined period of time. The database will keep changing its key and so working for as long as the app is running. Once the app is killed by the user or the system, the user will need to provide its password again.

## Installation
Run:`npm i nativescript-temporary-key-storage`

## Usage
To use this plugin, you first need to require it:
```
const keyStorage = require("nativescript-temporary-key-storage").keyStorage;
const processDb = require("nativescript-temporary-key-storage").processDb;
```

Setting the key:
```
keyStorage(myKeyGoesHere, 9000);
```

Here we're calling the "keyStorage" function, passing two arguments. The first one is the key itself, and the second is the amount of time (milliseconds) you want the database to change its encryption key. 

Getting the key:
```
let mainKey = {key:""};
    let requestKey = new processDb();
    requestKey.getKey(); 
    setTimeout(function() { 
        mainKey.key = requestKey.returnKey();
         if (mainKey.key === ""){
       Do something here!
    } else {
      Do something else!
    }
    },0);    
```    
We need to request the key `requestKey.returnKey();` inside a setTimout function; otherwise, it will return nothing. We also need to check if any key was returned, and that's why we used `if (mainKey.key === "")` in our example. 
