# Mania Group — offsite backup

Файл `db-latest.sql.gz.enc` — дамп бази, зашифрований AES-256-CBC
(openssl, PBKDF2, 200k ітерацій). Репозиторій публічний вимушено:
акаунту заборонені приватні репозиторії (trade controls), тому вміст
зашифровано.

Без ключа файл марний. Ключ зберігається окремо у власника.

## Відновлення

```bash
openssl enc -d -aes-256-cbc -pbkdf2 -iter 200000 \
  -in db-latest.sql.gz.enc -out db.sql.gz -pass file:./backup-key
gunzip db.sql.gz && psql "$DATABASE_URL" < db.sql
```
