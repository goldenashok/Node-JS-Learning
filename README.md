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



What is express js?

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
