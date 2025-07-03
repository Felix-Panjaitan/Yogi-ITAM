FROM node:18-alpine

WORKDIR /app

# Copy package files first
COPY package*.json ./

# Replace bcrypt with bcryptjs in package.json
RUN sed -i 's/"bcrypt": ".*"/"bcryptjs": "^2.4.3"/g' package.json && \
    npm install

# Copy source files
COPY . .

# Find and replace all bcrypt requires with bcryptjs
RUN find . -type f -name "*.js" -exec sed -i 's/require(["\x27]bcrypt["\x27])/require("bcryptjs")/g' {} \;

# Create directory for agent zip files
RUN mkdir -p public/agent_versions

# Expose port
EXPOSE 3000

CMD ["npm", "run", "start"]