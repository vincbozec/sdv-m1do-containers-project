# Utiliser l'image officielle de Rust
FROM rust:slim AS builder

# Définir le répertoire de travail
WORKDIR /app

# Copier les fichiers de configuration de Cargo
COPY . .

# Construire l'application
RUN cargo build --release

# Utiliser une image Debian pour exécuter l'application
FROM debian:bookworm-slim AS prod

# Installer les dépendances nécessaires
RUN apt-get update && apt-get install -y \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Copier l'application compilée
COPY --from=builder /app/target/release/sdv-api /usr/local/bin/sdv-api

# Exposer le port de l'application
EXPOSE 8000

# Commande pour exécuter l'application
CMD ["sdv-api"]