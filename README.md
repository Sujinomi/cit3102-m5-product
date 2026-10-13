# Product API

**Partners:** Juan Miguel S. Evangelista, N/A (Solo)
**Section:** IT1E
**Resource:** Product

## Setup

Follow these steps to run the project from a fresh clone:

1. Clone the repository:
```
   git clone https://github.com/Sujinomi/cit3102-m5-product.git
```
2. Go into the project folder:
```
   cd cit3102-m5-product
```
3. Install the dependencies:
```
   composer install
```
4. Copy the environment file:
```
   copy .env.example .env
```
5. Generate the app key:
```
   php artisan key:generate
```
6. Create the database tables (say **yes** if it asks to create the SQLite file):
```
   php artisan migrate
```
7. Start the server:
```
   php artisan serve
```

The API will run at `http://127.0.0.1:8000`. Send the header `Accept: application/json` with every request.

## Routes

| Verb | Path | What it does | Needs token? |
|---|---|---|---|
| POST | /api/register | Creates a new user and returns a token | No |
| POST | /api/login | Logs in a user and returns a token | No |
| POST | /api/logout | Deletes the current token | Yes |
| GET | /api/me | Shows the logged-in user | Yes |
| GET | /api/products | Lists all products (can filter by name, category, price, stock) | Yes |
| POST | /api/products | Creates a new product | Yes |
| GET | /api/products/{product} | Shows one product | Yes |
| PUT | /api/products/{product} | Updates a product | Yes |
| DELETE | /api/products/{product} | Deletes a product | Yes |

## Screenshots

**1. POST /api/register (201)**
![01-register](screenshots/01-register.png)

**2. POST /api/login (200)**
![02-login](screenshots/02-login.png)

**3. GET /api/products with no token (401)**
![03-no auth](screenshots/03-no-auth.png)

**4. GET /api/products with token (200)**
![04-token](screenshots/04-token.png)

**5. POST /api/products with valid data (201)**
![05-create](screenshots/05-create.png)

**6. POST /api/products with a missing field (422)**
![06-missing field](screenshots/06-missing-field.png)

**7. GET /api/products/1 (200)**
![07-first product](screenshots/07-first-product.png)

**8. GET /api/products/99999 (404)**
![08-error](screenshots/08-error.png)

**9. PUT /api/products/1 with changed data (200)**
![09-update](screenshots/09-update.png)

**10. DELETE /api/products/1 (204)**
![10-delete](screenshots/10-delete.png)

## Why does DELETE return 204 and not 200?

When a product is deleted, it no longer exists, so there is nothing left for the server to send back. A 200 usually comes with data in the response, like the product details, but here there is none. The status 204 means "No Content," which tells the client that the request worked and the body is empty on purpose. It is a cleaner way to say "done, nothing more to show."