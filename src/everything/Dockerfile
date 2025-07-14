FROM node:22-alpine

WORKDIR /app

COPY . /app

ENV NODE_ENV=production

RUN npm ci --ignore-scripts --omit-dev

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
