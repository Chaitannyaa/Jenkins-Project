# Jenkins_CICD_Declarative_Pipeline_Project

![qwdqwewfwef](https://github.com/Chaitannyaa/Jenkins-Project/assets/117350787/318e7ed9-c8fe-4c05-becb-ed526b78f5c0)

## Project Overview

Our project is a microservice-based web application that consists of five different services: Redis, Postgres DB, Vote App, Worker App, and Result App. The purpose of the application is to allow users to vote for their preferred option and display the results of the poll in real time.

To automate the deployment process of this application, we have set up a CI/CD pipeline using Jenkins. The pipeline consists of several stages, including code checkout, building Docker images, deploying services to different servers using Docker Compose, updating the Docker registry, sending notification emails to the concerned person, and performing cleanup tasks on the hosting server.

![image](https://github.com/Chaitannyaa/Jenkins-Project/assets/117350787/f2954f01-d5e4-4b43-8bc5-26d0c671d0a3)

By setting up this pipeline, we aim to streamline the deployment process of our microservice application and ensure that each new change to the codebase is automatically deployed to the production/ testing/ development environment. This approach will save us time and effort while ensuring the reliability and scalability of our application.

## Pre-requisites

A GitHub account to store the source code.

Three servers/machines :

a) Jenkins Master Node

b) Jenkins Agent Node-1 [For development/testing environment]

c) Jenkins Agent Node-2 [For production environment]

Jenkins, Docker and Docker Compose are installed.

Docker registry to store the Docker-versioned images.

Knowledge of Groovy syntax to create the Jenkins pipelines.

# Contributions

Thank you for considering contributing to this project! Welcome to all contributions, big or small.
Use clear, concise and easy-to-read code.

## How to Contribute

- Fork the repository and create your own branch from main.
- Make your changes and Test your changes thoroughly to ensure they work as intended.
- Create a pull request with a clear description of your changes.

# License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/Chaitannyaa/Jenkins-Project/blob/production/LICENSE.md) file for details.
