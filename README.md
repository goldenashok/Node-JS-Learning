# Node-JS-Learning
What is node.js?

Node JS is a JavaScript runtime environment that allows you to run JavaScript code outside of a web browser.

JavaScript only ran in web browsers. Node.js lets you run JavaScript on servers, computers, and other devices
It's built on Chrome's V8 JavaScript engine, which makes it fast and efficient

Common uses:
Building web servers and APIs
Creating command-line tools
Developing backend services
Building full-stack applications (using JavaScript for both frontend and backend)
Automation scripts and build tools

Key features:
Asynchronous and event-driven: It can handle many operations at once without blocking, making it good for real-time applications
NPM (Node Package Manager): Comes with access to hundreds of thousands of free, reusable code packages
Single language: Lets developers use JavaScript for both client-side and server-side code


Example 
```javascript
const http = require('http');
http.createServer((req, res) => {
  res.write('Hello World!');
  res.end();
}).listen(3000);
```

Why we need to use node?

Before Node.js, if you wanted to build a web application, you had to use different programming languages for different parts:
Frontend (browser): JavaScript
Backend (server): PHP, Ruby, Python, Java, etc.
This meant developers needed to know multiple languages and switch between them constantly.

Why We Need Node.js
1. JavaScript Everywhere
Write both frontend and backend in the same language
Share code between client and server
Easier for developers to work on the full stack
2. High Performance for Real-Time Applications
Handles many simultaneous connections efficiently
Perfect for chat apps, live notifications, collaborative tools, gaming servers
Non-blocking I/O means it doesn't wait around for slow operations (like database queries)
3. Fast Development
Huge ecosystem with NPM (over a million packages)
Don't reinvent the wheel - reuse existing solutions
Rapid prototyping and development
4. Scalability
Built to handle thousands of concurrent connections
Used by Netflix, LinkedIn, PayPal, Uber, and many large companies
Microservices architecture friendly
5. Modern Development Needs
APIs and RESTful services
Single Page Applications (SPAs)
WebSockets and real-time features
Streaming data



### What is express js?

Express.js web application framework for Node.js that makes building web servers and APIs much easier and faster.


It simplifies common web development tasks that would be tedious to write from scratch in plain Node.js:

**1. Routing** - Handling different URLs
```javascript
app.get('/', (req, res) => {
  res.send('Home page');
});

app.get('/about', (req, res) => {
  res.send('About page');
});
```

**2. Middleware** - Processing requests before they reach your routes
- Authentication checks
- Logging
- Parsing incoming data (JSON, forms, etc.)

**3. Request/Response Handling** - Easy access to:
- URL parameters
- Query strings
- Form data
- Headers and cookies

**4. Template Rendering** - Serving HTML pages dynamically

## **Why Use Express?**

- **Minimal and flexible** - Not bloated, you add what you need
- **Industry standard** - Most popular Node.js framework
- **Huge community** - Tons of tutorials, plugins, and support
- **Fast development** - Write less code to accomplish more

## **Simple Comparison**

**Plain Node.js** (verbose):

**Plain Node.js** (verbose):
```javascript
const http = require('http');
const server = http.createServer((req, res) => {
  if (req.url === '/' && req.method === 'GET') {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end('Home page');
  } else if (req.url === '/about' && req.method === 'GET') {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end('About page');
  }
});
server.listen(3000);
```


**With Express** (clean and simple):

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => res.send('Home page'));
app.get('/about', (req, res) => res.send('About page'));

app.listen(3000);
```

### Different type of router in express?

## **1. Basic Routing (All in One File)**

Everything in your main app file - fine for small apps:

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => res.send('Home'));
app.get('/about', (req, res) => res.send('About'));
app.get('/contact', (req, res) => res.send('Contact'));

app.listen(3000);
```

## **2. Express Router (Modular Routing)**

For larger apps, split routes into separate files using `express.Router()`:

**Main app file (app.js):**
```javascript
const express = require('express');
const app = express();

const userRoutes = require('./routes/users');
const productRoutes = require('./routes/products');

app.use('/users', userRoutes);
app.use('/products', productRoutes);

app.listen(3000);
```

**routes/users.js:**
```javascript
const express = require('express');
const router = express.Router();

// Matches: /users
router.get('/', (req, res) => {
  res.send('List of users');
});

// Matches: /users/:id
router.get('/:id', (req, res) => {
  res.send(`User ${req.params.id}`);
});

// Matches: /users (POST)
router.post('/', (req, res) => {
  res.send('Create user');
});

module.exports = router;
```

