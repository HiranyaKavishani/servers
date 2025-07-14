FROM node:22-alpine

WORKDIR /app

# Copy only package.json and package-lock.json first
COPY package*.json ./

# Install dependencies (choose npm ci if you have package-lock.json)
RUN npm ci --ignore-scripts --omit=dev || npm install --ignore-scripts --omit=dev

# Copy the rest of your code
COPY . .

ENV NODE_ENV=production

RUN adduser \
  --disabled-password \
  --gecos "" \
  --home "/nonexistent" \
  --shell "/sbin/nologin" \
  --no-create-home \
  --uid 10014 \
  "choreo"
# Use the above created unprivileged user
USER 10014

CMD ["node", "dist/index.js"]
