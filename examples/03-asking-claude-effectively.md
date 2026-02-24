# Example 3: How to Ask Claude Code Effectively

Claude Code is powerful, but the quality of your prompts determines the quality of results.

## The Core Principle

**Give context, not just commands.**

Claude Code can read your entire codebase, but it needs to know:
- What you're trying to achieve
- Where in the codebase to work
- What constraints to follow
- What patterns to match

---

## Prompt Patterns That Work Well

### Pattern 1: Exploration First

Before asking Claude to build something, ask it to understand first.

```
> Explore this codebase. What patterns does it use for:
> - API endpoints
> - Error handling
> - Database queries
> - Component structure
>
> Then summarize the conventions I should follow.
```

This helps Claude match your style when it writes new code.

---

### Pattern 2: The Full Context Prompt

```
> I need to add a "forgot password" flow.
>
> Requirements:
> - User enters their email on /forgot-password
> - If email exists, send a reset link (use the existing EmailService in src/services/email.js)
> - Link expires after 24 hours
> - Reset page at /reset-password?token=xxx validates the token and lets user set new password
>
> Use the existing auth patterns you see in src/routes/auth.js.
> Write the route handlers, the email template, and any DB schema changes needed.
```

---

### Pattern 3: Debugging with Full Error

```
> I'm getting this error when a user tries to upload a profile picture:
>
> TypeError: Cannot read properties of undefined (reading 'path')
>   at uploadHandler (src/routes/users.js:47:23)
>
> Here's what I expect to happen: user selects a file, clicks upload,
> it saves to /uploads and updates the DB with the path.
>
> Find the bug and fix it.
```

---

### Pattern 4: Iterative Refinement

Start simple, then layer on requirements.

```
> Create a ProductCard component that shows name, price, and image.

... review it ...

> Good. Now add an "Add to Cart" button that calls the addToCart prop.

... review it ...

> Now add a loading state while the cart operation is in progress.

... review it ...

> Now write tests for all three states: default, loading, and added.
```

---

### Pattern 5: Understanding Before Changing

When working on unfamiliar code:

```
> Before making any changes, explain to me:
> 1. How does the authentication middleware work?
> 2. What does the session object contain?
> 3. Where are permissions checked?
>
> I want to understand it before we modify it.
```

---

## Anti-Patterns to Avoid

### Too vague

```
# Bad
> Make the app better

# Good
> The product search is slow when there are more than 1000 items.
> Profile it and optimize the query in src/services/products.js
```

### Too many things at once

```
# Bad (too broad, Claude may skip things)
> Add authentication, a shopping cart, payment processing, and an admin dashboard

# Good (one at a time)
> Let's start with authentication. Implement JWT-based login and registration.
```

### No constraints

```
# Bad
> Add a database

# Good
> We're already using PostgreSQL via the pg library (see db/connection.js).
> Add a "orders" table and the CRUD functions for it in src/models/order.js.
```

---

## Useful Openers

| Situation | What to Say |
|---|---|
| New to a codebase | "Give me an overview of this project's structure and conventions" |
| Before a feature | "Where would I add X, given this codebase?" |
| Debugging | "Here's the error + what I expected. Find and fix the bug." |
| Code review | "Review this code for bugs, security issues, and style" |
| Learning | "Explain how [thing] works in this project, line by line" |
| Stuck | "I'm trying to do X but keep hitting Y. What am I missing?" |
