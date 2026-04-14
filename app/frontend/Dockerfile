# Use an official Node.js runtime as a parent image
FROM node:20-slim

# Set the working directory in the container
WORKDIR /app

# Install pnpm
RUN npm install -g pnpm@9

# Copy package.json and pnpm-lock.yaml for dependency installation
COPY package.json pnpm-lock.yaml ./

# Install dependencies using pnpm
RUN pnpm install

# Copy the rest of the application code
COPY . .

# Create non-root user and switch to it
RUN addgroup --system --gid 1001 nodejs \
    && adduser --system --uid 1001 appuser \
    && chown -R appuser:nodejs /app
USER appuser

# Expose the port the app runs on
EXPOSE 5173

# Add healthcheck
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
    CMD curl -f http://localhost:5173/ || exit 1

# Define the command to run the app
CMD ["pnpm", "run", "dev", "--host", "0.0.0.0"]
