# Users API

A JWT-secured REST API for user authentication and persistent data storage, built to back the [Met Artwork Explorer](https://met-artwork-explorer-753i37e4f-rendells-projects.vercel.app/) application.

> **Repo:** [renv39/users-api](https://github.com/renv39/users-api)

---

## What It Does

- Registers and authenticates users with hashed passwords
- Issues signed JWTs on login for stateless session management
- Exposes protected endpoints for reading and writing per-user favourites and search history
- Persists all data in MongoDB Atlas

## Endpoints

| Method | Route | Auth | Description |
|--------|-------|------|-------------|
| POST | `/api/user/register` | — | Create a new user account |
| POST | `/api/user/login` | — | Validate credentials, return JWT |
| GET | `/api/user/favourites` | ✅ | Get saved favourites |
| PUT | `/api/user/favourites/:id` | ✅ | Add a favourite |
| DELETE | `/api/user/favourites/:id` | ✅ | Remove a favourite |
| GET | `/api/user/history` | ✅ | Get search history |
| PUT | `/api/user/history` | ✅ | Add a history entry |
| DELETE | `/api/user/history/:id` | ✅ | Remove a history entry |

## Technologies

- Node.js / Express
- MongoDB Atlas / Mongoose
- jsonwebtoken
- Passport.js / passport-jwt
- bcryptjs

---

## Generated / Provided Code

**Full transparency:** the course provided a `user-api.zip` starter that included the Express app scaffold, a `user-service` module with pre-written Mongoose schema and helper functions (password hashing, user lookup), and stubbed route handlers. The starter handled data-model concerns so the focus of the assignment was authentication.

---

## My Responsibilities

### Configuration & Environment

- Created and configured the **MongoDB Atlas cluster** — set up the database, created a dedicated user, and whitelisted network access
- Wrote the **`.env` file** with `MONGO_URL` (Atlas connection string) and `JWT_SECRET`, and configured equivalent environment variables on the cloud deployment platform
- Connected Mongoose to the Atlas cluster using the connection string from `.env`

### Authentication Logic

- Configured **Passport.js** with a JWT strategy — extracted the token from the `Authorization` header, verified it against `JWT_SECRET`, and loaded the matching user from MongoDB
- Implemented **`POST /api/user/login`** — validated the incoming credentials against the stored hash, signed a JWT containing `_id` and `userName`, and returned it to the client
- Applied `passport.authenticate('jwt', { session: false })` middleware to all 6 protected routes

### Deployment

- Deployed the Express server to a cloud hosting platform with all environment variables configured for production

---

*Built as part of coursework at Seneca Polytechnic — Computer Programming & Analysis*