**routes/products.js:**
```javascript
const express = require('express');
const router = express.Router();

// Matches: /products
router.get('/', (req, res) => {
  res.send('List of products');
});

// Matches: /products/:id
router.get('/:id', (req, res) => {
  res.send(`Product ${req.params.id}`);
});

module.exports = router;
```

## **3. Route Parameters**

Different ways to capture dynamic values in URLs:

```javascript
// Simple parameter
app.get('/users/:id', (req, res) => {
  res.send(`User ID: ${req.params.id}`);
});

// Multiple parameters
app.get('/users/:userId/posts/:postId', (req, res) => {
  res.send(`User ${req.params.userId}, Post ${req.params.postId}`);
});

// Optional parameter
app.get('/posts/:id?', (req, res) => {
  if (req.params.id) {
    res.send(`Post ${req.params.id}`);
  } else {
    res.send('All posts');
  }
});
```

## **4. HTTP Method Routing**

Different routes for different HTTP methods:

```javascript
const router = express.Router();

router.get('/products', getAllProducts);      // GET
router.post('/products', createProduct);      // POST
router.put('/products/:id', updateProduct);   // PUT
router.delete('/products/:id', deleteProduct);// DELETE

// Or chain them:
router.route('/products')
  .get(getAllProducts)
  .post(createProduct);

router.route('/products/:id')
  .get(getProduct)
  .put(updateProduct)
  .delete(deleteProduct);
```

## **5. Nested Routers**

Routers within routers for complex structures:

```javascript
// routes/api.js
const express = require('express');
const router = express.Router();

const usersRouter = require('./users');
const postsRouter = require('./posts');

router.use('/users', usersRouter);
router.use('/posts', postsRouter);

module.exports = router;

// In main app:
app.use('/api', apiRouter);
// Now you have: /api/users, /api/posts, etc.
```

## **6. Route with Middleware**

Apply middleware to specific routes:

```javascript
const checkAuth = (req, res, next) => {
  if (req.isAuthenticated) {
    next();
  } else {
    res.status(401).send('Unauthorized');
  }
};

// Single route with middleware
router.get('/dashboard', checkAuth, (req, res) => {
  res.send('Dashboard');
});

// Multiple routes with middleware
router.use(checkAuth); // All routes below need auth
router.get('/profile', (req, res) => res.send('Profile'));
router.get('/settings', (req, res) => res.send('Settings'));
```

## **Best Practice Structure**

For a real project:
```
project/
├── app.js (main file)
├── routes/
│   ├── index.js (home routes)
│   ├── users.js
│   ├── products.js
│   └── api/
│       ├── v1/
│       │   ├── users.js
│       │   └── products.js
├── controllers/ (route handlers)
└── middleware/ (auth, validation, etc.)
```

### Router in Depth

## **1. Basic Route Structure**

```javascript
app.METHOD(PATH, HANDLER)
```

- **METHOD**: HTTP method (get, post, put, delete, etc.)
- **PATH**: Route path/pattern
- **HANDLER**: Function executed when route matches

```javascript
app.get('/users', (req, res) => {
  res.send('GET users');
});
```

## **2. Route Methods**

All HTTP methods are supported:

```javascript
app.get('/users', (req, res) => { });      // GET
app.post('/users', (req, res) => { });     // POST
app.put('/users/:id', (req, res) => { });  // PUT
app.patch('/users/:id', (req, res) => { });// PATCH
app.delete('/users/:id', (req, res) => { });// DELETE
app.all('/secret', (req, res) => { });     // ALL methods
```

**app.all()** - Matches all HTTP methods:

```javascript
// Runs for GET, POST, PUT, DELETE, etc.
app.all('/api/*', (req, res, next) => {
  console.log('API accessed');
  next();
});
```

## **3. Route Paths**

### **String Paths**

```javascript
// Exact match
app.get('/about', (req, res) => {
  res.send('About page');
});

// Root route
app.get('/', (req, res) => {
  res.send('Home');
});
```

### **String Patterns (Special Characters)**

