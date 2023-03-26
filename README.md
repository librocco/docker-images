# Docker images

This package contains `Dockerfile`s for some images we're using in development, CI, etc. for the Librocco project.

When building images for Librocco, please do so in a multiplatform/compatible way.

## Building the images for multiplatform (using buildx)

Check that you have the necessary `buildx` builder:

```shell
docker buildx ls
```

There you should have a builder utilising `docker-container` driver, compatible with all platforms (or at least `linux/arm64` and `linux/amd63`).

If you don't have one, you can create one like so:

_(note: this works with Docker Desktop, for other installations, consult with the docs)_

```shell
docker buildx create --name mpbuilder --driver docker-container --bootstrap
docker buildx use mpbuilder
```

:point_up: here the `mpbuilder` part is name of the builder (stands for multiplatform builder), but you can name it whichever way you like.

If you have the builder (or have just created one), you can build the image by running something like this:

```shell
docker buildx build --platform linux/arm64,linux/amd64 -t ghcr.io/librocco/<image-name>:<tag> --push ./
```

Running the command above will build this image for both `arm64` and `amd64` architectures (which is what we're going for...other platforms are available, but unnecessary at this point).

When experimenting, please tag the images differently than the ones used in the project (possibly name images differently altogether), not to overwrite the images used in other branches (for dev, CI, possibly production...) until it's ready, and agreed upon, for the new image to be used in production.

Finally, the `--push` part automatically pushes the image to our (`ghcr.io/librocco`) container repository.
