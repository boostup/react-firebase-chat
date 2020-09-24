# React Firebase Super Chat

A simple fullstack chat demo with React and Firebase.

Watch on full [React Firebase Chat Tutorial](https://youtu.be/zQyrwxMPm88) on YouTube.

[Live demo](https://fireship-demos.web.app/)

---

## Running the chat locally on Ubuntu :

### 1) optional: install java on Ubuntu

run the command :
\$ `sudo apt-get install openjdk-8-jre`
(get instructions for other platforms or linux distros here => https://openjdk.java.net/install/ )

### 2) optional : install firebase cli

run the command :
\$ `npm install -g firebase-tools`

### 2) start the local firebase emulators for functions and firestore

run the following commands root directory :
\$ `cd functions`
\$ `firebase emulators:start`
(follow the wizard and say Yes to "install emulators now")

You should now see a confirmation in the terminal window that your emulators are running thanks to this table:

│ Emulator │ Host:Port │ View in Emulator UI │
├───────────┼────────────────┼─────────────────────────────────┤
│ Functions │ localhost:5001 │ http://localhost:4000/functions │
├───────────┼────────────────┼─────────────────────────────────┤
│ Firestore │ localhost:8080 │ http://localhost:4000/firestore │
├───────────┼────────────────┼─────────────────────────────────┤
│ Hosting │ localhost:5000 │ n/a

### 3) add the following lines of code in `src/App.js`

```
import "firebase/functions";
...
...
firebase.initializeApp("your config obj here")
...
...
firebase.functions().useFunctionsEmulator("http://localhost:5001");

var db = firebase.firestore();
if (window.location.hostname === "localhost") {
    db.settings({
        host: "localhost:8080",
        ssl: false,
    });
}
```

### 4) running the React App

- open a second terminal window to allow for the firebase emulators to continue running from their own terminal window
- from the new terminal window, running the following command :
  \$ `npm start`

### 5) using the chat app

#### Testing from the same computer

- access your [http://localhost:3000](http://localhost:3000) from 2 different browsers
- sign in as 2 different google users
- start chattin'

#### Testing from 2 different computers/devices

- could not manage it to work even by accessing the server local ip address, i.e. : http://192.168.1.19:3000, and having specified the following config in the `firebase.json` file :

```
    "firestore": {
      "host": "192.168.1.19",
      "port": "8080"
    },
    "functions": {
      "host": "192.168.1.19",
      "port": "5001"
    }
```

## Testing guide for Cloud Firestore functions and security rules

- Article : [Testing guide for Cloud Firestore functions and security rules](https://medium.com/swlh/testing-guide-for-cloud-firestore-functions-and-security-rules-39d9f3c92d99)
- [Companion GitHub repo](https://github.com/danahartweg/testing-cloud-firestore)
- Files relevant :
  - https://github.com/danahartweg/testing-cloud-firestore/blob/master/server/firebase.json
  - https://github.com/danahartweg/testing-cloud-firestore/blob/master/server/rules/firestore.rules
