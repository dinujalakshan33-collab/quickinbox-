# quickinbox-Internet sender ──► Mailgun (MX for mail.yourdomain)
                        │  inbound route, HTTPS POST (HMAC-signed)
                        ▼
              /api/webhooks/inbound   (verify signature → dedupe → store → ack)
                        │
                        ▼
                  PostgreSQL (Prisma)
                        ▲
   Browser ──► /api/inboxes (create, token issued once)
           ──► /api/inboxes/[id]/messages (token required)
           ──► /api/messages/[id] (token required, sanitized HTML)
                        ▲
              Cron /api/cron/expire (deletes past retention)