FROM python:3.12-alpine

WORKDIR /app

# Crear usuario no-root
RUN addgroup -S app && adduser -S app -G app

# Copiar dependencias
COPY requirements.txt .

# Instalar dependencias
RUN pip install --no-cache-dir -r requirements.txt

# Copiar código
COPY app.py .

# Crear carpeta para logs
RUN mkdir -p /var/log/app && chown -R app:app /var/log/app

# Cambiar a usuario no-root
USER app

# Exponer puerto
EXPOSE 8080

# Healthcheck del contenedor
HEALTHCHECK --interval=10s --timeout=3s --retries=5 \
  CMD wget -qO- http://localhost:8080/health >/dev/null || exit 1

# Ejecutar aplicación
CMD ["python", "/app/app.py"]