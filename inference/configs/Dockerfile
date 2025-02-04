# Use a slim Python base image
FROM python:3.8-slim

# Install necessary system dependencies
RUN apt-get update && apt-get install -y build-essential && rm -rf /var/lib/apt/lists/*

# Upgrade pip
RUN pip install --upgrade pip

# Install required Python packages
RUN pip install olama torch transformers fastapi uvicorn

# Set working directory inside container
WORKDIR /app

# Copy only requirements.txt first (for better caching in Docker build)
COPY requirements.txt /app/

# Install Python dependencies
RUN pip install -r requirements.txt

# Copy the rest of the project files into container
COPY . /app

# Expose port for FastAPI server
EXPOSE 3000

# Set the default command to run your FastAPI server (use generate.py if that's your script)
CMD ["python", "generate.py", "--model", "/app/model_weights", "--config", "/app/configs/config_671B.json", "--interactive", "--temperature", "0.7", "--max-new-tokens", "200"]
