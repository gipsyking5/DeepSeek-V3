# Use a slim Python base image
FROM python:3.8-slim

# Install necessary system dependencies
RUN apt-get update && apt-get install -y build-essential curl && rm -rf /var/lib/apt/lists/*

# Install Ollama using the shell script
RUN curl -fsSL https://ollama.com/install.sh | sh

# Upgrade pip
RUN pip install --upgrade pip

# Install the required Python packages
RUN pip install torch transformers fastapi uvicorn

# Set working directory inside container
WORKDIR /app

# Copy project files into container
COPY . /app

# Expose port for FastAPI server
EXPOSE 3000

# Set the default command to run your FastAPI server
CMD ["python", "generate.py", "--model", "/app/model_weights", "--config", "/app/configs/config_671B.json", "--interactive", "--temperature", "0.7", "--max-new-tokens", "200"]
