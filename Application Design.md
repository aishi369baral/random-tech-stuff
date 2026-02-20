#### Difference between System Design & Clean Architecture:
```
System Design
│
├── High-level architecture (services, DB, cache, APIs)
│
└── Application Design
    └── Clean Architecture
```

- **System design decides =** WHAT components exist || about designing scable systems.
- **Clean Architecture decides** = HOW code inside a component is written || is about structuring code inside a service for testability, maintainability and scalibility by separation of concerns.

---

#### Postgres vs SQLite 
- **SQLite**
- *Pros:*
- Simple
- File based
- Zero config
- Perfect for MVP
- *Cons:*
- Not for high concurrency
- Not enterprise-grade
- **PostgreSQL**
- *Pros*
- Production ready
- scales well
- strong data integrity
- *Cons*
- Needs server
- More setup
```
*Use:*
SQLite -> learning/local/small apps
Postgres -> real-world, multi-user apps
```

---

#### What does "Zero Config" mean for SQLite?
**What is config:**
```
Configuration = settings you mucst provide so something can work.
```
**Examples of config you already know:**
- Database name
- Username/password
- Port number
- Server address
- Storage location
  
**Normal DB (Postgres/SQL Server) need config like:**
```
Server = localhost
Port = 5432
Database = Followup
Username = admin
Password = ****
```
*You must:*
- Install database software
- Start it
- Create users
- Open ports
- Manage permissions

**For SQLite = zero config**
- No username
- No password
- No server
- No port
- No setup screen
```
Data Source = followup.db
```
- If file exists --> DB works
- If it doesn't --> SQLite creates it

*Zero Configuration.*

---

#### Why is SQLite file-based?
SQLite stores everything in one file:
```
followup.db
```
Inside that file:
- Tables
- Rows
- Indexes
- Data

**Why file-based matters:**
- Easy to copy
- Easy to delete
- Easy to reset

*But not great for many user at once.*

---

#### What is high Concurrency?
```
Concurrency = many people at the same time.
```
Example:
- 1 user saving data -> fine
- 50 user saving data -> still ok
- 500 users saving data at the same -> stress

SQLite and concurrency:
- SQLite locks the entire file when writing
- Only one write at a time

Result:
- Others wait
- Apps slow down

Postgres and Concurrency:
- Uses row-level locking
- Multiple writes at same time
- Designed for multi-user systems

That is why SQLite is bad for high Concurrency.

---  

#### What does enterprise-grade mean?
```
enterprise-grade = safe for big companies
```

Includes:
- Thousand of users
- Huge data
- Backups
- Replication
- Failover
- Security
- Auditing

Postgres has all of these

SQLite does not

---

#### What is data integrity?
```
Data Integrity = data stays correct and trustworthy
```
Examples:
- No duplicate users
- No orphan records
- No half-saved data
- No invalid foreign keys

**PostgresSQL has strong data integrity**

Because it supports:
- Foreign key enforcement
- Transactons
- Constraints
- Isolation levels
- Rollbacks

Meaning: Either everything succeeds, or nothing is saved.

**SQLite supports some, but:**
- Less strict
- Easier to misuse

---

#### What does Production-ready mean?
```
Production = real users, real data
```

Production-ready means:
- Stable
- Secure
- Handles load
- Backups supported
- Recovery possible
- Monitored

**SQLite**
- Not ideal for production APIs
**Postgres:**
- Designed for production

---

#### SQLite doesn't need a server - what does that mean?
PostgresSQL:
- Runs as a backgraound service
- Always listening
- Apps connect to it

```
[Your App] -> [Postgres Server] -> [Database Files]
```
SQLite:
- No background service
- App opens the file directly

```
[You App] -> followup.db
```
---

#### What is Swagger?
**Swagger**
- Auto-generates API UI
- Lets you test APIs in browser

**Used when**
- Building APIs
- Testing endpoints

**Alternatives**
- Postman
- Insomnia
---
#### Why SWagger is used in Followup Tracker but not in Ebookstore?
**EbookStore**
- MVC app
- Views + Controllers

