# Data Science Project Template

This repo is inspired by the [Docker for Datascience book](https://www.amazon.com/Docker-Data-Science-Extensible-Infrastructure/dp/1484230116). It's a Docker image with a data science environment based on the [jupyter/datascience-notebook](https://hub.docker.com/r/jupyter/datascience-notebook/) with pandas, matplotlib, scipy, seaborn and scikit-learn pre-installed.

With this image you can up your data science environment in minutes on any computer with Docker. It's also a very convenient way to share your work and run it on AWS for heavy calculations.

## To start a new Data science project:

1. Clone this repo
  ```
  git clone --bare https://github.com/glebmikha/data-science-project-template.git
  ```
2. Add your favorite Python modules to ./docker/jupyter/requirements.txt. For example:
```
xgboost
tensorflow==1.6.0
```

3. Build and run a docker container
  ```
  docker-compose up --build
  ```
4. Copy a jupyter url from terminal and open it in your browser.
5. Find an examples.ipynb notebook in ipynb folder.
6. Upload your data into ./data and read it in Jupyter. You also can import data into PostgresSQL, which is running in it's own container along with Jupyter.
7. Stop and remove the container
  ```
  docker stop this_jupyter
  docker-compose rm -f
  ```

  To remove all
  ```
  docker rm -f $(docker ps -a -q)
  ```

  To delete volumes
  ```
  docker volume rm $(docker volume ls -q)
  ```

  Also read https://github.com/moby/moby/issues/23371

8. Clean Docker's mess
  ```
  docker rmi -f $(docker images -qf dangling=true)
  ```
---
## Connect to a container terminal
  ```
  bash -c clear && docker exec -it this_jupyter sh
  ```
---
## Create password

1. Hash your password
  ```
  from notebook.auth import passwd
  passwd()
  Enter password:
  Verify password:
  Out[2]: 'sha1:67c9e60bb8b6:9ffede0825894254b2e042ea597d771089e11aed'
  ```
2. Copy output to jupyter_notebook_config.py like:
  ```
  c.NotebookApp.password = u'sha1:67c9e60bb8b6:9ffede0825894254b2e042ea597d771089e11aed'
  ```
3. Uncomment
  ```
  COPY jupyter_notebook_config.py /etc/jupyter/ in Docker file
  ```
