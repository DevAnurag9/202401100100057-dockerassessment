FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

WORKDIR /app

# Install available OS security updates and clean package cache
RUN apt-get update \
    && apt-get upgrade -y \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt \
    && groupadd --system appgroup \
    && useradd --system --gid appgroup --no-create-home appuser

# Copy application with non-root ownership
COPY --chown=appuser:appgroup app.py .

# Run application without root privileges
USER appuser

EXPOSE 5000

CMD ["python", "app.py"]
