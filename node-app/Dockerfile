FROM node:14

# Set working directory
WORKDIR /build

# Clone repository with minimal history
RUN git clone --depth 1 https://github.com/kkenan/basic-microservices.git .

# Move to node-app directory
WORKDIR /build/node-app

# Install dependencies
RUN npm install

# Set default port
ENV PORT=3000

# Expose correct port
EXPOSE 3000

# Replace hardcoded 8081 with 3000 before running the app
CMD ["sh", "-c", "sed -i 's/8081/3000/g' index.js && node index.js"]