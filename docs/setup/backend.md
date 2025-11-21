# Environment

This section lists all the dependencies and environment required for **Kya Saabzi Backend** [:fontawesome-brands-github:](https://github.com/manav-gkmit/kya-saabzi-backend/)

---

## Installation

### Clone the repository for yourself
```console
git clone https://github.com/manav-gkmit/kya-saabzi-backend.git  

cd kya-saabzi-backend
```

### Initialize a virtual environment and install the dependencies
```console
python3 -m venv venv  

pip3 install -r requirements.txt

---> 100%
```

### Create PostgreSQL Database 
```sql
CREATE DATABASE mydb;

\c mydb
```
and make sure you have privileges to create tables. Then create/configure `.env` file:

```console
DATABASE_URL=postgres://YourUserName:YourPassword@YourHostname:5432/mydb
SECRET_KEY=yoursecretkey
CORS_ORIGINS=["http://localhost:5173"]
```

### Run the alembic migrations
```bash
alembic upgrade head
```

### Run the backend

```console
uvicorn app.main:app --reload
```