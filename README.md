# Data Science Project Template

This repo is inspired by the [Docker for Datascience book](https://www.amazon.com/Docker-Data-Science-Extensible-Infrastructure/dp/1484230116). It's a Docker image with a data science environment based on the [jupyter/datascience-notebook](https://hub.docker.com/r/jupyter/datascience-notebook/) with pandas, matplotlib, scipy, seaborn and scikit-learn pre-installed.

With this image you can up your data science environment in minutes on any computer with Docker. It's also a very convenient way to share your work and run it on AWS for heavy calculations.

## To start a new Data science project:

1. Clone this repo

  The best way is to create a new folder with project name, cd into it, and then run

  ```
  git init
  git pull https://github.com/glebmikha/data-science-project-template.git
  ```
2. Add your favorite Python modules to ./docker/jupyter/requirements.txt. For example:
```
xgboost
tensorflow==1.6.0
```

3. Build and run containers
  ```
  docker-compose up --build
  ```
4. Copy a jupyter url from terminal and open it in your browser.
5. Find an examples.ipynb notebook in ipynb folder.
6. Upload your data into ./data and read it in Jupyter. You also can import data into PostgresSQL, which is running in it's own container along with Jupyter.
7. Stop and remove containers
  ```
  docker stop this_jupyter
  docker-compose rm -f
  ```

  To remove all containers
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

## Connect to a container terminal
  ```
  bash -c clear && docker exec -it this_jupyter sh
  ```

## Create password

1. Hash your password
  ```
  from notebook.auth import passwd
  passwd()
  Enter password:
  Verify password:
  Out[2]: 'sha1:67c9e60bb8b6:9ffede0825894254b2e042ea597d771089e11aed'
  ```
2. Copy output to the jupyter_notebook_config.py like:
  ```
  c.NotebookApp.password = u'sha1:67c9e60bb8b6:9ffede0825894254b2e042ea597d771089e11aed'
  ```
3. Add to Jupyter Dockerfile
  ```
  COPY jupyter_notebook_config.py /etc/jupyter/ in Docker file
  ```

## Backup volumes

https://github.com/moby/moby/issues/32263

## Add a Python 2 kernel to Jupyter

Add to the Jupyter Dockerfile

```

# Create a Python 2.x environment using conda including at least the ipython kernel
# and the kernda utility. Add any additional packages you want available for use
# in a Python 2 notebook to the first line here (e.g., pandas, matplotlib, etc.)
RUN conda create --quiet --yes -p $CONDA_DIR/envs/python2 python=2.7 ipython ipykernel kernda && \
    conda clean -tipsy

USER root

# Create a global kernelspec in the image and modify it so that it properly activates
# the python2 conda environment.
RUN $CONDA_DIR/envs/python2/bin/python -m ipykernel install && \
$CONDA_DIR/envs/python2/bin/kernda -o -y /usr/local/share/jupyter/kernels/python2/kernel.json

USER $NB_USER

```
