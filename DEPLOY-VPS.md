# Despliegue en el VPS upflowi vía Komodo

Este fork tiene el `docker-compose.yml` adaptado para correr detrás de
Nginx Proxy Manager en el VPS upflowi (sin `ports:` públicos, con la red
externa `proxy` en `cap-web` y `minio`).

## Antes de desplegar

Al crear el Stack en Komodo, completa el campo **Environment** con estas
variables (los valores reales te los pasó Claude por chat — nunca se
commitean a este repo):

```
NEXTAUTH_SECRET=
DATABASE_ENCRYPTION_KEY=
MEDIA_SERVER_WEBHOOK_SECRET=
MYSQL_PASSWORD=
MYSQL_ROOT_PASSWORD=
MINIO_ROOT_USER=
MINIO_ROOT_PASSWORD=
CAP_URL=https://cap.flowi.it.com
S3_PUBLIC_URL=https://cap-storage.flowi.it.com
```

## Dominios

- App: `cap.flowi.it.com` → contenedor `cap-web`, puerto `3000`
- Storage (API S3): `cap-storage.flowi.it.com` → contenedor `cap-minio`,
  puerto `9000`

Ambos Proxy Hosts + SSL en NPM se crean por separado (no los gestiona
Komodo). La consola de administración de MinIO (puerto `9001`) queda
intencionalmente sin publicar a internet.

## Requisito en el servidor

La red externa `proxy` debe existir de antemano en el servidor
(`docker network create proxy` si no existiera — en upflowi ya existe).
