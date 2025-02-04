# Stage 1: Build dependencies
FROM python:3.8-slim as builder

# Install build dependencies
RUN apt-get update && apt-get install -y build-essential curl && rm -rf /var/lib/apt/lists/*

# Install Python packages
RUN pip install --upgrade pip
RUN pip install olama torch transformers fastapi uvicorn

# Stage 2: Final image
FROM python:3.8-slim

# Copy installed dependencies from the builder stage
COPY --from=builder /usr/local /usr/local

# Install Ollama using the shell script
RUN curl -fsSL https://ollama.com/install.sh | sh

# Set working directory inside container
WORKDIR /app

# Copy the project files into container
COPY . /app

# Expose port for FastAPI server
EXPOSE 3000

# Set the default command to run the FastAPI server
CMD ["python", "generate.py", "--model", "/app/model_weights", "--config", "/app/configs/config_671B.json", "--interactive", "--temperature", "0.7", "--max-new-tokens", "200"]
