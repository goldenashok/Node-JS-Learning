In Node.js, asynchronous errors are handled differently based on the async pattern used.
### 1. Using try...catch with async/await ✅
Node.js uses:

```
async function getUser() {
  try {
    const user = await fetchUser();
    console.log(user);
  } catch (err) {
    console.error("Error:", err.message);
  }
}
```
This is the most common and clean approach.
### 2.Handling Promise Rejections with .catch()
```
fetchUser()
  .then(user => console.log(user))
  .catch(err => console.error("Error:", err.message));
```

### 3.Error-First Callback Pattern
Many Node.js APIs use callbacks:

```
s.readFile("test.txt", (err, data) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(data.toString());
});
```
The first parameter is always the error object.
### 4. Global Unhandled Promise Rejections

```
process.on("unhandledRejection", (reason) => {
  console.error("Unhandled Rejection:", reason);
});
```
Useful as a safety net, but don't rely on it for normal error handling.
