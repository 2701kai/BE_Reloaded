# RESTful API




## xyz



## Example:

Ah, perfect example 😎 You just showed me a **RESTful API request** (in practice). Let’s dissect it:

---

### 🔎 The Example

```bash
curl --request GET \
--url 'https://api.x.com/2/tweets?ids=1260294888811347969' \
--header 'Authorization: Bearer $BEARER_TOKEN'
```

### 1. **Tool**

* `curl` → command-line tool to make HTTP requests.
* Developers use it to test APIs quickly.

### 2. **HTTP Method**

* `--request GET` → This is a **GET request** (read data).

### 3. **Endpoint (URL)**

* `https://api.x.com/2/tweets` → API endpoint of Twitter/X (version 2).
* Query parameter: `?ids=1260294888811347969` → You’re asking for **a specific tweet by ID**.

### 4. **Authorization**

* `--header 'Authorization: Bearer $BEARER_TOKEN'` →

  * Many APIs require authentication.
  * **Bearer Token** = kind of API key / access token.
  * `$BEARER_TOKEN` is a placeholder for your actual secret token.

---

### 🔹 Why this is RESTful

* Resource: **tweet** (a piece of content)
* URL identifies the resource: `/2/tweets?ids=...`
* Method: `GET` → read data
* Authentication: Bearer token in headers
* Response: JSON object with tweet info

Example response (simplified):

```json
{
  "data": [
    {
      "id": "1260294888811347969",
      "text": "Just setting up my twttr"
    }
  ]
}
```

---

✅ So, what you’ve got here is a **real-world REST API call** to **Twitter/X API v2**, fetching a tweet by ID.

---

Compared to GraphQL:

Cool 😎 — let’s compare **REST vs GraphQL** using your Twitter/X API example.

---

## 🔹 REST Example (your version)

```bash
curl --request GET \
--url 'https://api.x.com/2/tweets?ids=1260294888811347969' \
--header 'Authorization: Bearer $BEARER_TOKEN'
```

* **Method**: `GET`
* **Resource**: `/2/tweets`
* **Query param**: `ids=...`
* **Response** (simplified JSON):

  ```json
  {
    "data": [
      {
        "id": "1260294888811347969",
        "text": "Just setting up my twttr"
      }
    ]
  }
  ```

---

## 🔹 Same in **GraphQL**

With GraphQL, instead of hitting `/tweets?ids=...`, you send **one POST request** to the GraphQL endpoint (`/graphql`) and describe exactly what you want:

```bash
curl --request POST \
--url 'https://api.x.com/graphql' \
--header 'Authorization: Bearer $BEARER_TOKEN' \
--header 'Content-Type: application/json' \
--data '{
  "query": "query { tweet(id: \"1260294888811347969\") { id text author { username } } }"
}'
```

### Explanation:

* Always `POST` to `/graphql`.

* **Query language**:

  ```graphql
  query {
    tweet(id: "1260294888811347969") {
      id
      text
      author {
        username
      }
    }
  }
  ```

  * You **declare the shape of the data** you want.
  * Here: tweet `id`, `text`, plus nested `author.username`.

* **Response** (exactly shaped as requested):

  ```json
  {
    "data": {
      "tweet": {
        "id": "1260294888811347969",
        "text": "Just setting up my twttr",
        "author": {
          "username": "jack"
        }
      }
    }
  }
  ```

---

## 🔑 Key Difference

* **REST**: Separate endpoints for each resource, fixed response.
* **GraphQL**: One endpoint, flexible queries → client decides what fields to return.


---

## 🔹 REST Example (your version)

```bash
curl --request GET \
--url 'https://api.x.com/2/tweets?ids=1260294888811347969' \
--header 'Authorization: Bearer $BEARER_TOKEN'
```

* **Method**: `GET`
* **Resource**: `/2/tweets`
* **Query param**: `ids=...`
* **Response** (simplified JSON):

  ```json
  {
    "data": [
      {
        "id": "1260294888811347969",
        "text": "Just setting up my twttr"
      }
    ]
  }
  ```

---

## 🔹 Same in **GraphQL**

With GraphQL, instead of hitting `/tweets?ids=...`, you send **one POST request** to the GraphQL endpoint (`/graphql`) and describe exactly what you want:

```bash
curl --request POST \
--url 'https://api.x.com/graphql' \
--header 'Authorization: Bearer $BEARER_TOKEN' \
--header 'Content-Type: application/json' \
--data '{
  "query": "query { tweet(id: \"1260294888811347969\") { id text author { username } } }"
}'
```

### Explanation:

* Always `POST` to `/graphql`.

* **Query language**:

  ```graphql
  query {
    tweet(id: "1260294888811347969") {
      id
      text
      author {
        username
      }
    }
  }
  ```

  * You **declare the shape of the data** you want.
  * Here: tweet `id`, `text`, plus nested `author.username`.

* **Response** (exactly shaped as requested):

  ```json
  {
    "data": {
      "tweet": {
        "id": "1260294888811347969",
        "text": "Just setting up my twttr",
        "author": {
          "username": "jack"
        }
      }
    }
  }
  ```

---

## 🔑 Key Difference

* **REST**: Separate endpoints for each resource, fixed response.
* **GraphQL**: One endpoint, flexible queries → client decides what fields to return.

---

