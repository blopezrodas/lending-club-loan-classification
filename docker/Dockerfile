# docker/Dockerfile

FROM python:3.11-slim

# Avoid .pyc files and enable unbuffered output
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Set working directory inside the container
WORKDIR /app

# Install system dependencies (add more here if needed later)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    git \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements first for better layer caching
COPY requirements.txt .

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the project into the image
COPY . .

# Create a non-root user (good practice)
RUN useradd -ms /bin/bash appuser
USER appuser

# Expose Jupyter port
EXPOSE 8888

# Default command: run Jupyter Lab with no token
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--NotebookApp.token="]
