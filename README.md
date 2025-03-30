# Using JSON File as an API in React

This guide will show you different ways to use a JSON file as an API in your React project.

---

## ✅ 1. Using `public/` Folder (Recommended for Static JSON)
If you have a static `data.json` file, place it inside the `public/` folder and fetch it using `fetch()`.

### 📌 Steps:
1. Place your `data.json` file inside the `public/` folder.
2. Fetch the data inside your React component.

```jsx
import { useEffect, useState } from "react";

function App() {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetch("/data.json") // No need to specify public/ in path
      .then((response) => response.json())
      .then((json) => setData(json))
      .catch((error) => console.error("Error fetching JSON:", error));
  }, []);

  return (
    <div>
      <h1>JSON Data</h1>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  );
}

export default App;
```

✅ **Best for:** Static JSON data that doesn’t change frequently.

---

## ✅ 2. Using a Local JSON File Inside `src/`
You can also store JSON inside the `src/` folder and import it directly.

### 📌 Steps:
1. Place your `data.json` inside `src/`.
2. Import the JSON file inside your component.

```jsx
import data from "./data.json";

function App() {
  return (
    <div>
      <h1>JSON Data</h1>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  );
}

export default App;
```

✅ **Best for:** Small datasets that are part of your source code.

---

## ✅ 3. Running a Local JSON Server (Fake API)
If you want a real API-like experience, use `json-server`.

### 📌 Steps:
1. Install `json-server` globally:
   ```sh
   npm install -g json-server
   ```
2. Create a `db.json` file with your data:
   ```json
   {
     "users": [
       { "id": 1, "name": "Alice" },
       { "id": 2, "name": "Bob" }
     ]
   }
   ```
3. Run the JSON server:
   ```sh
   json-server --watch db.json --port 5000
   ```
4. Fetch data in React:
   ```jsx
   import { useEffect, useState } from "react";

   function App() {
     const [users, setUsers] = useState([]);

     useEffect(() => {
       fetch("http://localhost:5000/users")
         .then((res) => res.json())
         .then((data) => setUsers(data))
         .catch((err) => console.error(err));
     }, []);

     return (
       <div>
         <h1>Users List</h1>
         <ul>
           {users.map((user) => (
             <li key={user.id}>{user.name}</li>
           ))}
         </ul>
       </div>
     );
   }

   export default App;
   ```

✅ **Best for:** Simulating a backend API without writing server code.

---

## ✅ 4. Hosting JSON Online (Mock API)
If you want a free hosted API, use **Mockaroo** or **JSONPlaceholder**.

Example with JSONPlaceholder:
```jsx
useEffect(() => {
  fetch("https://jsonplaceholder.typicode.com/users")
    .then((res) => res.json())
    .then((data) => setUsers(data));
}, []);
```

✅ **Best for:** Testing API requests with mock data.

---

## 🚀 Which Method Should You Use?
| **Method** | **Best for** |
|------------|-------------|
| `public/` Folder | Static JSON files |
| `src/` Folder | Small local JSON files |
| `json-server` | Fake API for development |
| Online Mock API | Quick testing |

Let me know if you need further clarification! 🚀😊
