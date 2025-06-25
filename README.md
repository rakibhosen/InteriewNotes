
# ✅ Tracking vs. No-Tracking in Entity Framework Core (.NET C#)

In **Entity Framework Core**, how you query data determines whether the **context tracks entity changes**. This affects memory usage, performance, and how updates are managed.

---

## 🔍 Tracking in EF Core

EF Core **tracks entities by default**. It keeps a record of all changes made to retrieved entities. When you call `SaveChanges()`, it automatically generates the SQL statements needed to persist those changes.

### 🟢 Use Tracking When:

* You want to **update**, **delete**, or monitor changes in the data.

### ✅ Example:

```csharp
var customer = await _context.Customers.FirstOrDefaultAsync(c => c.Id == 1);

if (customer != null)
{
    customer.Name = "Updated Name";
    await _context.SaveChangesAsync(); // EF Core tracks and saves changes
}
```

---

## 📊 Tracking vs. No-Tracking Comparison

| Feature              | Tracking (Default)       | No-Tracking (`AsNoTracking()`)    |
| -------------------- | ------------------------ | --------------------------------- |
| Change Tracking      | ✅ Yes                    | ❌ No                              |
| Suitable for Updates | ✅ Yes                    | ❌ No (manual attach needed)       |
| Read Performance     | ❌ Slower (more overhead) | ✅ Faster                          |
| Memory Usage         | ❌ Higher                 | ✅ Lower                           |
| Default in EF Core   | ✅ Yes                    | ❌ No (must use `.AsNoTracking()`) |

---

## 🔍 SSR vs. CSR in Web Development

| Action              | SSR (Server-Side Rendering) | CSR (Client-Side Rendering)    |
| ------------------- | --------------------------- | ------------------------------ |
| First Page Load     | Full HTML sent every time   | HTML shell + JS sent once      |
| New Page Navigation | New full HTML from server   | Handled by JS, no page reload  |
| HTML Requests       | On every page visit         | Only once; JS handles the rest |


