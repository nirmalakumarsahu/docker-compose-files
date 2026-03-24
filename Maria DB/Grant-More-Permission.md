# 🧑‍💻 1. Login as Root First

```bash
docker exec -it mariadb mariadb -u root -p
```

Enter password:

```
root
```

---

# 🔐 2. Your Current User (`<DATABASE USERNAME>`)

Right now, Docker already did this internally:

```sql
GRANT ALL PRIVILEGES ON <DATABASE NAME>.* TO '<DATABASE USERNAME>'@'%';
```

👉 So no need to repeat unless you want to modify access.

---

# 🚀 3. Grant More Permissions (Options)

## ✅ Option 1: Allow user to create databases (Recommended for dev)

```sql
GRANT CREATE ON *.* TO '<DATABASE USERNAME>'@'%';
FLUSH PRIVILEGES;
```

👉 Now user can:

* ✔ Create new DBs
* ❌ Not full admin

---

## ✅ Option 2: Full Admin Access (like root) ⚠️

```sql
GRANT ALL PRIVILEGES ON *.* TO '<DATABASE USERNAME>'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

👉 Now user can:

* ✔ Create DB
* ✔ Drop DB
* ✔ Grant permissions to others

⚠️ Use only for:

* Local development
* Testing

---

## ✅ Option 3: Access Multiple Databases (Best Practice)

```sql
GRANT ALL PRIVILEGES ON <DATABASE NAME>.* TO '<DATABASE USERNAME>'@'%';
GRANT ALL PRIVILEGES ON <OTHER DATABASE NAME>.* TO '<DATABASE USERNAME>'@'%';
FLUSH PRIVILEGES;
```

---

## ✅ Option 4: Read-Only User (for reporting)

```sql
GRANT SELECT ON <DATABASE NAME>.* TO '<DATABASE USERNAME>'@'%';
FLUSH PRIVILEGES;
```

---

# 🧪 Verify Permissions

```sql
SHOW GRANTS FOR '<DATABASE USERNAME>'@'%';
```

---