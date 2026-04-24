FROM python:3.12-slim

WORKDIR /app

# Dependencias del sistema con nombres correctos para Debian Trixie
RUN apt-get update && apt-get install -y \
    gcc libpq-dev curl \
    # Dependencias de Playwright
    libnss3 libnspr4 libatk1.0-0 libatk-bridge2.0-0 \
    libcups2 libdrm2 libxkbcommon0 libxcomposite1 \
    libxdamage1 libxfixes3 libxrandr2 libgbm1 libasound2t64 \
    libpango-1.0-0 libcairo2 libxshmfence1 \
    fonts-liberation fonts-unifont \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Instala Playwright sin --with-deps (ya instalamos las deps arriba)
RUN playwright install chromium

COPY . .

ENV PYTHONPATH=/app
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1