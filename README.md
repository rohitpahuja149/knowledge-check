# TODO Module API (Server-Rendered Routes)

This app exposes server-rendered TODO routes from `index.js` (no auth module, no API tokens).

**Base URL:** `http://localhost:3000`  
**Content type for form posts:** `application/x-www-form-urlencoded`

## Endpoints

### 1) List todos
- **Method:** `GET`
- **Route:** `/`
- **Description:** Renders the home page with all todos.

**Example request**
```bash
curl -i http://localhost:3000/
```

**Example response**
```http
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8

<!DOCTYPE html>
<html>...Things To Do...<li>Go to the gym</li>...</html>
```

---

### 2) View a single todo
- **Method:** `GET`
- **Route:** `/todo/:id`
- **Description:** Renders one todo by ID.

**Example request**
```bash
curl -i http://localhost:3000/todo/9f2a1c9d-aaaa-bbbb-cccc-1234567890ab
```

**Example response**
```http
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8

<!DOCTYPE html>
<html>...<h1>Go to the gym</h1>...<p>Start with a warm-up...</p>...</html>
```

---

### 3) Add page (new todo form)
- **Method:** `GET`
- **Route:** `/addTodo`
- **Description:** Renders the "Add todo" form page.

**Example request**
```bash
curl -i http://localhost:3000/addTodo
```

**Example response**
```http
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8

<!DOCTYPE html>
<html>...<form action="/createTodo" method="POST">...</form>...</html>
```

---

### 4) Create todo
- **Method:** `POST`
- **Route:** `/createTodo`
- **Description:** Creates a todo (`id` generated server-side), then redirects to `/`.
- **Body fields:** `name`, `about`

**Example request**
```bash
curl -i -X POST http://localhost:3000/createTodo \
  -H "Content-Type: application/x-www-form-urlencoded" \
  --data "name=Buy%20milk&about=2%20liters%20from%20store"
```

**Example response**
```http
HTTP/1.1 302 Found
Location: /
```

---

### 5) Edit page (existing todo form)
- **Method:** `GET`
- **Route:** `/edit/:id`
- **Description:** Renders the edit form pre-filled with the selected todo.

**Example request**
```bash
curl -i http://localhost:3000/edit/9f2a1c9d-aaaa-bbbb-cccc-1234567890ab
```

**Example response**
```http
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8

<!DOCTYPE html>
<html>...<form action="/edit/save" method="POST">...</form>...</html>
```

---

### 6) Save edited todo
- **Method:** `POST`
- **Route:** `/edit/save`
- **Description:** Updates a todo by submitted `id`, then redirects to `/`.
- **Body fields:** `id`, `name`, `about`

**Example request**
```bash
curl -i -X POST http://localhost:3000/edit/save \
  -H "Content-Type: application/x-www-form-urlencoded" \
  --data "id=9f2a1c9d-aaaa-bbbb-cccc-1234567890ab&name=Gym&about=Cardio%20then%20weights"
```

**Example response**
```http
HTTP/1.1 302 Found
Location: /
```

---

### 7) Delete todo
- **Method:** `GET`
- **Route:** `/delete/:id`
- **Description:** Deletes a todo by ID, then redirects to `/`.
- **Note:** The current implementation performs deletion via `GET` (as defined in `index.js`).

**Example request**
```bash
curl -i http://localhost:3000/delete/9f2a1c9d-aaaa-bbbb-cccc-1234567890ab
```

**Example response**
```http
HTTP/1.1 302 Found
Location: /
```
