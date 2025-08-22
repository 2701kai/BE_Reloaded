# 🔐 Authentication Intro (2025 Edition)

## 🎯 Learning Goals

- 🔎 Authentication vs Authorization vs Identification
- 💡 Why authentication is essential in modern web apps
- ⚙️ How authentication flows work
- 🧂 How to hash and salt passwords securely using `bcrypt`
- 🛡️ Understand brute-force attacks and how to prevent them
- 🚫 Why storing plain passwords is dangerous
- 💪 Enforcing strong passwords
- 🧾 Building a secure Register + Login system (backend-focused)

---

## 📚 Recommended Resources

- 📹 [bcrypt explained visually](https://bcrypt.online/)
- 📦 [bcrypt on npm](https://www.npmjs.com/package/bcrypt)
- 🎥 [Hashing, salting & bcrypt – explained](https://www.youtube.com/watch?v=qgpsIBLvrGY)
- 🎥 [Express.js Auth with bcrypt – tutorial](https://www.youtube.com/watch?v=Ud5xKCYQTjM)
- 🎥 [Why storing JWT in localStorage is risky (explained)](https://www.youtube.com/watch?v=3_WFZTIxDW4)

---

## 🧠 Identification vs Authentication vs Authorization

| Concept            | Meaning                                            | Question Answered         |
| ------------------ | -------------------------------------------------- | ------------------------- |
| **Identification** | User provides their identity (e.g. email/username) | _"Wer bin ich?"_          |
| **Authentication** | System verifies identity (e.g. password check)     | _"Bin ich wirklich ich?"_ |
| **Authorization**  | System checks user’s permissions                   | _"Was darf ich tun?"_     |

➡️ All three are critical for a secure and user-centric app.

---

## 🔐 Types of Authentication (2025)

- **Basic Auth**: Username/password sent in header → ❌ insecure (no hashing)
- **JWT (JSON Web Token)**: Server issues signed token after login → ✅ popular for MERN stack
- **Cookie-based Auth**: JWT stored in `httpOnly` cookies → ✅ safer than localStorage
- **OAuth2**: Login via Google, GitHub, etc. → great for 3rd-party logins
- **MFA / 2FA**: Extra security using email codes, apps, biometrics, etc.
- **Biometric Auth**: Face ID, fingerprints – used more in mobile/web hybrid apps

---

## 🤔 Why Do We Need Authentication?

- ✅ **Protect user data**: Personal, sensitive info must stay private
- 🚫 **Prevent unauthorized access**: Guard protected pages/data
- 👤 **Enable personalization**: Themes, preferences, saved data
- 🔐 **Secure your system**: Prevent impersonation, breaches, and abuse

---

## 🔄 How Authentication Works (Secure Flow)

1. **User registers** with username & password
2. **Password is salted & hashed** using `bcrypt`
3. 🔐 **Hashed password saved** in DB (not the real one!)
4. User logs in → server hashes entered password, **compares with stored hash**
5. If valid, server returns a **JWT** (either in cookie or response)
6. Client uses token to access protected routes → token is **verified server-side**

---

## 🧂 Bcrypt: Hashing & Salting Passwords (Node.js 22+)

### ✍️ Example using async/await

```js
import bcrypt from "bcrypt";

const saltRounds = 10;

async function hashPassword(plainPassword) {
  const hashed = await bcrypt.hash(plainPassword, saltRounds);
  return hashed;
}

async function verifyPassword(input, storedHash) {
  const match = await bcrypt.compare(input, storedHash);
  return match;
}
```

> ⚠️ Never store the plain password
> ✅ Always hash passwords before saving to your DB

---

## 🛡️ Brute-Force Attacks – What & How to Prevent

**Brute force** = trying millions of password combinations

🧱 **Prevention techniques:**

- 🚦 **Rate limiting** (e.g. max 5 logins/min per IP)
- 🔒 **Account lockout** after multiple failed attempts
- 🤖 **CAPTCHA** to block bots
- 🔑 **2FA** (email/code/token)
- 📉 **Bcrypt’s cost factor** (`saltRounds`) makes brute-force slow

---

## 🔐 Strong Password Enforcement

Require users to create **strong passwords** like:

- ✅ Min. 8–12 characters
- ✅ Uppercase + lowercase letters
- ✅ Numbers
- ✅ Special characters

Example regex:

```js
const strongPassword = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[\W_]).{8,}$/;
```

---

## 🚫 Never Store Passwords in Plain Text!

**Bad:**

```json
{ "username": "max", "password": "abc123" }
```

**Good:**

```json
{ "username": "max", "password": "$2b$10$abc...123" }
```

> Even if the DB leaks, the real passwords stay protected!

---

## ✅ Recap: What You Should Do

| Task                   | Best Practice                              |
| ---------------------- | ------------------------------------------ |
| Storing Passwords      | Hash with `bcrypt`                         |
| Securing Auth Routes   | Use JWT in `httpOnly` cookies              |
| Preventing Brute Force | Rate limit, lockout, CAPTCHA               |
| Strong Passwords       | Enforce via regex                          |
| Auth System Design     | Separate login, register, protected routes |

---
