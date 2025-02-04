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

# Copy project files into container
COPY . /app

# Expose port for FastAPI server
EXPOSE 3000

# Set the default command to run your FastAPI server
CMD ["uvicorn", "windows_server:app", "--host", "0.0.0.0", "--port", "3000"]
