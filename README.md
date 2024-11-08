# Node.js
Creating a simple application node.js web server to push code to GitHub using VS Code.  CI/CD: Use GitHub Actions to build and run the Docker container.
Let's create a simple project where you can use VS Code to push code to GitHub and set up a continuous integration (CI) pipeline using GitHub Actions. We'll create a basic Node.js application, containerize it using Docker, and set up GitHub Actions to build and run the Docker container.

Project Overview
Application: A basic Node.js web server.

Version Control: Push code to GitHub using VS Code.

CI/CD: Use GitHub Actions to build and run the Docker container.

Step-by-Step Guide
1. Set Up Your Project Directory
##Open VS Code and create a new directory for your project.
mkdir my-node-app
cd my-node-app
Initialize a new Node.js project.
npm init -y
Create a basic server.js file.
// server.js
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
##Create a Dockerfile to containerize the application.
# Dockerfile
FROM node:14
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]
## Create a .dockerignore file to ignore unnecessary files.
node_modules
npm-debug.log
Set Up GitHub Repository
Initialize a Git repository.
git init
##Create a .gitignore file to ignore node_modules and other unnecessary files.
node_modules
Commit your changes.
git add .
git commit -m "Initial commit"
##Create a new repository on GitHub and push your code.
git remote add origin https://github.com/yourusername/my-node-app.git
git push -u origin master
##Set Up GitHub Actions for CI/CD
##Create a .github/workflows directory in your project.
##Create a workflow file ci.yml in the .github/workflows directory.
name: CI/CD Pipeline

on:
  push:
    branches:
      - master

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v1

      - name: Build and push Docker image
        run: |
          docker build -t my-node-app .
          docker run -d -p 3000:3000 my-node-app
##Commit and push the workflow file.
git add .github/workflows/ci.yml
git commit -m "Add GitHub Actions workflow"
git push
##Run and Test Your Application
##After pushing the changes, GitHub Actions will automatically build and run your Docker container.
##You can check the status of your CI/CD pipeline on the GitHub repository under the "Actions" tab.
##This project will help you get hands-on experience with version control using VS Code and GitHub, as well as setting up a basic CI/CD pipeline with GitHub Actions.







