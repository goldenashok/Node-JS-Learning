In Express.js, both app.use() and app.get() are used to handle requests, but they serve different purposes.
# app.use()
Used to register middleware.

```
app.use((req, res, next) => {
  console.log('Middleware executed');
  next();
});
```
## Characteristics
  - Executes for all HTTP methods (GET, POST, PUT, DELETE, etc.).
  - Can run for every route or a specific path prefix.
  - Usually used for:
    - Logging
    - Authentication
    - Error handling
    - Parsing request bodies
    - Setting headers
### Example :

```
app.use('/api', (req, res, next) => {
  console.log('API request');
  next();
});
```

This middleware runs for:
```
GET    /api/users
POST   /api/users
PUT    /api/users/1
DELETE /api/users/1
```
# app.get()
Used to handle GET requests only.
```
app.get('/users', (req, res) => {
  res.send('Users List');
});
```

## Characteristics

  - Triggered only for HTTP GET.
  - Matches an exact route pattern.
  - Usually used to return data or pages.

```
app.get('/products', (req, res) => {
  res.json(products);
});
```
Runs only for:
GET /products

Not for:

POST /products
PUT /products
DELETE /products

Execution Order Example

```
app.use((req, res, next) => {
  console.log('Middleware');
  next();
});

app.get('/users', (req, res) => {
  console.log('GET Handler');
  res.send('Users');
});
```

Request:
GET /users

### Output: 

Middleware
GET Handler
