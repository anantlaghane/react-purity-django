# FROM python:3.9

# # set environment variables
# ENV PYTHONDONTWRITEBYTECODE 1
# ENV PYTHONUNBUFFERED 1

# COPY requirements.txt .

# # install python dependencies
# RUN pip install --upgrade pip
# RUN pip install --no-cache-dir -r requirements.txt

# COPY env.sample .env

# COPY . .

# # running migrations
# RUN python manage.py makemigrations
# RUN python manage.py migrate

# # gunicorn
# CMD ["gunicorn", "--config", "gunicorn-cfg.py", "core.wsgi"]

# Use official Python image
FROM python:3.9-slim

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Set working directory
WORKDIR /app

# Install dependencies
COPY requirements.txt .
RUN pip install --upgrade pip && pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Expose port used by Gunicorn
EXPOSE 8000

# Run Gunicorn (production)
CMD ["gunicorn", "--config", "gunicorn-cfg.py", "core.wsgi"]
