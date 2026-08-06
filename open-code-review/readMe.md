# Open Code Review (OCR)
https://open-codereview.ai/docs/mcp
## What is Open Code Review?

Open Code Review (OCR) is an AI-powered code review system. Instead of interacting with your application like a user, it analyzes your source code and provides feedback similar to what an experienced Senior Developer would during a Pull Request review.

Its primary goal is to improve code quality by identifying bugs, security issues, performance problems, architecture concerns, and violations of best practices before the code reaches production.

Think of it as an AI reviewer rather than an AI programmer.

---

# How Does It Work?

Instead of reading an entire project every time, OCR mainly focuses on the code that has changed.

For example:

```text
Project
50,000+ lines of code

Modified:
app/Http/Controllers/Controller.php
+25 lines
```

Rather than analyzing the entire application, OCR reviews only those modified lines and their surrounding context.

This makes reviews:

* Faster
* Cheaper
* More focused
* More relevant

---

# What Can Open Code Review Detect?

## 1. Logic Bugs

Example:

```php
if ($user->isAdmin()) {
    // ...
}
```

Possible review:

* Possible null reference.
* Missing null check.

---

## 2. Security Issues

Examples:

* Missing authorization
* SQL Injection risks
* XSS vulnerabilities
* Insecure file uploads
* Missing permission checks

Example:

```php
Order::find($id);
```

Possible review:

> Missing authorization before accessing the order.

---

## 3. Validation Problems

Example:

```php
Order::create($request->all());
```

Possible review:

* Missing request validation.
* Potential Mass Assignment vulnerability.

---

## 4. Performance Problems

Example:

```php
foreach ($orders as $order) {
    User::find($order->user_id);
}
```

Possible review:

* Possible N+1 Query.
* Consider eager loading.

---

## 5. Architecture Issues

OCR can identify:

* Business logic inside controllers
* Large classes
* Large methods
* Duplicate code
* Poor separation of responsibilities

Example:

```text
OrderController
3000 lines
```

Possible review:

> Move business logic into a dedicated Service class.

---

## 6. Laravel Best Practices

OCR can suggest improvements such as:

* Form Requests
* Policies
* Route Model Binding
* Dependency Injection
* Eager Loading
* Service Layer
* Repository Pattern (when appropriate)

---
