# build the dockerfile
docker build -t sample-test .
# run dockerfile as container
docker run -d -p 8080:8080 sample-test .
