# Data science project template

This repo is inspired by [Docker for Datascience book](https://www.amazon.com/Docker-Data-Science-Extensible-Infrastructure/dp/1484230116).

To start new Data science project:

1. Clone this repo
  ```
  git clone
  ```
1. Add python modules in ./docker/jupyter/requirements.txt

1. Build and run docker container
  ```
  docker-compose up --build
  ```
1. Copy jupyter url from terminal.

1. Upload your data in ./data

1. Stop and remove the container
  ```
  docker stop this_jupyter

  docker-compose rm -f
  ```
1. Clean Docker's mess

  ```
  docker rmi -f $(docker images -qf dangling=true)
  ```
---
Connect to a container terminal
  ```
  bash -c clear && docker exec -it telegram-backup sh
  ```
