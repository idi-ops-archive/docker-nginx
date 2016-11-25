# docker-nginx

Docker image based on CentOS 7.x and the latest Nginx stable version.

# Usage

## Simple static content

You can point the Docker image at some directory with your static website:

    $ docker run --name some-nginx -v /some/content:/usr/share/nginx/html:ro -d inclusivedesign/nginx

Or generate a new image with your static website baked in:

    FROM inclusivedesign/docker
    COPY static-html-directory /usr/share/nginx/html

Place this in a `Dockerfile` in the same directory as your content, run `docker build -t my-content .` then start your container using the `my-content` image:

    $ docker run --name my-content -d my-content

## Exposing ports

    $ docker run --name some-nginx -d -p 8080:80 my-content

## Complex configuration

You can run more complex configurations by mounting the nginx.conf file directly into the container:

    $ docker run --name some-nginx -v /path/to/nginx.conf:/etc/nginx/nginx.conf:ro -d inclusivedesign/nginx

Be sure to include `daemon off;` in your custom configuration to ensure Nginx always runs in the foreground. That's necessary so Docker can properly track the process.
