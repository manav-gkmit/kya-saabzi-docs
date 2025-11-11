# Environment

This section lists all the dependencies and environment required for **Kya Saabzi**

---

## `backend/requirements.txt` {data-toc-label="Backend"}
```txt
fastapi==0.110.2
uvicorn[standard]==0.29.0
SQLAlchemy==2.0.30
alembic==1.13.1
psycopg[binary]>=3.2.2
pydantic==2.8.2
pydantic-settings==2.2.1
passlib[bcrypt]==1.7.4
python-jose[cryptography]==3.3.0
python-dotenv==1.0.1
httpx==0.27.0
pytest==8.2.0
pytest-asyncio==0.23.6

# For cleaner code
black==24.4.2
isort==5.13.2
flake8==7.1.0
```

## `frontend/package.json` {data-toc-label="Frontend"}
```json
{
  "name": "kya-saabzi-frontend",
  "version": "1.0.0",
  "private": true,
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  },
  "devDependencies": {
    "vite": "^5.0.10",
    "vite-plugin-pwa": "^0.17.5",
    "eslint": "^8.57.0",
    "prettier": "^3.3.0"
  }
}
```