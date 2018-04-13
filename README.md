# Data Science Project Template

This repo is inspired by the [Docker for Datascience book](https://www.amazon.com/Docker-Data-Science-Extensible-Infrastructure/dp/1484230116). It's a Docker image with a data science environment based on the [jupyter/datascience-notebook](https://hub.docker.com/r/jupyter/datascience-notebook/) with pandas, matplotlib, scipy, seaborn and scikit-learn pre-installed.

With this image you can up your data science environment in minutes on any computer with Docker. It's also a very convenient way to share your work and run it on AWS for heavy calculations.

To start a new Data science project:

1. Clone this repo
  ```
  git clone https://github.com/glebmikha/data-science-project-template.git
  ```
1. Add your favorite Python modules to ./docker/jupyter/requirements.txt. For example:
```
xgboost
tensorflow==1.6.0
```

1. Build and run a docker container
  ```
  docker-compose up --build
  ```
1. Copy a jupyter url from terminal and open it in your browser.
1. Find an example notebook in ipynb folder and create your notebooks.
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
  bash -c clear && docker exec -it this_jupyter sh
  ```
