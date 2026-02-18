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

***Zero Configuration.***

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
  ***But not great for many user at once.***

  #### What is high Concurrency?
  
  
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
#### Why SWagger is used in Followup Tracker but not in Ebookstore?
**EbookStore**
- MVC app
- Views + Controllers
**Followup**
- Pure API
- No UI
**Swagger replaces UI for APIs**
#### Why EbookStore and Followup tracker has different code structure?
**EbookStore:**
- Server-side rendering
- Views + Controllers tightly coupled
**FollowUp:**
- API-first
- Frontend separated
***Modern Architecture***

#### Models vs Data folder
```
Models --> Business entities
Data --> Database configuration
```
#### Web App vs Web API
**Web App:**
- Renders HTML
- Razor Views
**Web API**
- Returns JSON
- Used by Frontend/mobile apps
#### GUID vs Integer IDs
**Integer**
- Simple
- Database-managed
**GUID**
- Globally unique
- Safe across system
- Best for distributed apps

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

   

