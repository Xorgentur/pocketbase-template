# PocketBase on Railway

PocketBase is an open-source backend in a single file—database, auth, file storage, and admin dashboard included.

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/deploy/sR-Cq9?referralCode=xorg)

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `PB_ENCRYPTION_KEY` | 32-character key to encrypt sensitive settings (e.g. SMTP passwords) | No |

Generate an encryption key:
```bash
openssl rand -base64 32 | tr -d '=' | cut -c1-32
```

## Updating PocketBase

Change `PB_VERSION` in the Dockerfile and redeploy. All user data in `/pb/pb_data` persists across updates.

---

**Note:** After deployment, visit `/_/` to create your first superuser.
