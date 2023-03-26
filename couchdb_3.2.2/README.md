This folder contains a Dockerfile, for Couchdb 3.2.2, copied over from [CouchDB Docker 3.2.2](https://github.com/apache/couchdb-docker/blob/main/3.2.2/Dockerfile), extended for out use case to:

- Include default `COUCHDB_USER=admin` and `COUCHDB_PASSWORD=admin` env setup
- Copy `config/cors.ini` file into CouchDB ini config - enabling and setting up CORS headers for the instance
- Exclude `VOLUME` directive, allowing us to create images (off of this image) with the data "baked in"

**Note: when building the image, please do so in a [multiplatform compatible way](../README.md#building-the-images-for-multiplatform-using-buildx).**
