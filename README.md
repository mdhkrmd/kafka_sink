# Kafka Target Sink Compose

Menjalankan Kafka target single-node dengan Kafka Connect, Schema Registry, dan Kafka UI untuk simulasi Sink Kafka / MirrorSourceConnector.

## Jalankan

```bash
docker compose up -d --build
```

## Akses

- Kafka external bootstrap server: `localhost:29092`
- Kafka internal bootstrap server: `kafka-target:9093`
- Kafka SASL_PLAINTEXT listener: `kafka-target:9094`
- Kafka SSL listener: `kafka-target:9095`
- Kafka SASL_SSL listener: `kafka-target:9096`
- Kafka Connect REST API: `http://localhost:8084`
- Kafka UI: `http://localhost:8090`
- Schema Registry: `http://localhost:8082`

## SSL/SASL Secrets

Generate dev JKS dan file ConfigProvider dari repo dashboard:

```bash
cd /home/andhika/Python/Data\ Engineering/unem-cdc-dashboard
./scripts/generate-dev-kafka-certs.sh
```

Folder `secrets` di-mount ke container Connect sebagai `/kafka/secrets`. Di UI Kafka Sink, isi truststore/keystore location sebagai path container, bukan path laptop/browser, misalnya `/kafka/secrets/target.truststore.jks`.

Kafka Connect target sudah mengaktifkan FileConfigProvider. Reference contoh:

```text
${file:/kafka/secrets/source.properties:sasl.jaas.config}
${file:/kafka/secrets/source.properties:truststore.password}
${file:/kafka/secrets/target.properties:sasl.jaas.config}
${file:/kafka/secrets/target.properties:truststore.password}
```

Untuk fitur upload JKS dari UI, `kconnect-target` juga me-mount `../unem-cdc-dashboard/uploads/connect-secrets` sebagai `/kafka/secrets/uploads:ro`. Buat directory ini di repo dashboard sebelum recreate stack jika belum ada.

## Stop

```bash
docker compose down
```

Kalau ingin ikut menghapus volume data Kafka:

```bash
docker compose down -v
```
