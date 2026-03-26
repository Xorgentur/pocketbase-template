# Deploy and Host PocketBase on Railway

PocketBase is an open-source backend in a single file—database (SQLite), authentication, file storage, and admin dashboard included. No configuration required, deploy instantly.

## About Hosting PocketBase

Deploying PocketBase on Railway is straightforward with a containerized setup. The template includes a Dockerfile that downloads the official PocketBase binary, exposes port 8080, and configures the service to accept connections from any host. Data is stored persistently on Railway's volume system. After deployment, you create your first superuser via the admin panel or through the deploy logs. No external database or additional services are required.

## Common Use Cases

- **Rapid prototyping** with built-in auth and file storage
- **Internal tools and admin dashboards** for teams
- **Mobile/web app backends** with REST API and real-time subscriptions

## Dependencies for PocketBase Hosting

- [Dockerfile](Dockerfile) - Container definition using Alpine Linux
- [Railway Volume](https://docs.railway.com/reference/volumes) - Persistent storage for SQLite database

### Deployment Dependencies

- [PocketBase GitHub Repository](https://github.com/pocketbase/pocketbase)
- [PocketBase Documentation](https://pocketbase.io/docs/)

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `PB_ENCRYPTION_KEY` | 32-character key to encrypt sensitive settings (e.g. SMTP passwords) | No |
| `GOMEMLIMIT` | Memory limit to prevent OOM crashes in MB (e.g. `512`, `1024`) | No |

## After Deployment

1. **Access the admin panel:** Visit `https://your_domain_here.railway.app/_/` after deployment
2. **Create your superuser:** If you see a login screen instead of a setup page, check the **Deploy Logs** in Railway dashboard for a direct link to create your first admin user

![Deploy Logs showing superuser creation link](https://raw.githubusercontent.com/Xorgentur/pocketbase-template/main/assets/deploy_log.png)

## Why Deploy PocketBase on Railway?

Railway is a singular platform to deploy your infrastructure stack. Railway will host your infrastructure so you don't have to deal with configuration, while allowing you to vertically and horizontally scale it.

By deploying PocketBase on Railway, you are one step closer to supporting a complete full-stack application with minimal burden. Host your servers, databases, AI agents, and more on Railway.
