# Dart wrapper library for the new Firebase

[![Build Status](https://travis-ci.org/Janamou/firebase3-dart.svg?branch=master)](https://travis-ci.org/Janamou/firebase3-dart)

This is an unofficial Dart wrapper library for the new [Firebase](https://firebase.google.com). 

You can find more information on how to use Firebase on [Getting started](https://firebase.google.com/docs/web/setup) page.

Don't forget to setup correct **rules** for your [realtime database](https://firebase.google.com/docs/database/security/) and/or [storage](https://firebase.google.com/docs/storage/security/) in Firebase console. 
Auth has to be also set in the Firebase console if you want to use it. For more info, see [next section](https://github.com/Janamou/firebase3-dart#before-tests-and-examples-are-run) in this document.

## Usage

### Installation

Install the library from the pub or Github.

### Include Firebase source

You must include the original Firebase JavaScript source into your `.html` file to be able to use the library.

```html
<script src="https://www.gstatic.com/firebasejs/3.5.0/firebase.js"></script>
```

### Use it

```dart
import 'package:firebase3/firebase.dart' as firebase;

void main() {
  firebase.initializeApp(
    apiKey: "YourApiKey",
    authDomain: "YourAuthDomain",
    databaseURL: "YourDatabaseUrl",
    storageBucket: "YourStorageBucket");
    
  Database database = firebase.database();
  DatabaseReference ref = database.ref("messages");  

  ref.onValue.listen((e) {
    DataSnapshot datasnapshot = e.snapshot;
    //Do something with datasnapshot
  });
  
  ...
}
```

## Examples

You can find more examples on realtime database, auth and storage in the [example](https://github.com/Janamou/firebase3-dart/tree/master/example) folder.

## Before tests and examples are run

You need to ensure a couple of things before tests and examples in this library are run.

### All tests and examples

Create `config.json` file (see `config.json.sample`) in `lib/src/assets` folder with configuration for your Firebase project.

> Warning: Use `config.json` for this package [development and testing only](https://github.com/Janamou/firebase3-dart/tree/master/lib/src/assets).

### App tests

No special action needed here.

### Auth tests and example

Auth tests and some examples need to have **Auth providers** correctly set. The following providers need to be enabled in Firebase console, `Auth/Sign-in method` section:

* E-mail/password
* Anonymous

### Database tests and example

Database tests and example need to have **public rules** to be able to read and write to database. Update your rules in Firebase console, `Database/Rules` section to:

```
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

> Warning: At the moment, anybody can read and write to your database. You *usually* don't want to have this in your production apps. You can find more information on how to setup correct database rules in the official [Firebase documentation](https://firebase.google.com/docs/database/security/). 

### Storage tests and example

Storage tests and example need to have **public rules** to be able to read and write to storage. Update your rules in Firebase console, `Storage/Rules` section to:

```
service firebase.storage {
  match /b/YOUR_STORAGE_BUCKET_URL/o {
    match /{allPaths=**} {
      allow read, write;
    }
  }
}
```

> Warning: At the moment, anybody can read and write to your storage. You *usually* don't want to have this in your production apps. You can find more information on how to setup correct storage rules in the official [Firebase documentation](https://firebase.google.com/docs/storage/security/). 


## Bugs

This is the first version of the library, the bugs may appear. If you find a bug, please create an [issue](https://github.com/Janamou/firebase3-dart/issues).