**Followup**
- Pure API
- No UI

*Swagger replaces UI for APIs*

---

#### Why EbookStore and Followup tracker has different code structure?
**EbookStore:**
- Server-side rendering
- Views + Controllers tightly coupled

**FollowUp:**
- API-first
- Frontend separated

*Modern Architecture*

---
#### Models vs Data folder
```
Models --> Business entities
Data --> Database configuration
```
---
#### Data folder contains data config
```
Configuration = rules + setup
```
In data/:
- Hw models map to tables
- Relationships
- Indexes
- Constraints
- Database provider

```
options.UseSqlite()
```

That's configuration:
```
"Use SQLite, not SQL Server"
```

- Models = **What data looks like**
- Data = **How data is stored**

---

#### Web App vs Web API :
**Web App:**
- Renders HTML
- Razor Views

**Web API**
- Returns JSON
- Used by Frontend/mobile apps
---

#### GUID vs Integer IDs
**Integer**
- Simple
- Database-managed

**GUID**
- Globally unique
- Safe across system
- Best for distributed apps

---
#### Integer IDs are database-managed 
**Integer ID**
```
Id INT AUTO_INCREMENT
```
**Database:**
- Generates next number
- Ensures uniqueness
- Controls sequence

**App:**
- Doesn't care
- Just inserts row

**Problems in Distributed systems**
```
if:
- Two databases
- Two servers
- syn later

Both generate:
id = id

Collision
```
---
#### Why GUIDs are best for Distributed apps
GUID:
- Generated by app
- Globally unique
- No central authority needed

Two systems generate IDs:
```
7f9c2e6a...
a1b9d002...

No collision. Ever.
```

**Why GUID is safe across systems**
Because:
- Huge address space
- Randomized
- Practically impossible to duplicate

---
#### When to use Integer vs GUID
**Use Integer when:**
- Single database
- Small app
- Internal systems
- Performance critical tables
**Use GUID when:**
- APIs
- Microservices
- Sync between systems
- Offline-first apps
- Public identifiers

---

#### Where to put ConnectionStrings?
**Best practice for now:**
```
appsettings.Development.json
```
**Because:**
- Local DB
- Dev-only

**Later:**
- Production secrets go to environment variables.

---

#### What is JWT Authentication?
First what is Authentication?
```
Authentication = proving who you are
```
Examples:
- Logging in with email + password
- OTP verfication
- Fingerprint / Face ID

**JWT Authentication(simple meaning):**
- JWT = JSON Web Token
- JWT Authentication means:
```
After you log in once, the server gives you a signed token

You send that token with every request to prove who you are
```
**Real-life analogy:**
- Login = showing ID at reception
- JWT = entry badge
- Every room you enter -> you show the badge
- No need to re-verify identity again and again

**What does a JWT look like?**
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```
it contains:
- UserId
- Email
- Expiry time
- Signature (to prevent tampering)

---

#### When is JWT used?
JWT is used when:
- You have APIs
- Frontend and backend are separated
- Mobile apps
- SPA (React, Angular, Vue)
- Microservices
- Scalable systems

**Summary:** 
```
JWT Token is created by Auth/JWTService.cs in backend on Register/login ------>  (Authentication)
Token sent to frontend which stores it
Token is sent with each request to the backend  --------------------------------> (Authorization: checking what user can do)
```
---

#### What does stateless mean?
First what is state:
```
State = stored memory on server
```
Example:
- Session stored in server memory
- Server remembers logged-in users

**Stateful authentication(old way)**
- Server stores session
- Each user has session data
- Needs memory / database
```
Server remembers you
```

**JWT is Stateless**
```
Stateless = server remembers nothing
```
- Server does NOT store login info
- Token itself contains all info
- Server only verifies signature

---

#### Why stateless is powerful?
- Easy to scale
- No session storage
- Works across servers
- Cloud friendly

---

#### Summary (JWT)
```
Term                  Meaning
JWT                   Signed identity token used for authentication
Authentication        Proving identity
Stateless             Server does not store login state
Used in               APIs, SPAs, mobile apps
```

---
#### What does it mean to Serialize the JwtSecurityToken? and why it is needed?

You create this object:

```
var token = new JwtSecurityToken(
    issuer: _config["Jwt:Issuer"],      // you created the token. your API verifies it later
    audience: _config["Jwt:Audience"],   // Who it was created for. Prevent token reuse in another system 
    claims: claims,                        // Claims: user data inside the token
    expires: DateTime.UtcNow.AddDays(7),    // Token Lifetime (7 days)
    signingCredentials: creds                // Attaches the digital signature
);

