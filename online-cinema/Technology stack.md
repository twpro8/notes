# Technology stack

### **FastAPI**  
- Authentication and authorization (JWT/OAuth2)  
- Protected routes for authenticated users and for administrators  
- Routes for CRUD operations for all entities  
- WebSockets for sync data between users  
- FastAPI streaming and routers for it  
- Routers for streaming uploading  
  
### **SQLAlchemy**  
- ORM models for all entities  
- Relationships and polymorphism  
- Repositories and services for separating logic from API  
- Alembic migrations  
- Optimized queries  
  
### **Redis**  
- Creating redis cache  
- Caching popular queries (films/series catalog, ratings)  
- Caching frequently used data  
- TTL (Time to Live) for cache  
- Storing user sessions  
  
### **Celery**  
- Sending email/push notifications (email confirmation, new releases, new message)  
- Uploading films/series/images etc.  
- Cleaning outdated data (tokens, cache)  
- Scheduled tasks (e.g. updating collections)  
  
### **PostgreSQL**  
- Storing all information (films, users, playlists, favorites, etc.)  
- Indexes to speed up search  
  
---