```javascript
// ? makes preceding character optional
app.get('/ab?cd', handler);
// Matches: /acd, /abcd

// + means one or more of preceding character
app.get('/ab+cd', handler);
// Matches: /abcd, /abbcd, /abbbcd

// * means anything can go here
app.get('/ab*cd', handler);
// Matches: /abcd, /abXYZcd, /ab123cd

// () for grouping
app.get('/ab(cd)?e', handler);
// Matches: /abe, /abcde
```

### **Regular Expression Paths**

```javascript
// Anything with 'a' in the route
app.get(/a/, handler);
// Matches: /about, /contact, /api

// Routes ending with 'fly'
app.get(/.*fly$/, handler);
// Matches: /butterfly, /dragonfly

// Specific pattern
app.get(/^\/users\/\d+$/, handler);
// Matches: /users/123, /users/456
// Doesn't match: /users/abc
```

## **4. Route Parameters**

### **Basic Parameters**

```javascript
// Single parameter
app.get('/users/:userId', (req, res) => {
  res.send(`User ID: ${req.params.userId}`);
});
// /users/123 → userId = "123"

// Multiple parameters
app.get('/users/:userId/posts/:postId', (req, res) => {
  const { userId, postId } = req.params;
  res.send(`User ${userId}, Post ${postId}`);
});
// /users/5/posts/10 → userId = "5", postId = "10"
```

### **Optional Parameters**

```javascript
app.get('/users/:id?', (req, res) => {
  if (req.params.id) {
    res.send(`User ${req.params.id}`);
  } else {
    res.send('All users');
  }
});
// Matches: /users AND /users/123
```

### **Parameter Patterns**

```javascript
// Only numeric IDs
app.get('/users/:id(\\d+)', (req, res) => {
  res.send(`User ${req.params.id}`);
});
// Matches: /users/123
// Doesn't match: /users/abc

// Specific format
app.get('/files/:name.:ext', (req, res) => {
  res.send(`File: ${req.params.name}.${req.params.ext}`);
});
// /files/photo.jpg → name="photo", ext="jpg"
```

### **Wildcard Parameters**

```javascript
// Catch-all parameter
app.get('/files/*', (req, res) => {
  res.send(`Path: ${req.params[0]}`);
});
// /files/docs/2024/report.pdf → params[0] = "docs/2024/report.pdf"
```

## **5. Query Parameters**

```javascript
app.get('/search', (req, res) => {
  const { q, page, limit } = req.query;
  res.json({
    query: q,
    page: page || 1,
    limit: limit || 10
  });
});
// /search?q=express&page=2&limit=20
// req.query = { q: 'express', page: '2', limit: '20' }
```

## **6. Route Handlers**

### **Single Handler**

```javascript
app.get('/user', (req, res) => {
  res.send('User info');
});
```

### **Multiple Handlers (Middleware Chain)**

```javascript
const checkAuth = (req, res, next) => {
  if (req.headers.authorization) {
    next(); // Continue to next handler
  } else {
    res.status(401).send('Unauthorized');
  }
};

const getUser = (req, res) => {
  res.send('User data');
};

// Multiple handlers
app.get('/profile', checkAuth, getUser);
```

### **Array of Handlers**

```javascript
const logRequest = (req, res, next) => {
  console.log('Request logged');
  next();
};

const validateData = (req, res, next) => {
  console.log('Data validated');
  next();
};

const sendResponse = (req, res) => {
  res.send('Success');
};

app.post('/data', [logRequest, validateData, sendResponse]);
```

### **Combination of Functions and Arrays**

```javascript
app.get('/complex', 
  middleware1,
  [middleware2, middleware3],
  middleware4,
  finalHandler
);
```

## **7. Express Router**

### **Basic Router**

```javascript
// routes/users.js
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
  res.send('All users');
});

router.get('/:id', (req, res) => {
  res.send(`User ${req.params.id}`);
});

router.post('/', (req, res) => {
  res.send('Create user');
});

module.exports = router;

// app.js
const userRoutes = require('./routes/users');
app.use('/users', userRoutes);
```

### **Router with Middleware**

```javascript
const router = express.Router();

// Middleware for all routes in this router
router.use((req, res, next) => {
  console.log('Router middleware');
  next();
});

// Middleware for specific routes
router.use('/:id', (req, res, next) => {
  console.log(`ID param: ${req.params.id}`);
  next();
});

router.get('/:id', (req, res) => {
  res.send('User details');
});
```

### **Router Parameters Middleware**

