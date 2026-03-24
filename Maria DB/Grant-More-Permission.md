# 🧑‍💻 1. Login as Root First

```bash
docker exec -it mariadb mariadb -u root -p
```

Enter password:

```
root
```

---

# 🔐 2. Your Current User (`nirmala`)

Right now, Docker already did this internally:

```sql
GRANT ALL PRIVILEGES ON moltaai.* TO 'nirmala'@'%';
```

👉 So no need to repeat unless you want to modify access.

---

# 🚀 3. Grant More Permissions (Options)

## ✅ Option 1: Allow user to create databases (Recommended for dev)

```sql
GRANT CREATE ON *.* TO 'nirmala'@'%';
FLUSH PRIVILEGES;
```

👉 Now user can:

* ✔ Create new DBs
* ❌ Not full admin

---

## ✅ Option 2: Full Admin Access (like root) ⚠️

```sql
GRANT ALL PRIVILEGES ON *.* TO 'nirmala'@'%' WITH GRANT OPTION;
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
GRANT ALL PRIVILEGES ON moltaai.* TO 'nirmala'@'%';
GRANT ALL PRIVILEGES ON another_db.* TO 'nirmala'@'%';
FLUSH PRIVILEGES;
```

---

## ✅ Option 4: Read-Only User (for reporting)

```sql
GRANT SELECT ON moltaai.* TO 'nirmala'@'%';
FLUSH PRIVILEGES;
```

---

# 🧪 Verify Permissions

```sql
SHOW GRANTS FOR 'nirmala'@'%';
```

---