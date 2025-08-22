# APIs 🚀:

---

## 🔹 RESTful API

**REST = Representational State Transfer**
A **RESTful API** is an interface that follows REST principles, usually built on top of HTTP.

### Key Principles:

1. **Stateless** → Every request contains all info (server doesn’t remember client state).
2. **Resources** → Everything is treated as a resource (user, post, product), identified by a unique URL.
3. **HTTP Methods map to CRUD**:

| HTTP Verb | CRUD Operation   | Example                                 |
| --------- | ---------------- | --------------------------------------- |
| `GET`     | Read             | `GET /users/1` → fetch user with id=1   |
| `POST`    | Create           | `POST /users` → create new user         |
| `PUT`     | Update (replace) | `PUT /users/1` → replace user with id=1 |
| `PATCH`   | Update (partial) | `PATCH /users/1` → update some fields   |
| `DELETE`  | Delete           | `DELETE /users/1` → remove user         |

4. **Stateless Responses** → Server just responds to request; no session state stored.
5. **Standard Codes** → Uses HTTP status codes (200, 201, 404, 503, …).

👉 REST is popular because it’s **simple, scalable, and human-readable.**

---

## 🔹 Other Types of APIs

### 1. **SOAP (Simple Object Access Protocol)**

* XML-based, older enterprise standard.
* Strict rules, contracts (WSDL).
* Often used in banking, legacy enterprise systems.

### 2. **GraphQL**

* Query language for APIs (by Facebook/Meta).
* Client specifies exactly what data it needs in one request.
* Example:

  ```graphql
  {
    user(id: 1) {
      name
      posts {
        title
      }
    }
  }
  ```

  → returns **only** name + post titles.
* Great for mobile apps & complex data.
* ends on graphql, POST requests


### 3. **gRPC**

* High-performance, binary protocol (built on HTTP/2).
* Uses Protocol Buffers (protobuf) instead of JSON.
* Often used in microservices.

### 4. **WebSockets**

* Persistent two-way connection (not request-response like REST).
* Perfect for chat apps, live dashboards, gaming.

### 5. **JSON-RPC / XML-RPC**

* Remote Procedure Calls (function-like API).
* Simpler than SOAP, usually not as flexible as REST.

### 6. **OData**

* Microsoft’s protocol for querying APIs with URL parameters (`$filter`, `$select`).
* Example:

  ```
  GET /users?$filter=age gt 20&$select=name,email
  ```

---

⚡️ TL;DR:

* **REST** → simple, standard, works everywhere.
* **GraphQL** → flexible queries, one request, no over-fetching.
* **gRPC** → fast binary comms, great for microservices.
* **SOAP** → enterprise, heavy XML.
* **WebSockets** → real-time, persistent.

---

👉 Soll ich Dir eine **Vergleichstabelle** (REST vs GraphQL vs gRPC vs SOAP usw.) bauen, so dass Du die Stärken/Schwächen auf einen Blick siehst?
