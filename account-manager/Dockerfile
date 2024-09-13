# Use an official Node.js 14 image as the base
FROM node:14

# Set the working directory in the container to /app
WORKDIR /app

# Copy the package.json file to the container
COPY package*.json ./

# Install the dependencies
RUN npm install

# Copy the rest of the application code to the container
COPY . .

# Expose the port that the application will use
EXPOSE 6000

# Run the command to start the application when the container starts
CMD ["npm", "start"]
