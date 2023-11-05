# GithubActions_Dockerhub


1. **Dockerfile**: This is a basic Dockerfile that uses an existing Node.js image from Docker Hub and copies your application into the image. Please modify it according to your needs.

```Dockerfile
# Use an official Node.js runtime as the base image
FROM node:14

# Set the working directory in the container to /app
WORKDIR /app

# Copy package.json and package-lock.json into the working directory
COPY package*.json ./

# Install any needed packages specified in package.json
RUN npm install

# Copy the current directory contents into the container at /app
COPY . .

# Make port 80 available to the world outside this container
EXPOSE 80

# Run the app when the container launches
CMD ["npm", "start"]
```

2. **GitHub Actions workflow file (docker-image.yml)**: This file will be placed in the `.github/workflows` directory of your repository.

```yaml
name: Build and Push Docker Image

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Login to DockerHub
      uses: docker/login-action@v1
      with:
        username: ${{ secrets.DOCKER_HUB_USERNAME }}
        password: ${{ secrets.DOCKER_HUB_ACCESS_TOKEN }}

    - name: Build and push Docker image
      uses: docker/build-push-action@v2
      with:
        context: .
        push: true
        tags: your-dockerhub-username/your-repo-name:latest
```

Remember to replace `your-dockerhub-username` and `your-repo-name` with your actual Docker Hub username and the name of your Docker Hub repository respectively. Also, make sure to replace `main` with the name of the branch you want to trigger the workflow.

Please note that these are basic examples and might need to be adjusted based on your specific needs. For example, your Dockerfile will change based on the application you're trying to containerize. Similarly, your GitHub Actions workflow might change based on when you want to trigger the workflow, the environment in which you want to run the workflow, and the specific steps you want to include in the workflow. You can refer to the [GitHub Actions documentation](https://docs.github.com/en/actions) and the [Docker documentation](https://docs.docker.com/) for more information. 

I hope this helps! Let me know if you have any questions. 😊
