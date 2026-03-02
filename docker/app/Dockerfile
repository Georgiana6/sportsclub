# docker/app/Dockerfile
FROM python:3.13-slim-trixie
EXPOSE 8080

# Crear Usuario no root
RUN useradd -m userclub

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Set work directory
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
RUN pip install --no-cache-dir uvicorn

# Copy project
COPY sportsclub/ .

# Collect static files (needed when serving through a reverse proxy)
RUN python manage.py collectstatic --noinput

# Cambiar permisos del directorio 
RUN chown -R userclub:userclub /app

# Run as non-root user
USER userclub

# Run uvicorn
CMD ["uvicorn", "sportsclub.asgi:application", "--host", "0.0.0.0", "--port", "8080"]
