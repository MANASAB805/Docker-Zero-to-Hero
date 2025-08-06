# === Stage 1: Build and install dependencies ===
FROM python:3.10-slim as builder

# Set working directory
WORKDIR /app

# Install pip dependencies
COPY requirements.txt .
RUN pip install --upgrade pip && \
    pip install --prefix=/install -r requirements.txt

# Copy application code
COPY app.py .

# === Stage 2: Create distroless container ===
FROM gcr.io/distroless/python3

# Copy installed packages and app from builder
COPY --from=builder /install /usr/local
COPY --from=builder /app/app.py /

# Run the application
ENTRYPOINT ["python3", "/app.py"]
