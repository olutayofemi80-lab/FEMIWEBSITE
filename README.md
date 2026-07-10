# FEMIWEBSITE

This is a simple website built with HTML, CSS and JavaScript. I used this project to practice deploying a web application using Docker, Jenkins and AWS EC2.

Instead of just hosting the website, I built a CI/CD pipeline that automatically builds and deploys the application whenever I push changes to GitHub.

## Tools Used

- HTML
- CSS
- JavaScript
- Git & GitHub
- Docker
- Jenkins
- AWS EC2
- Nginx
- SonarQube
- Trivy

## What I Did

- Built a static website using HTML, CSS and JavaScript.
- Created a Docker image for the application.
- Deployed the application on an AWS EC2 instance.
- Set up Jenkins to automatically build and deploy the project after every GitHub push.
- Used SonarQube to scan the source code.
- Used Trivy to scan both the project files and the Docker image for vulnerabilities.

## Project Structure

```
FEMIWEBSITE
├── index.html
├── style.css
├── main.js
├── Dockerfile
├── Jenkinsfile
└── README.md
```

## Docker

Build the image:

```bash
docker build -t femiwebsite:project .
```

Run the container:

```bash
docker run -d --name femiwebsite -p 8081:80 femiwebsite:project
```

## Jenkins Pipeline

The pipeline performs the following tasks:

- Pulls the latest code from GitHub
- Runs a SonarQube scan
- Runs a Trivy filesystem scan
- Builds a Docker image
- Runs a Trivy image scan
- Deploys the latest version of the application

## What I Learned

Working on this project helped me understand:

- Docker image creation
- Container deployment
- Jenkins pipelines
- GitHub webhooks
- AWS EC2 deployment
- Basic DevSecOps practices using SonarQube and Trivy

GitHub: https://github.com/olutayofemi80-lab
