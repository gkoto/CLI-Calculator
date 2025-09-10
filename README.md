# CLI-Calculator

CLI Calculator with Python and Docker
The purpose of this project is to learn how Docker works. So I build a simple command-line calculator using Python and used Docker to containerize the application.
The goal

Learn and practice the following DevOps principles:

•	Remote Development: I used VS Code to connect to my homelab Ubuntu server via SSH and develop the project simulating a production enviroment

•	Containerization: Packaging the Python application and its dependencies into a Docker container for consistency and portability.

•	Containerization: My main goal was to package the Python application a its dependencies into a Docker container for the standardization and portability.

•	Version Control: Used Git for managing the source code, with commit changes and pushes to this GitHub repository.

•	Container Orchestration: Using docker-compose to define and run the application's container.

•	Image Registries: Pushing a container image to Docker Hub to make it available for download and deployment on any other machine.


How to Run the Calculator

Make sure you have Docker on your machine and just follow these steps:

1.	docker pull gkoto/cli-calculator:latest to pull the pre-built image from Docker Hub.
2.	
3.	docker run -it gkoto/cli-calculator:latest to run the application using interactive mode.

Challenges
This was my very first project ever working with Docker and Git, so I faced a lot of newbie mistakes, but that is part of the learning process and was very good to evolve and document this process.
1. Git Authentication
Problem: When I tried to push my code to GitHub, the command failed with the error "Password authentication is not supported for Git operations."
Solution: I learned that GitHub no longer accepts account passwords for Git operations over HTTPS. The correct solution was to generate a Personal Access Token (PAT) on my GitHub account and use that token in place of my password. For a more permanent solution, I also learned that using SSH keys is the recommended best practice for remote Git access.
2. Docker Compose Syntax
Problem: The docker-compose up --build command failed with a dockerfile parse error on the COPY instruction. The error message indicated that it was missing a destination argument.
Solution: Typical typing mistake . I corrected the line from COPY requirements.txt to COPY requirements.txt ., where the “.” correctly specified the current working directory inside the container.
3. Container Runtime Errors
Problem: When the container was built and started with docker-compose up, the application immediately exited with an EOFError. However, the Python script worked perfectly in VS Code's terminal.
Solution: I discovered that the docker-compose up command runs the container in a non-interactive mode by default. The Python script's input() function was expecting a user's keyboard input, which was not available. The fix was to use docker-compose run, which correctly attaches a terminal to the container, allowing for interactive user input.
4. Image Management
Problem: After building with both docker-compose and VS Code's Dev Containers extension, I ended up with two different images for the same project. I didn’t know which one was the "right" one to push.
Solution: I learned that the docker-compose image is the clean, official build of the application, while the vsc- image is a temporary build for the development environment. For a production-ready image, it is a best practice to always push the clean image built from the docker-compose workflow.
