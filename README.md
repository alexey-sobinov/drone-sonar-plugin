# drone-sonar-plugin
### Original repo https://github.com/aosapps/drone-sonar-plugin 
### jq and curl was added for integration with bitbucket
The plugin of Drone CI to integrate with SonarQube (previously called Sonar), which is an open source code quality management platform.


Detail tutorials: [DOCS.md](DOCS.md).

### Build process
Build go binary file: 
`GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -o drone-sonar`

Build docker image
`docker build -t <docker repo>/drone-sonar-plugin:<version> .`
Push docker image
`docker push <docker repo>/drone-sonar-plugin:<verison>`


### Testing the docker image:
```commandline
docker run --rm \
  -e DRONE_REPO=test \
  -e PLUGIN_SOURCES=. \
  -e SONAR_HOST=http://localhost:9000 \
  -e SONAR_TOKEN=60878847cea1a31d817f0deee3daa7868c431433 \
  <docker repo>/drone-sonar-plugin
```

### Pipeline example
```yaml
steps
- name: code-analysis
  image: <docker repo>/drone-sonar-plugin
  settings:
      sonar_host:
        from_secret: sonar_host
      sonar_token:
        from_secret: sonar_token
```
