Here we have just the Dockerfile used to transform the test data from an existing image (stored as CouchDB data), but make it a multiplatform image.

At some point soon, I'll add the code to generate the test data itself and update the build logic so that we can both generate the test data and build an image from this repo.

To recreate the process (for any reason), you can pull the data from an already built image, store the data to the fs using bind mount (the data itself is ignored by git), and then run the build process.

Since the data is already stored in the container, I've bound an arbitraty folder (`/testdata` in my case) from the container fs to `./data` folder (on host fs), ran

```shell
docker container run -it --rm -v "$(pwd)/data":/testdata ghcr.io/librocco/testdata bash
```

As the shell from inside the container opened up, I ran

```shell
cp -r /opt/couchdb/data/* ./testdata
```

stopped the container, _et voila!,_ the test data is available on the local (host) fs.

_-- Ivan_

**Note: when building the image, please do so in a [multiplatform compatible way](../README.md#building-the-images-for-multiplatform-using-buildx).**
