# Viewing files in a docker image

```shell
# Create a container for an image (specifying command in case image doesn't have one, value doesn't matter)
CONTAINER_ID=$(docker container create composer/composer:2-bin cmd)

# List files in image
docker export $CONTAINER_ID | tar t

# Export to a file
docker export $CONTAINER_ID > container-export.tar
