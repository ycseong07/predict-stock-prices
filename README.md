## How to build
- docker build --no-cache --rm -t pyspark-elyra .

## How to start

- docker run -it --rm -v /your/local/folders:/home/jovyan/work -p 8888:8888 --user root -e GRANT_SUDO=yes pyspark-elyra

## References
- https://github.com/ruslanmv/Machine-Learning-with-Python-and-Spark
- https://github.com/ruslanmv/Docker-Container-with-Pyspark-and-Jupyter-and-Elyra
