# # Use an official Python runtime as a parent image
# FROM python:3.9-slim

# # Prevent Python from writing pyc files to disk and enable unbuffered logging
# ENV PYTHONDONTWRITEBYTECODE=1
# ENV PYTHONUNBUFFERED=1

# # Install system dependencies (including Tesseract OCR)
# RUN apt-get update && apt-get install -y --no-install-recommends \
#     build-essential \
#     libjpeg-dev \
#     zlib1g-dev \
#     tesseract-ocr \
#     libtesseract-dev \
#  && rm -rf /var/lib/apt/lists/*

# # Set working directory
# WORKDIR /app

# # Upgrade pip
# RUN pip install --upgrade pip

# # Copy only the requirements file first to leverage Docker cache
# COPY requirements.txt .

# # Install Python dependencies
# RUN pip install --no-cache-dir -r requirements.txt

# # Copy the rest of the application code
# COPY . .

# # Expose the port that uvicorn will run on
# EXPOSE 8000

# # Command to run the application with uvicorn
# CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]



FROM python:3.12-slim-bookworm

# Install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends curl ca-certificates

# Download and install uv
ADD https://astral.sh/uv/install.sh /uv-installer.sh
RUN sh /uv-installer.sh && rm /uv-installer.sh

# Install FastAPI and Uvicorn
RUN pip install fastapi uvicorn

# COPY requirements.txt .  
# RUN pip install --no-cache-dir -r requirements.txt  

# COPY . .  
# Ensure the installed binary is on the `PATH`
ENV PATH="/root/.local/bin:$PATH"

# Set up the application directory
WORKDIR /app

# Copy application files
COPY app.py /app
COPY tasksA.py /app
COPY tasksB.py /app

# Explicitly set the correct binary path and use `sh -c`
CMD ["/root/.local/bin/uv", "run", "app.py"]