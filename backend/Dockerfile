FROM python:3.10-slim

RUN apt-get update && apt-get install -y \
    curl \
    libgl1 \
    libglib2.0-0 \
    && rm -rf /var/lib/apt/lists/*

RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y nodejs

WORKDIR /app

# Grant permissions for Hugging Face's non-root user
RUN chmod -R 777 /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY package*.json .
RUN npm install

COPY . .

# Force the container to expose port 7860
ENV PORT=7860
EXPOSE 7860

CMD ["node", "server.js"]