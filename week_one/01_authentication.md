# Authentication intro

## Learning goals

- Authentication vs Authorization vs Identification
- Why do we need authentication?
- How does authentication work?
- Create a password hashing function using Bcrypt and salting
- Brute force attacks and how to prevent them
- You can't see/have your users' passwords, you have to save the hashed passwords
- Force the user give a strong password
- Register and Login system

## Resources

- [how bycript works](https://bcrypt.online/)
- [bcrypt npm](https://www.npmjs.com/package/bcrypt)
- [hashing, salting, bcrypt - video](https://www.youtube.com/watch?v=qgpsIBLvrGY)
- [authentication using express js and bcrypt - video](https://www.youtube.com/watch?v=Ud5xKCYQTjM)

## Authentication vs Authorization vs Identification

- **Identification**: The process of identifying a user, usually by a username or email address.
- **Authentication**: The process of verifying the identity of a user, usually by checking a password. =(wer bin ich)
- **Authorization**: The process of determining what a user is allowed to do, usually by checking roles or permissions. =(was darf ich)

All three are important parts of a **security and access control system**.

## Authentication

There are many types of authentication:

- **Basic Authentication**: The client sends a username and password in the request header. This is not secure because the password is sent in plain text.
- **Token-based Authentication**: The client sends a username and password to the server, and the server responds with a token. The client then sends this token in the request header for subsequent requests. This is more secure because the token is not the actual password.
- **OAuth**: A protocol that allows a user to grant a third-party application limited access to their resources without sharing their credentials.
- **Multi-factor Authentication**: A method of confirming a user's claimed identity by using two or more different factors: something they know (password), something they have (token), or something they are (biometric).
- **Biometric Authentication**: A method of verifying a user's identity by using unique biological traits, such as fingerprints, facial recognition, or voice recognition.

## Why do we need authentication?

- **Protecting User Data**: Authentication ensures that only authorized users can access sensitive data.
- **Preventing Unauthorized Access**: Authentication prevents unauthorized users from accessing restricted resources.
- **Personalization**: Authentication allows users to personalize their experience by saving preferences and settings.
- **Security**: Authentication helps in securing the application from unauthorized access and data breaches.

## How does authentication work?

1. **User Registration**: The user creates an account by providing a username and password.
2. **Password Hashing**: The password is hashed using a secure hashing algorithm, such as bcrypt, to protect it from being exposed in case of a data breach.
3. **Password Salting**: A random value (salt) is added to the password before hashing to prevent the same password from producing the same hash.
4. **Storing the Hashed Password**: The hashed password and the salt are stored in the database.
5. **User Login**: When the user logs in, the entered password is hashed with the stored salt and compared with the stored hashed password. If the hashes match, the user is authenticated.

## Create a password hashing function using Bycrypt and salting

```javascript
import bcrypt from "bcrypt";

// Hashing a password
const saltRounds = 10;
const password = "myPassword123";

bcrypt.hash(password, saltRounds, function (err, hash) {
  if (err) {
    console.error(err);
  } else {
    console.log(hash);
  }
});

// Comparing a password

const hashedPassword = "$2b$10$3v6";
const enteredPassword = "myPassword123";

bcrypt.compare(enteredPassword, hashedPassword, function (err, result) {
  if (err) {
    console.error(err);
  } else {
    console.log(result);
  }
});
```

## Brute force attacks and how to prevent them

- **Brute Force Attack**: An attack in which an attacker tries to guess a password by trying all possible combinations until the correct one is found.
- **Preventing Brute Force Attacks**:
  - **Rate Limiting**: Limit the number of login attempts per user or IP address.
  - **Account Lockout**: Lock the user account after a certain number of failed login attempts.
  - **CAPTCHA**: Use CAPTCHA (determine if the user is an human) to prevent automated bots from performing brute force attacks.
  - **Two-factor Authentication**: Require a second form of authentication, such as a token or biometric verification, in addition to the password.

## Force the user give a strong password

A strong password should be at least 8 characters long and contain a combination of uppercase and lowercase letters, numbers, and special characters.

## You can't see/have your users' passwords, you have to save the hashed passwords

It is important to never store passwords in plain text. Instead, use a secure hashing algorithm, such as bcrypt, to hash the passwords before storing them in the database. This ensures that even if the database is compromised, the passwords are not exposed.
