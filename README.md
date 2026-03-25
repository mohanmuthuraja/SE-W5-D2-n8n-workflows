# 🚀 n8n Workflow Guide — Basics to Conditional Automation

This repository/document provides a beginner-to-intermediate overview of **n8n workflows**, covering node types, expressions, and sample workflows.

---

# 📌 What is an n8n Node?

An **n8n Node** is the fundamental building block of a workflow.

👉 Each node performs a specific task:

* Triggering workflows
* Processing data
* Calling APIs
* Transforming data
* Controlling execution flow

---

# 🧩 Types of Nodes in n8n

## 🔹 1. Trigger Nodes

* Start the workflow
* Executes when an event occurs

**Examples:**

* Webhook Trigger
* Schedule Trigger
* Telegram Trigger
* Manual Trigger

---

## 🔹 2. Regular / Action Nodes

* Perform operations after trigger
* Execute business logic

**Examples:**

* Send Email
* Create Record
* Update Data

---

## 🔹 3. Core Nodes

Essential nodes used in most workflows.

### ✅ Code Node

* Write custom JavaScript
* Used for advanced logic and transformations

```javascript
return items.map(item => {
  return {
    json: {
      message: "Hello " + item.json.name
    }
  };
});
```

---

### ✅ HTTP Request Node

* Call external APIs
* Supports GET, POST, PUT, DELETE

Use cases:

* Fetch data from API
* Send data to external systems

---

### ✅ Webhook Node

* Exposes a URL
* Allows external systems to trigger workflows

---

## 🔹 4. Flow Control Nodes

Control execution path of workflows.

**Examples:**

* IF Node (conditions)
* Switch Node
* Loop / Split In Batches
* Merge Node

---

## 🔹 5. Data Transformation Nodes

Used to manipulate data inside workflows.

**Examples:**

* Set Node
* Edit Fields
* Rename Keys
* Remove Duplicates
* Code Node (advanced transformation)

---

# 🧠 Expressions in n8n

Expressions allow dynamic values using JavaScript syntax.

### Example:

```javascript
{{ $json.name }}
{{ $json.age > 25 ? "Adult" : "Minor" }}
```

### Common Usage:

* Access incoming data
* Perform calculations
* Conditional logic

---

# 🧪 Exercises in n8n

## ✅ 1. Hello World Application

### Workflow:

1. Schedule Trigger (daily execution)
2. Constant Field Node (Name = "Mohan")
3. Greetings Node

### Output:

```text
Hi Mohan, Welcome to Social Eagle
```

---

## ✅ 2. Sample Workflow — Conditional Flows

### Objective:

Process multiple user records and classify based on age.

### Steps:

1. Input JSON records (name, age, city)
2. Convert JSON → JS (Code Node)
3. Loop through records
4. Apply condition:

   * If age < 27 → Young
   * Else → Old

---

### Logic:

```text
IF age < 27 → TRUE → Person is Young
ELSE → FALSE → Person is Old
```

---

# 🔄 Example Flow Structure

```text
Trigger → JSON Data → Code → Loop → IF → True/False Paths
```

---

# 📊 Key Concepts Summary

| Concept      | Description       |
| ------------ | ----------------- |
| Trigger Node | Starts workflow   |
| Action Node  | Performs task     |
| Code Node    | Custom logic      |
| HTTP Node    | API calls         |
| Webhook      | External trigger  |
| IF Node      | Conditional logic |
| Expressions  | Dynamic values    |

---

# 💡 Best Practices

* Use **Code Node** only when needed
* Prefer **built-in nodes** for simplicity
* Use **Expressions** instead of hardcoding values
* Keep workflows modular and readable
* Test using **Execute Workflow**

---

# 🚀 Next Steps

* Build Telegram Bot using n8n
* Integrate AI (OpenAI / Gemini)
* Add database (Google Sheets / MySQL)
* Implement error handling workflows

---

# 📎 Notes

* All executions can be tracked in **Execution Tab**
* Use **Active mode** for production workflows
* Use **Test mode** for debugging

---

# 🙌 Conclusion

n8n provides a powerful low-code platform to build automation workflows using:

* Visual nodes
* JavaScript logic
* API integrations

Mastering nodes + expressions + flow control = powerful automation 🚀

---
