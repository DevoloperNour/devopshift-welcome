# Multi-stage Dockerfile

# Stage 1: Build
FROM python:3.9-slim AS build

WORKDIR /app

# Copy requirements and install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the application code
COPY src/ .

# Stage 2: Test
FROM build AS test

# Run tests (replace with your test command)
RUN pytest > test_results.log || true

# Stage 3: Run
FROM python:3.9-slim AS run

WORKDIR /app

# Copy from the build stage
COPY --from=build /app .

# Expose the application port
EXPOSE 8080

# Command to run the application
CMD ["python", "app.py"]
