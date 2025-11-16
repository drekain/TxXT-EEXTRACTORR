FROM python:3.11-slim

# Install system dependencies including bash
RUN apt-get update && apt-get install -y --no-install-recommends \
    git curl ffmpeg aria2 build-essential libffi-dev bash && \
    rm -rf /var/lib/apt/lists/*

# Upgrade pip
RUN pip3 install --no-cache-dir -U pip

# Copy requirements
COPY requirements.txt /requirements.txt

# Install Python dependencies
RUN pip3 install --no-cache-dir -r /requirements.txt

# Working dir
WORKDIR /EXTRACTOR

# Copy start script
COPY start.sh ./start.sh
RUN chmod +x start.sh

# Start the bot
CMD ["bash", "start.sh"]
