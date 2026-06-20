# Kafka 3.9 Compose

Menjalankan Kafka 3.9 single-node dengan mode KRaft dan `kafka-ui`.

## Jalankan

```bash
docker compose up -d
```

## Akses

- Kafka bootstrap server: `localhost:9092`
- Kafka UI: `http://localhost:8080`

## Stop

```bash
docker compose down
```

Kalau ingin ikut menghapus volume data Kafka:

```bash
docker compose down -v
```
