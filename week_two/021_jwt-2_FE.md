# 🛠 MERN Auth-Beispiel mit JWT 🚀 (FE)

**Frontend-Part mit Vite + React**

## 🎯 Ziel: Frontend für JWT Auth

### Features:

- ✅ Registrierung
- ✅ Login
- ✅ Token speichern (temporär in `localStorage`)
- ✅ Token mitsenden (`Authorization: Bearer ...`)
- ✅ Geschützte Komponente (`/protected`)
- ✅ Logout

---

## ⚙️ Schritt 1: Vite React Setup

```bash
npm create vite@latest client -- --template react
cd client
npm install
npm install axios
```

Dann:

```bash
npm run dev
```

---

## 📁 Projektstruktur (Frontend)

```
/client
├── src/
│   ├── App.jsx
│   ├── api.js
│   ├── pages/
│   │   ├── Login.jsx
│   │   ├── Register.jsx
│   │   └── Protected.jsx
│   └── components/
│       └── Navbar.jsx
└── ...
```

---

## 📡 Schritt 2: Axios API Setup

**`src/api.js`**

```js
import axios from "axios";

const API = axios.create({
  baseURL: "http://localhost:5000/api",
});

API.interceptors.request.use((config) => {
  const token = localStorage.getItem("token");
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

export default API;
```

---

## 🧾 Schritt 3: Seiten – Register, Login

**`src/pages/Register.jsx`**

```jsx
import { useState } from "react";
import API from "../api";

export default function Register() {
  const [form, setForm] = useState({ username: "", password: "" });

  const handleSubmit = async (e) => {
    e.preventDefault();
    try {
      await API.post("/auth/register", form);
      alert("User registered! Jetzt einloggen.");
    } catch (err) {
      alert(err.response?.data?.message || "Fehler");
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <h2>Register</h2>
      <input
        placeholder="Username"
        onChange={(e) => setForm({ ...form, username: e.target.value })}
      />
      <input
        type="password"
        placeholder="Password"
        onChange={(e) => setForm({ ...form, password: e.target.value })}
      />
      <button type="submit">Register</button>
    </form>
  );
}
```

**`src/pages/Login.jsx`**

```jsx
import { useState } from "react";
import API from "../api";
import { useNavigate } from "react-router-dom";

export default function Login() {
  const [form, setForm] = useState({ username: "", password: "" });
  const navigate = useNavigate();

  const handleSubmit = async (e) => {
    e.preventDefault();
    try {
      const res = await API.post("/auth/login", form);
      localStorage.setItem("token", res.data.token);
      navigate("/protected");
    } catch (err) {
      alert("Login fehlgeschlagen");
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <h2>Login</h2>
      <input
        placeholder="Username"
        onChange={(e) => setForm({ ...form, username: e.target.value })}
      />
      <input
        type="password"
        placeholder="Password"
        onChange={(e) => setForm({ ...form, password: e.target.value })}
      />
      <button type="submit">Login</button>
    </form>
  );
}
```

---

## 🛡️ Schritt 4: Protected Page

**`src/pages/Protected.jsx`**

```jsx
import { useEffect, useState } from "react";
import API from "../api";

export default function Protected() {
  const [data, setData] = useState("");

  useEffect(() => {
    API.get("/auth/protected")
      .then((res) => setData(res.data.message))
      .catch(() => setData("Zugriff verweigert oder Token abgelaufen"));
  }, []);

  return <h2>{data}</h2>;
}
```

---

## 🧭 Schritt 5: Routing + Navbar

```bash
npm install react-router-dom
```

**`src/App.jsx`**

```jsx
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";
import Register from "./pages/Register";
import Login from "./pages/Login";
import Protected from "./pages/Protected";

function App() {
  const handleLogout = () => {
    localStorage.removeItem("token");
    window.location.href = "/login";
  };

  return (
    <BrowserRouter>
      <nav>
        <Link to="/register">Register</Link> | <Link to="/login">Login</Link> |{" "}
        <Link to="/protected">Protected</Link> |{" "}
        <button onClick={handleLogout}>Logout</button>
      </nav>

      <Routes>
        <Route path="/register" element={<Register />} />
        <Route path="/login" element={<Login />} />
        <Route path="/protected" element={<Protected />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

---

## ✅ Testflow (ADHD-friendly):

1. 🏁 Start den **Backend** mit:

   ```bash
   npm run dev
   ```

2. 🚀 Starte das **Frontend** mit:

   ```bash
   npm run dev
   ```

3. 🔐 Register: `http://localhost:5173/register`

4. 🔑 Login → speichert JWT in `localStorage`

5. 🔒 Gehe zu `/protected` → Token wird gesendet

6. ⛔ Logout löscht den Token

---

## 🔜 Nächste Steps (optional):

- Cookie statt localStorage (httpOnly für mehr Sicherheit)
- Token Refresh (Access + Refresh Tokens)
- Protected Routes nur mit Token sichtbar
- Fehlerhandling/Toasts
- Styling mit Tailwind

---

Willst du einen dieser nächsten Schritte machen oder lieber in eine andere Richtung weiterarbeiten (z. B. Deployment, Zustand speichern, Role-based Auth)? Sag einfach Bescheid – ich bin bereit. 💪
