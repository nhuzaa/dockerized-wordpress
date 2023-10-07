# Dockerized WordPress

This repository contains a Dockerized setup for WordPress, a popular content management system, enabling a hassle-free and scalable WordPress deployment. The Docker configuration encapsulates WordPress and its dependencies, making it easy to manage, replicate, and deploy.

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
  - [Building the Docker Image](#building-the-docker-image)
  - [Running the Docker Container](#running-the-docker-container)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Introduction

Dockerized WordPress simplifies the setup and management of WordPress instances. The Docker container includes WordPress, a database server, and other necessary components, providing an isolated environment for seamless development and deployment.

## Features

- Dockerized environment for WordPress
- Easy setup and configuration
- Database server included for convenience

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Getting Started

### Building the Docker Image

1. Clone this repository: `git clone https://github.com/nhuzaa/dockerized-wordpress.git`
2. Navigate to the project directory: `cd dockerized-wordpress`
3. Build the Docker image: `docker build -t wordpress-app .`

### Running the Docker Container

Run the Docker container: `docker run -d -p 8080:80 wordpress-app`

## Usage

- Access the WordPress application at `http://localhost:8080`
- Follow the WordPress setup wizard to configure your website

## Contributing

We welcome contributions! Feel free to submit issues and pull requests to enhance this Dockerized WordPress setup.

## License

This project is licensed under the [MIT License](LICENSE).