```javascript
// Runs whenever :userId is in the route
router.param('userId', (req, res, next, id) => {
  // Fetch user from database
  req.user = { id: id, name: 'John' }; // Simulated
  next();
});

router.get('/users/:userId', (req, res) => {
  res.json(req.user); // User already loaded by param middleware
});

router.get('/users/:userId/posts', (req, res) => {
  res.json({ user: req.user, posts: [] });
});
```

### **Nested Routers**

```javascript
// routes/api/index.js
const express = require('express');
const router = express.Router();

const usersRouter = require('./users');
const postsRouter = require('./posts');

router.use('/users', usersRouter);
router.use('/posts', postsRouter);

module.exports = router;

// app.js
const apiRouter = require('./routes/api');
app.use('/api/v1', apiRouter);

// Results in:
// /api/v1/users
// /api/v1/posts
```

## **8. Route Chaining**

```javascript
// Instead of:
app.get('/book', getBooks);
app.post('/book', createBook);
app.put('/book', updateBook);

// Use route chaining:
app.route('/book')
  .get(getBooks)
  .post(createBook)
  .put(updateBook);

// With parameters:
app.route('/book/:id')
  .get(getBook)
  .put(updateBook)
  .delete(deleteBook);
```

## **9. Advanced Routing Patterns**

### **RESTful API Structure**

```javascript
const router = express.Router();

// Collection routes
router.route('/users')
  .get(getAllUsers)      // GET /users
  .post(createUser);     // POST /users

// Resource routes
router.route('/users/:id')
  .get(getUser)          // GET /users/:id
  .put(updateUser)       // PUT /users/:id
  .delete(deleteUser);   // DELETE /users/:id

// Nested resources
router.route('/users/:userId/posts')
  .get(getUserPosts)     // GET /users/:userId/posts
  .post(createUserPost); // POST /users/:userId/posts

router.route('/users/:userId/posts/:postId')
  .get(getUserPost)      // GET /users/:userId/posts/:postId
  .put(updateUserPost)   // PUT /users/:userId/posts/:postId
  .delete(deleteUserPost);// DELETE /users/:userId/posts/:postId
```

### **Versioned API Routes**

```javascript
// routes/v1/users.js
const router = express.Router();
router.get('/', (req, res) => {
  res.json({ version: 'v1', users: [] });
});
module.exports = router;

// routes/v2/users.js
const router = express.Router();
router.get('/', (req, res) => {
  res.json({ version: 'v2', users: [], meta: {} });
});
module.exports = router;

// app.js
app.use('/api/v1/users', require('./routes/v1/users'));
app.use('/api/v2/users', require('./routes/v2/users'));
```

### **Conditional Routing**

```javascript
const router = express.Router();

router.get('/users/:id', (req, res, next) => {
  if (req.params.id === 'me') {
    // Handle current user
    res.json({ user: 'current user' });
  } else {
    // Pass to next handler
    next();
  }
}, (req, res) => {
  // Handle specific user ID
  res.json({ user: req.params.id });
});
```

## **10. Error Handling in Routes**

### **Route-Level Error Handling**

```javascript
app.get('/users/:id', async (req, res, next) => {
  try {
    const user = await getUserById(req.params.id);
    if (!user) {
      return res.status(404).json({ error: 'User not found' });
    }
    res.json(user);
  } catch (error) {
    next(error); // Pass to error handler
  }
});

// Error handler
app.use((err, req, res, next) => {
  console.error(err);
  res.status(500).json({ error: 'Something went wrong' });
});
```

### **404 Handler (Must be last)**

```javascript
// All your routes here...

// 404 handler - catches unmatched routes
app.use((req, res) => {
  res.status(404).json({
    error: 'Route not found',
    path: req.path
  });
});
```

## **11. Route Organization Best Practices**

### **Project Structure**

```
project/
├── app.js
├── routes/
│   ├── index.js          // Main router
│   ├── auth.js           // Authentication routes
│   ├── users.js          // User routes
│   ├── posts.js          // Post routes
│   └── api/
│       ├── v1/
│       │   ├── index.js
│       │   ├── users.js
│       │   └── posts.js
│       └── v2/
│           ├── index.js
│           └── users.js
├── controllers/          // Route handlers
│   ├── userController.js
│   └── postController.js
├── middleware/
│   ├── auth.js
│   └── validate.js
└── models/
```

