# 🍪 Cookies

## Learning goals

- Login and Logout with cookies and JWT
- Using cookies to save state across requests (http-only cookies)
- Setting cookies with `res.cookie()`
- Using `cookieParser` to read cookies: `req.cookies`
- Cookies are accessible from JavaScript; can be stolen - unless you configure them with http-only!

## Resources

- [localStorage vs sessionStorage vs cookies (Video)](https://www.youtube.com/watch?v=GihQAC1I39Q&t=3s)
- [store jwt in localstorage is dangerous - (Video)](https://www.youtube.com/watch?v=3_WFZTIxDW4)

---

Sehr gutes Thema! 👏 Cookies bieten eine **sichere Alternative** zum Speichern von JWTs, besonders mit **`httpOnly`** Cookies, die **nicht aus JavaScript auslesbar** sind (also nicht durch XSS geklaut werden können).

---

## 🍪 Cookies & JWT – Lernziele Schritt für Schritt:


### ✅ 1. **Login + Logout mit JWT + Cookies**

> Ziel: Statt Token im `localStorage`, speichert der Server den JWT direkt in einem sicheren Cookie.

---

### 📦 2. **Pakete installieren (Backend)**

```bash
npm install cookie-parser
```

In `server.js`:

```js
const cookieParser = require("cookie-parser");
app.use(cookieParser());
```

---

### 🧠 3. **JWT in httpOnly Cookie speichern (Login)**

In deiner **Login-Route** (`routes/auth.js`):

```js
router.post("/login", async (req, res) => {
  const { username, password } = req.body;
  const user = await User.findOne({ username });

  if (!user) return res.status(400).json({ message: "User not found" });

  const match = await bcrypt.compare(password, user.password);
  if (!match) return res.status(401).json({ message: "Wrong password" });

  const token = jwt.sign(
    { userId: user._id, username: user.username },
    process.env.JWT_SECRET,
    { expiresIn: "1h" }
  );

  // 🍪 Set Cookie (httpOnly, secure in production)
  res.cookie("token", token, {
    httpOnly: true,
    secure: false, // ⛔ in production: true with HTTPS!
    sameSite: "strict",
    maxAge: 3600000, // 1h
  });

  res.json({ message: "Login successful" });
});
```

---

### 🔓 4. **Logout: Cookie löschen**

```js
router.post("/logout", (req, res) => {
  res.clearCookie("token");
  res.json({ message: "Logged out" });
});
```

---

### 🔍 5. **JWT Middleware prüft Cookie statt Header**

**`middleware/authMiddleware.js`**

```js
const jwt = require("jsonwebtoken");

const authMiddleware = (req, res, next) => {
  const token = req.cookies.token; // 🍪 lies den JWT aus Cookie

  if (!token) return res.status(401).json({ message: "Kein Token" });

  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    next();
  } catch (err) {
    res.status(403).json({ message: "Ungültiger Token" });
  }
};

module.exports = authMiddleware;
```

---

### 🚀 6. **Frontend-Anpassung (Login/Logout)**

#### `axios` Setup (Frontend `api.js`):

```js
const API = axios.create({
  baseURL: "http://localhost:5000/api",
  withCredentials: true, // ✅ Sendet Cookies mit
});
```

#### Login-Request:

```js
await API.post("/auth/login", form); // keine Token-Speicherung in localStorage!
```

#### Logout:

```js
await API.post("/auth/logout");
```

#### Authentifizierte Anfrage (z. B. `/protected`):

```js
const res = await API.get("/auth/protected");
```

---

## 🧠 Wichtige Cookie-Sicherheitsregeln

| Attribut   | Wirkung                                             |
| ---------- | --------------------------------------------------- |
| `httpOnly` | JS kann Cookie nicht auslesen → schützt vor XSS 🛡️ |
| `secure`   | Cookie wird **nur über HTTPS** gesendet 🔒          |
| `sameSite` | Schutz vor CSRF (z. B. `"strict"` oder `"lax"`) 🚧  |

> 🔐 httpOnly + secure + sameSite = sichere Auth über Cookies!

---

## 🎯 Zusammenfassung (Lernziele erfüllt?)

| Ziel                           | Erfüllt? |
| ------------------------------ | -------- |
| Login mit Cookie               | ✅        |
| Logout via `clearCookie`       | ✅        |
| Cookie vs localStorage erklärt | ✅        |
| Verwendung von `cookie-parser` | ✅        |
| `httpOnly` Vorteile verstanden | ✅        |

---

## 🧪 Nächste Schritte?

* Authenticated frontend routing mit Zustand (z. B. Context)
* Refresh Tokens (länger leben mit `refresh + access` Strategie)
* Vercel + HTTPS Deployment mit Cookie Auth
* CSRF-Schutz & Cookie SameSite-Strategien

Sag einfach:
👉 „Nächstes Thema“
👉 „Jetzt Kontext & Protected Route im FE“
👉 „Ich will Refresh Tokens verstehen“

Ich richte mich nach deinem Fokus. 🧭
