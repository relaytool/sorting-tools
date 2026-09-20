# Firebase Label Request Queue

This version adds:

- Worker screen
- Controller screen
- Live Firebase Realtime Database queue
- Multiple workers/devices
- XD9 / XD23 grouped-code parsing
- Multiple source PDFs
- Global copies
- PDF page extraction
- Request status updates

## 1. Create Firebase project

Go to the Firebase console and create a project.

Create a **Realtime Database**.

For the simple no-login version, use open rules while testing, then paste the rules from `firebase-rules.json` into:

Firebase Console -> Realtime Database -> Rules

This intentionally allows public read/write because this app was designed without authentication.

## 2. Add a Web App

In Firebase:

Project settings -> Your apps -> Web -> Register app.

Copy the Firebase configuration object.

Open `index.html` and replace:

```js
const firebaseConfig = {
    ...
};
```

with your project's actual configuration.

Make sure `databaseURL` is the URL of your Realtime Database.

## 3. Put on GitHub Pages

Upload:

- index.html
- firebase-rules.json

to your GitHub Pages repository.

## 4. Worker URL

Use:

```text
https://YOURNAME.github.io/YOURREPO/?mode=worker
```

Workers can open this from phones, tablets or PCs.

## 5. Controller URL

Use:

```text
https://YOURNAME.github.io/YOURREPO/?mode=controller
```

The controller PC selects the PDFs.

It does NOT upload the PDFs to Firebase.

The PDFs remain on the controller computer.

## 6. How it works

Worker:

```text
enter station
    ->
enter XD codes
    ->
SEND REQUEST
    ->
Firebase
```

Controller:

```text
Firebase live queue
    ->
select waiting requests
    ->
FIND WAITING REQUESTS
    ->
search local PDFs
    ->
mark found/not_found
    ->
GENERATE PDF
```

## 7. Code examples

```text
XD9 45,50,40
```

becomes:

```text
XD945
XD950
XD940
```

and:

```text
XD23 50,45,34
```

becomes:

```text
XD2350
XD2345
XD2334
```

Multiple XD groups can be entered together.

## Important

The open rules mean anyone who can access the Firebase database can potentially read/write the queue. This is intentional for the simple no-login version. If this ever becomes internet-facing beyond the intended workplace, add Firebase Authentication and proper rules.