### **Separation of Concerns**

```javascript
// controllers/userController.js
exports.getAllUsers = async (req, res) => {
  const users = await User.find();
  res.json(users);
};

exports.getUser = async (req, res) => {
  const user = await User.findById(req.params.id);
  res.json(user);
};

// routes/users.js
const express = require('express');
const router = express.Router();
const userController = require('../controllers/userController');
const auth = require('../middleware/auth');

router.get('/', auth, userController.getAllUsers);
router.get('/:id', auth, userController.getUser);

module.exports = router;
```

## **12. Route Testing & Debugging**

### **List All Routes**

```javascript
// Helper to see all registered routes
app._router.stack.forEach((middleware) => {
  if (middleware.route) {
    console.log(middleware.route);
  }
});
```

### **Route Logging Middleware**

```javascript
app.use((req, res, next) => {
  console.log(`${req.method} ${req.path}`);
  console.log('Params:', req.params);
  console.log('Query:', req.query);
  console.log('Body:', req.body);
  next();
});
```

## **13. Performance Tips**

```javascript
// ❌ BAD: Inefficient route order
app.get('/users/:id', getUser);      // Checked first
app.get('/users/me', getCurrentUser); // Never reached! :id matches 'me'

// ✅ GOOD: Specific routes first
app.get('/users/me', getCurrentUser);  // Checked first
app.get('/users/:id', getUser);        // Checked second
```

```javascript
// ✅ Use router.param for repeated logic
router.param('id', async (req, res, next, id) => {
  req.item = await Model.findById(id);
  next();
});

// Now all routes with :id have req.item available
router.get('/:id', (req, res) => res.json(req.item));
router.put('/:id', (req, res) => { /* req.item available */ });



### Cors?
## **The Problem CORS Solves**

Browsers have a security policy called "Same-Origin Policy" that blocks websites from making requests to different domains. This prevents malicious sites from stealing your data.

**Example of the problem:**
- Your frontend runs on: `http://localhost:3000`
- Your backend API runs on: `http://localhost:5000`
- Browser blocks the request because they're different origins!

## **What is an "Origin"?**

An origin = **protocol + domain + port**

```
http://example.com:3000
│      │           │
│      │           └─ Port
│      └─ Domain
└─ Protocol
```

**Different origins:**
- `http://localhost:3000` ≠ `http://localhost:5000` (different port)
- `http://example.com` ≠ `https://example.com` (different protocol)
- `http://example.com` ≠ `http://api.example.com` (different subdomain)

## **CORS Error Example**

Without CORS setup, you'll see this error in the browser console:

```
Access to fetch at 'http://localhost:5000/api/users' from origin 
'http://localhost:3000' has been blocked by CORS policy: 
No 'Access-Control-Allow-Origin' header is present.
```

## **Using CORS in Express**

**1. Install the CORS package:**
```bash
npm install cors
```

**2. Basic usage (Allow all origins):**
```javascript
const express = require('express');
const cors = require('cors');
const app = express();

// Enable CORS for all routes
app.use(cors());

app.get('/api/users', (req, res) => {
  res.json({ users: ['John', 'Jane'] });
});

app.listen(5000);
```

**3. Allow specific origin:**
```javascript
const corsOptions = {
  origin: 'http://localhost:3000', // Only this origin allowed
  optionsSuccessStatus: 200
};

app.use(cors(corsOptions));
```

**4. Allow multiple origins:**
```javascript
const allowedOrigins = [
  'http://localhost:3000',
  'http://localhost:3001',
  'https://myapp.com'
];

const corsOptions = {
  origin: function (origin, callback) {
    if (!origin || allowedOrigins.indexOf(origin) !== -1) {
      callback(null, true);
    } else {
      callback(new Error('Not allowed by CORS'));
    }
  }
};

app.use(cors(corsOptions));
```

**5. Enable CORS for specific routes only:**
```javascript
// CORS only on this route
app.get('/api/public', cors(), (req, res) => {
  res.json({ message: 'Public data' });
});

// No CORS on this route
app.get('/api/private', (req, res) => {
  res.json({ message: 'Private data' });
});
```

**6. Advanced configuration:**
```javascript
const corsOptions = {
  origin: 'http://localhost:3000',
  methods: ['GET', 'POST', 'PUT', 'DELETE'], // Allowed methods
  allowedHeaders: ['Content-Type', 'Authorization'], // Allowed headers
  credentials: true, // Allow cookies
  maxAge: 3600 // Cache preflight request for 1 hour
};

app.use(cors(corsOptions));
```

