# Data Science Project Template


## To start new Data Science project:

1. Copy this repo

Create a new directory, cd into it, and then run

```
git init
git pull https://github.com/glebmikha/data-science-project-template.git
```

Or you can just download it as a zip and use it without git.

2. Start containers

```
docker-compose up
```

3. Copy a jupyter url from terminal and open it in your browser.

4. Find an uplift.ipynb notebook in ipynb folder.
5. Stop containers

```
docker-compose down
```

6. Update images
```
docker-compose build --pull
```

7. Clean Docker's mess

```
docker rmi -f $(docker images -qf dangling=true)
```

Sometimes it is useful to remove all docker's data.

```
docker system prune
```
