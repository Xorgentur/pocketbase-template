# Deploy and Host PocketBase with Railway

PocketBase is an open-source backend in a single file—real-time database, authentication, file storage, and admin dashboard included. Deploy your backend instantly without complex configuration or multiple services.

[![Deploy on Railway](https://railway.app/button.svg)](https://railway.com?referralCode=xorg)

## About Hosting PocketBase

PocketBase is completely portable and self-contained, requiring zero external dependencies. This template deploys PocketBase using a lightweight Alpine Linux container. The deployment includes persistent storage for your data and automatic health checks. PocketBase serves its own admin dashboard, API, and real-time subscriptions from a single process, making it ideal for rapid prototyping and production applications alike.

## Common Use Cases

- **SaaS Applications:** User authentication, database, and file storage for multi-tenant apps
- **Mobile App Backends:** Real-time sync, push notifications, and user management for iOS/Android apps
- **Prototyping & MVPs:** Rapid backend setup without DevOps complexity
- **Internal Tools:** Admin dashboards, CRUD operations, and team collaboration tools
- **Content Management:** File uploads, rich text editing, and structured content APIs

## Dependencies for PocketBase Hosting

- **Docker:** Container runtime for building and running PocketBase
- **Railway:** Platform-as-a-Service for deployment and infrastructure management
- **Persistent Volume:** Required for storing database files and uploaded assets
- **Optional SMTP Service:** For production email delivery (Mailgun, SendGrid, AWS SES, etc.)

### Deployment Dependencies

- [PocketBase Documentation](https://pocketbase.io/docs/)
- [Railway Documentation](https://docs.railway.com/)
- [PocketBase GitHub](https://github.com/pocketbase/pocketbase)

### Environment Variables

**User-configurable:**

| Variable | Description | Required |
|----------|-------------|----------|
| `PB_ENCRYPTION_KEY` | 32-character key to encrypt sensitive settings (e.g. SMTP passwords). Only used if set. | No |

To generate an encryption key:
```bash
openssl rand -base64 32 | tr -d '=' | cut -c1-32
```

**Railway-provided (read-only, auto-set):**

| Variable | Description |
|----------|-------------|
| `PORT` | Port assigned by Railway, used automatically by the start command |
| `RAILWAY_PUBLIC_DOMAIN` | Public hostname for the PocketBase service |
| `RAILWAY_PRIVATE_DOMAIN` | Private hostname for service-to-service communication within Railway |
| `RAILWAY_VOLUME_MOUNT_PATH` | Volume mount path (`/pb/pb_data`) |
| `RAILWAY_VOLUME_NAME` | Name of the attached volume |

Other Railway services can reference PocketBase using these variables, e.g.:
```
POCKETBASE_URL=https://${{PocketBase.RAILWAY_PRIVATE_DOMAIN}}
```

### Implementation Details

The Docker image uses a minimal Alpine Linux base with PocketBase downloaded at build time. Data is persisted to `/pb/pb_data` via Railway volumes. You can also mount `pb_migrations` and `pb_hooks` directories for custom migrations and JavaScript hooks.

### Updating PocketBase

All user data (database, uploaded files, settings) is stored in the `/pb/pb_data` volume and **persists across updates**.

When this template is updated (e.g. a new PocketBase version is released), Railway will notify you of the available update. Applying the update triggers a new deployment with the updated binary, but your data on the volume remains untouched.

To manually update the PocketBase version, change the `PB_VERSION` argument in the Dockerfile and redeploy.

## Why Deploy PocketBase on Railway?

Railway provides a singular platform to deploy your infrastructure stack with zero configuration. By deploying PocketBase on Railway, you get:

- **Automatic HTTPS:** SSL certificates handled automatically
- **Persistent Storage:** Your data survives redeployments
- **Horizontal Scaling:** Scale vertically and horizontally as needed
- **Private Networking:** Secure service-to-service communication
- **Monitoring & Logs:** Built-in observability for your backend

Deploy PocketBase today and focus on building your application, not managing infrastructure.

---

**Note:** After deployment, visit `/api/health` to verify the service is running, then access the admin dashboard at `/_/` to create your first superuser.