## **CORS with Credentials (Cookies/Auth)**

If you need to send cookies or authentication:

**Backend:**
```javascript
app.use(cors({
  origin: 'http://localhost:3000',
  credentials: true // Important!
}));
```

**Frontend:**
```javascript
fetch('http://localhost:5000/api/users', {
  credentials: 'include' // Include cookies
})
```

## **Manual CORS Setup (Without the package)**

You can also set CORS headers manually:

```javascript
app.use((req, res, next) => {
  res.header('Access-Control-Allow-Origin', '*'); // or specific origin
  res.header('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE');
  res.header('Access-Control-Allow-Headers', 'Content-Type, Authorization');
  
  // Handle preflight
  if (req.method === 'OPTIONS') {
    return res.sendStatus(200);
  }
  
  next();
});
```

## **Common CORS Scenarios**

**Development:**
```javascript
// Allow all during development
app.use(cors());
```

**Production:**
```javascript
// Restrict to your frontend domain
app.use(cors({
  origin: 'https://myapp.com',
  credentials: true
}));
```

**API for multiple apps:**
```javascript
const whitelist = [
  'https://app1.com',
  'https://app2.com',
  'https://mobile.app.com'
];

app.use(cors({
  origin: (origin, callback) => {
    if (whitelist.includes(origin)) {
      callback(null, true);
    } else {
      callback(new Error('Not allowed'));
    }
  }
}));
```

## **Preflight Requests**

For complex requests (PUT, DELETE, custom headers), browsers send a "preflight" OPTIONS request first. The `cors` package handles this automatically, but if doing it manually, you need to handle OPTIONS requests.

## **Security Tips**

- **Never use `origin: '*'` with `credentials: true`** in production
- **Whitelist specific origins** instead of allowing all
- **Only allow necessary HTTP methods** and headers
- **Use HTTPS** in production

### What is a Preflight
A preflight request is an **automatic OPTIONS request** that the browser sends **before** the actual request to check if the server allows it.

## **When Does a Preflight Happen?**

The browser sends a preflight for "non-simple" requests:

**Simple requests (NO preflight):**
- Methods: `GET`, `HEAD`, `POST`
- Headers: Only simple headers like `Accept`, `Content-Type` (with limited values)
- Content-Type: `application/x-www-form-urlencoded`, `multipart/form-data`, or `text/plain`

**Non-simple requests (YES preflight):**
- Methods: `PUT`, `DELETE`, `PATCH`
- Custom headers: `Authorization`, `X-Custom-Header`, etc.
- Content-Type: `application/json`
- Credentials with cross-origin requests

## **How Preflight Works**

**Step 1:** Browser sends OPTIONS request
```
OPTIONS /api/users HTTP/1.1
Origin: http://localhost:3000
Access-Control-Request-Method: DELETE
Access-Control-Request-Headers: Authorization, Content-Type
```

**Step 2:** Server responds with allowed permissions
```
HTTP/1.1 200 OK
Access-Control-Allow-Origin: http://localhost:3000
Access-Control-Allow-Methods: GET, POST, PUT, DELETE
Access-Control-Allow-Headers: Authorization, Content-Type
Access-Control-Max-Age: 86400
```

**Step 3:** If approved, browser sends the actual request
```
DELETE /api/users/123 HTTP/1.1
Origin: http://localhost:3000
Authorization: Bearer token123
```

## **Handling Preflight in Node/Express**

### **Method 1: Using the `cors` Package (Easiest)**

```javascript
const express = require('express');
const cors = require('cors');
const app = express();

// Automatically handles preflight
app.use(cors({
  origin: 'http://localhost:3000',
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization'],
  credentials: true,
  maxAge: 86400 // Cache preflight for 24 hours
}));

app.delete('/api/users/:id', (req, res) => {
  res.json({ message: 'User deleted' });
});

app.listen(5000);
```

### **Method 2: Manual Preflight Handling**

