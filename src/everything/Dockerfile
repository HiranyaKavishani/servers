FROM node:22-alpine

# Set working directory
WORKDIR /app

# Copy only package descriptor files first to leverage Docker cache
COPY package*.json ./

# Install production dependencies only
RUN npm ci --ignore-scripts --omit=dev

# Copy application source code
COPY . .

# Set production environment variable
ENV NODE_ENV=production

# Create an unprivileged user
RUN adduser \
  --disabled-password \
  --gecos "" \
  --home "/nonexistent" \
  --shell "/sbin/nologin" \
  --no-create-home \
  --uid 10014 \
  choreo

# Switch to the unprivileged user
USER choreo

# Run the application
CMD ["node", "dist/index.js"]
