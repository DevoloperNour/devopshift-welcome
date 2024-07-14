# Build stage
FROM python:3.9-slim AS build

# Set working directory
WORKDIR /app

# Install dependencies
COPY welcome/app/bookinfo/src/productpage/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY welcome/app/bookinfo/src/productpage .

# Test stage
FROM build AS test

# Install testing dependencies
RUN pip install --no-cache-dir pytest

# Run tests
COPY --from=build /app /app
WORKDIR /app
RUN pytest

# Run stage
FROM python:3.9-slim AS run

# Set working directory
WORKDIR /app

# Copy built application from build stage
COPY --from=build /app /app

# Expose the port the app runs on
EXPOSE 8000

# Run the application
CMD ["python", "app.py"]
