# Project Reflection

This report details the reflections on the development, deployment, and overall life-cycle of the full stack application project.

## 1. What Went Well
- The transition from static frontend to a fully dynamic REST API went smoothly.
- Structuring the application into distinct client and server directories improved maintainability.
- Integration of SQLite via `better-sqlite3` was efficient and straightforward, bypassing complex database setup steps during development.
- Securely handling authentication with JWT and bcrypt enhanced the overall security posture.

## 2. Challenges Faced
- **Dependency Versioning**: Moving up to Node.js 24 required ensuring all native modules (like SQLite bindings) were compatible. Resolving these mismatches was essential for a stable deployment.
- **Deployment File System Limitations**: Realizing that cloud platforms often have ephemeral filesystems meant rethinking database storage, highlighting the need for persistent volumes.
- **CORS Configuration**: Handling Cross-Origin Resource Sharing during the transition from local development to a hosted environment initially caused some friction with client-server communication.

## 3. Lessons Learned
- **Environment Parity**: Keeping development environments as close to production as possible (e.g., using `.env` files locally) mitigates deployment surprises.
- **Infrastructure as Code**: Creating deployment scripts (like `render.yaml` or a `Procfile`) makes scaling and migrating hosting providers significantly easier.
- **Security First**: Implementing basic rate limiting and helmet.js headers early in the development cycle prevents having to retrofit security measures later.

## 4. Improvements for Future Projects
- **Database Scalability**: For the next iteration or project, I plan to start with PostgreSQL or MySQL instead of SQLite to better accommodate concurrent connections.
- **Containerization**: Learning to Dockerize the full stack application will allow for seamless deployment on any cloud provider without worrying about underlying system Node.js version disparities.
- **Comprehensive Testing**: Implementing CI/CD pipelines and improving test coverage (E2E testing) would catch regression bugs before they hit production.
