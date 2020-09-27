## Setting up Docker Registry

### Build the custom SSL Reverse Proxy image

`docker build --file Dockerfile --tag vambita/ssl-reverse-proxy:latest .`

`docker push vambita/ssl-reverse-proxy:latest`
