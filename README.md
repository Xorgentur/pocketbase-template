# PocketBase on Railway

PocketBase is an open-source backend in a single file—database, auth, file storage, and admin dashboard included.

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/deploy/sR-Cq9?referralCode=xorg)

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `PB_ENCRYPTION_KEY` | 32-character key to encrypt sensitive settings (e.g. SMTP passwords) | No |
| `GOMEMLIMIT` | Memory limit to prevent OOM crashes in MB (e.g. `512`, `1024`) | No |

---

## After deployment

**First-time setup:** After deployment, visit `https://your_domain_here.railway/_/` to create your first superuser.
**You only see a login screen?:** In this case you need to look into the "Deploy Logs"
