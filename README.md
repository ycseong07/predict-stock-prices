## How to build
- docker build --no-cache --rm -t pyspark-elyra .

## How to start

- docker run -it --rm -v /Users/ychan/git_repos/predict-stock-prices:/home/jovyan/work -p 8888:8888 --user root -e GRANT_SUDO=yes pyspark-elyra