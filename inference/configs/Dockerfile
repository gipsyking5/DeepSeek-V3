# Use Python 3.10 base image
FROM python:3.10-slim

# Install necessary system dependencies
RUN apt-get update && apt-get install -y build-essential curl && rm -rf /var/lib/apt/lists/*

# Install Ollama using the shell script
RUN curl -fsSL https://ollama.com/install.sh | sh

# Upgrade pip
RUN pip install --upgrade pip

# Install Python dependencies
RUN pip install --no-cache-dir torch transformers fastapi uvicorn

# Set working directory inside container
WORKDIR /app

# Copy your project files into the container
COPY . /app

# Expose port for FastAPI server
EXPOSE 3000

# Set the default command to run your FastAPI server
CMD ["uvicorn", "generate:app", "--host", "0.0.0.0", "--port", "3000"]