```javascript
const express = require('express');
const app = express();

// Middleware to handle CORS and preflight
app.use((req, res, next) => {
  // Set CORS headers
  res.header('Access-Control-Allow-Origin', 'http://localhost:3000');
  res.header('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE, PATCH');
  res.header('Access-Control-Allow-Headers', 'Content-Type, Authorization');
  res.header('Access-Control-Allow-Credentials', 'true');
  res.header('Access-Control-Max-Age', '86400'); // 24 hours
  
  // Handle preflight OPTIONS request
  if (req.method === 'OPTIONS') {
    return res.status(200).end(); // Send 200 OK for preflight
  }
  
  next();
});

app.delete('/api/users/:id', (req, res) => {
  res.json({ message: 'User deleted' });
});

app.listen(5000);
```

### **Method 3: Specific Route Preflight**

```javascript
const express = require('express');
const app = express();

// Handle preflight for specific route
app.options('/api/users/:id', (req, res) => {
  res.header('Access-Control-Allow-Origin', 'http://localhost:3000');
  res.header('Access-Control-Allow-Methods', 'DELETE, PUT');
  res.header('Access-Control-Allow-Headers', 'Content-Type, Authorization');
  res.status(200).end();
});

// Actual DELETE route
app.delete('/api/users/:id', (req, res) => {
  res.header('Access-Control-Allow-Origin', 'http://localhost:3000');
  res.json({ message: 'User deleted' });
});

app.listen(5000);
```

## **Real Example: Frontend Making a Preflight Request**

**Frontend (React/JavaScript):**
```javascript
// This triggers a preflight because:
// 1. Method is DELETE
// 2. Has Authorization header
// 3. Content-Type is application/json

fetch('http://localhost:5000/api/users/123', {
  method: 'DELETE',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer token123'
  },
  credentials: 'include'
})
.then(res => res.json())
.then(data => console.log(data));
```

**Backend (Express):**
```javascript
const express = require('express');
const cors = require('cors');
const app = express();

app.use(cors({
  origin: 'http://localhost:3000',
  credentials: true,
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization']
}));

app.delete('/api/users/:id', (req, res) => {
  // Browser automatically sent OPTIONS first
  // cors package handled it
  // Now this DELETE executes
  res.json({ message: `User ${req.params.id} deleted` });
});

app.listen(5000);
```

## **Debugging Preflight Issues**

**Check in browser DevTools (Network tab):**

1. Look for an OPTIONS request before your actual request
2. Check the response headers:
   - `Access-Control-Allow-Origin`
   - `Access-Control-Allow-Methods`
   - `Access-Control-Allow-Headers`

**Common errors:**

```javascript
// ❌ BAD: Missing OPTIONS handler
app.delete('/api/users/:id', (req, res) => {
  res.json({ message: 'Deleted' });
});
// Browser sends OPTIONS, gets 404!

// ✅ GOOD: Use cors middleware
app.use(cors());
app.delete('/api/users/:id', (req, res) => {
  res.json({ message: 'Deleted' });
});
```

## **Optimizing Preflight with Max-Age**

Cache preflight responses to reduce requests:

```javascript
app.use(cors({
  origin: 'http://localhost:3000',
  maxAge: 86400 // Browser caches preflight for 24 hours
}));
```

Now the browser only sends the preflight once per day instead of before every request!

## **Complete Working Example**

```javascript
const express = require('express');
const cors = require('cors');
const app = express();

// Parse JSON
app.use(express.json());

// Enable CORS with preflight support
app.use(cors({
  origin: 'http://localhost:3000',
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization'],
  credentials: true,
  maxAge: 3600 // 1 hour
}));

// Routes
app.get('/api/users', (req, res) => {
  res.json({ users: ['John', 'Jane'] });
});

app.post('/api/users', (req, res) => {
  res.json({ message: 'User created', data: req.body });
});

app.put('/api/users/:id', (req, res) => {
  // Preflight handled automatically by cors middleware
  res.json({ message: `User ${req.params.id} updated` });
});

app.delete('/api/users/:id', (req, res) => {
  // Preflight handled automatically by cors middleware
  res.json({ message: `User ${req.params.id} deleted` });
});

app.listen(5000, () => {
  console.log('Server running on port 5000');
});
```

## **Key Takeaways**

1. **Preflight = Automatic OPTIONS request** before complex requests
2. **Use `cors` package** - it handles preflight automatically
3. **Manual setup:** Handle OPTIONS method explicitly
4. **Cache with maxAge** to reduce preflight requests
5. **Always check browser DevTools** to debug CORS issues
