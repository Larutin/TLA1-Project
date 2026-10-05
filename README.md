# 💰 Enterprise Income Tracker (React + Vite)

A React application refactored from our Vanilla JavaScript Income Category Ledger for **Finals TLA 1**.

- **GitHub Repository:** GitHub Repository: https://github.com/clarutin230000001521/TLA1-Project

---

## 📋 Architectural Overview: Vanilla JavaScript vs. React Refactor

This application transitions the original Vanilla JavaScript implementation from direct DOM manipulation into a React functional component model:

| Architectural Concept | Vanilla JavaScript | React Application |
| :--- | :--- | :--- |
| **Input Management** | Direct DOM element access | Controlled inputs using `useState` |
| **Event Handling** | `addEventListener()` | React events such as `onSubmit`, `onChange`, and `onClick` |
| **Data Storage** | DOM elements | `categories` state array |
| **Adding Records** | Dynamically creates HTML elements | Adds objects to React state |
| **Updating Records** | Directly modifies DOM elements | Uses `map()` to update the selected category |
| **Deleting Records** | Removes DOM elements | Uses `filter()` to remove a category |
| **Searching** | Manual DOM filtering | Uses `filter()` and `includes()` |
| **UI Rendering** | Direct DOM manipulation | React re-renders when state changes |

---

## 🤖 AI Implementation & Code Defense

### 1. Features Developed with AI Assistance

AI assistance was used throughout the refactoring and development process to help improve the application's React structure and functionality:

* **React Conversion:** Assisted in converting the original HTML, CSS, and JavaScript application into a React application using JSX and `useState`.
* **State Management:** Assisted in managing category names, descriptions, category records, search text, and editing status using React state.
* **CRUD Features:** Assisted in implementing Add, Edit, and Delete functionality for income categories.
* **Search & Validation:** Assisted in creating the search feature, required-field validation, and duplicate category checking.
* **UI Design:** Assisted in creating the enterprise-style dashboard layout and responsive CSS design.

---

### 2. Technical Explanation & Code Defense

#### **A. React State Management (`App.jsx`)**

The application uses `useState` to manage the data that changes while the application is running:

```jsx
const [categoryName, setCategoryName] = useState("");
const [categoryDesc, setCategoryDesc] = useState("");
const [categories, setCategories] = useState([]);
const [search, setSearch] = useState("");
const [editingId, setEditingId] = useState(null);

Each state has a specific purpose: `categoryName` stores the category name, `categoryDesc` stores the description, `categories` stores all category records, `search` stores the search text, and `editingId` identifies the category currently being edited.

#### **B. Adding Categories**

The `handleAddCategory()` function validates the input before adding a new category:

```jsx
if (!categoryName.trim() || !categoryDesc.trim()) {
  alert("Please complete both input fields.");
  return;
}
```

A new category is added using the spread operator:

```jsx
setCategories([
  ...categories,
  {
    id: Date.now(),
    name: categoryName.trim(),
    description: categoryDesc.trim(),
    date: new Date().toLocaleDateString()
  }
]);
```

The spread operator keeps the existing categories while adding the new record.

#### **C. Duplicate Validation**

The `some()` method checks if another category already has the same name:

```jsx
const duplicate = categories.some(
  (category) =>
    category.name.toLowerCase() === categoryName.trim().toLowerCase() &&
    category.id !== editingId
);
```

This prevents duplicate category names while still allowing the current category to be edited.

#### **D. Editing Categories**

When the user selects Edit, the category information is placed back into the form:

```jsx
setCategoryName(category.name);
setCategoryDesc(category.description);
setEditingId(category.id);
```

The `map()` method then updates only the selected category:

```jsx
categories.map((category) =>
  category.id === editingId
    ? {
        ...category,
        name: categoryName.trim(),
        description: categoryDesc.trim()
      }
    : category
)
```

The matching category is updated while the other records remain unchanged.

#### **E. Deleting Categories**

The `filter()` method removes the selected category from the state:

```jsx
setCategories(
  categories.filter((category) => category.id !== id)
);
```

Only the category whose ID matches the selected ID is removed.

#### **F. Search and Filtering**

The application uses `filter()` and `includes()` to search the category name and description:

```jsx
const filteredCategories = categories.filter((category) =>
  category.name.toLowerCase().includes(search.toLowerCase()) ||
  category.description.toLowerCase().includes(search.toLowerCase())
);
```

This creates a filtered list without modifying the original `categories` state.

#### **G. Declarative Rendering**

React uses `map()` to display the filtered categories:

```jsx
{filteredCategories.map((category) => (
  <div className="category" key={category.id}>
    <h3>{category.name}</h3>
    <p>{category.description}</p>
  </div>
))}
```

The `key={category.id}` allows React to identify each category when the list changes.

#### **H. Controlled Inputs and Form Submission**

The input fields are controlled by React state:

```jsx
<input
  type="text"
  value={categoryName}
  onChange={(event) =>
    setCategoryName(event.target.value)
  }
/>
```

The form uses `onSubmit` to handle submission through React:

```jsx
function handleSubmit(event) {
  event.preventDefault();
  handleAddCategory();
}
```

`event.preventDefault()` prevents the browser from refreshing the page when the form is submitted.

## 🛠️ Tech Stack & Dependencies

Framework: React 19

Build Tool: Vite

Language: JavaScript / JSX

Styling: CSS

Version Control: Git & GitHub

Package Manager: npm

Dependencies: React, React DOM, and Bootstrap
