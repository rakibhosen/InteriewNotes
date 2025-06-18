# ✅ Tracking vs. No-Tracking in Entity Framework Core (.NET C#)

In **Entity Framework Core (.NET)**, how you query data determines whether the **context tracks entity changes**. This impacts memory usage, performance, and how updates are handled.

---

## 🔍 Tracking in EF Core

EF Core **tracks entities by default**. It keeps a record of all changes made to retrieved entities. When you call `SaveChanges()`, it automatically generates the necessary SQL statements.

### 🟢 Use Tracking When:
- You want to **update**, **delete**, or detect changes in the data.

### ✅ Example:
```csharp
var customer = await _context.Customers.FirstOrDefaultAsync(c => c.Id == 1);

if (customer != null)
{
    customer.Name = "Updated Name";
    await _context.SaveChangesAsync(); // EF Core tracks and saves changes
}

| Feature              | Tracking (Default)       | No-Tracking (`AsNoTracking()`)          |
| -------------------- | ------------------------ | --------------------------------------- |
| Change Tracking      | ✅ Yes                    | ❌ No                                    |
| Suitable for Updates | ✅ Yes                    | ❌ No (manual attach needed)             |
| Read Performance     | ❌ Slower (more overhead) | ✅ Faster                                |
| Memory Usage         | ❌ Higher                 | ✅ Lower                                 |
| Default in EF Core   | ✅ Yes                    | ❌ No (explicitly use `.AsNoTracking()`) |