```

This is a C# object, which can not be sent over Http.
### Serializing = converting the object ---> compact string

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
```

That string is what:
- goes to the browser
- is stored in localStorage/cookies
- is sent in Authorization: Bearer <token>

```
without serialization -> the token can't travel over the network.
```
---
#### What is Encoding.UTF8.GetBytes() /
it converts a string -> byte[]
```
"MySecretKey123"
```
becomes:
```
[77, 121, 83, 101, 99, 114, 101, 116, 75, 101, 121, 49, 50, 51]
```
**Why this is needed:**

Cryptographic function do not work with strings.
They work with raw bytes.

So we convert:
```
secret text -> bytes -> used by crypto algorithm (HMACSHA256 signing algorithm) 
```

#### What is the "secret key string" ?
```
your server's private password for signing tokens
```

**Why it is needed?**
it is used to:

- prove the token was created by your server
- detect if someone modified the token

**If the key changes -> tokens become invalid**


**Summary:**
- The secret key is converted from string -> byte[] (using Encoding.UTF8.GetBytes())
- the newly converted key then is used by the server to sign the JWT token using HMACSHA256 signing algorithm. 
--- 

#### What is a Rest API?
What is an API?
```
API = way for programs to talk to each other
```
Example:

- Browser -> Server
- Mobile app -> Backend
- Frontend -> Database (via backend)

#### Rest API (Representational State Tranfer)(simple meaning)
```
REST = rules for building APIs
```

REST API means:
```
API that follows standard web rules using HTTP
```

**Core REST rules(simple)**
- Uses HTTP methods
- Uses URLs to represent resources
- is stateless
- Returns JSON

**HTTP Methods you already use**
| Method | Meaning     |
| ------ | ----------- |
| GET    | Read data   |
| POST   | Create data |
| PUT    | Update      |
| DELETE | Remove      |


**REST Example:**
```
GET/api/users
POST/api/users
GET/api/users/5
```

**REST API vs general API:**
| API             | REST API           |
| --------------- | ------------------ |
| Any interface   | Follows REST rules |
| Can be anything | Uses HTTP          |
| May be stateful | Stateless          |
| Any format      | Usually JSON       |

REST is a type of APIs.

**WHen do we use REST APIs?**
Use REST when:

- Frontend & backend ar separate
- Mobile apps
- Web apps
- Public APIs
- Microservices


---

#### Authentication vs Authorization

**Authentication (WHO are you)**
- Login
- Verify identify
- Email + password

Example:
```
"I am Aishi"
```

**Authorization (What can you do)**
- Permissions
- Roles
- Access control

Example:
```
"Can Aishi delete users?"
```

**Example in app:**
| Step          | Meaning        |
| ------------- | -------------- |
| Login         | Authentication |
| Admin role    | Authorization  |
| Delete client | Authorization  |
| View own data | Authorization  |

**Quick comparison table:**
| Authentication | Authorization   |
| -------------- | --------------- |
| Who you are    | What you can do |
| Login          | Permissions     |
| Happens first  | Happens after   |


**How JWT fits here:**
```
- JWT handles authentication
- Authorization uses JWT claims(roles, permission)
```

---

#### Final mental model:

- JWT = digital ID card
- Stateless = server has no memory
- REST = rules for API design
- Authentication = identity
- Authorization = permissions
