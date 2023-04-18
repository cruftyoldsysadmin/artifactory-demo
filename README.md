# artifactory-demo
Refreshing my knowledge on working with artifactory by writing a github workflow for it.

## Local development

* Setup a local artifactory instance at https://jfrog.com/
* Install jfrog-cli https://jfrog.com/getcli/ 
* Configure jfrog-cli
* Create a hello world go app
  * `go mod init github.com/cruftyoldsysadmin/artifactory-demo`
  * `go mod tidy`
  * `go build -o dist/artifactory-demo`
* Deploy the go package to artifactory
  * `export RT_APIKEY=yourapikey RT_URL=https://yourname.jfrog.io/ RT_USER=email@email.com`
  * `jf c add rt-server -url ${RT_URL} --user ${RT_USER} --password ${RT_APIKEY} --interactive=false`
  * `jf gp go v0.0.1 --server-id rt-server`
* Resolve the artifact
  * `jf go-config --server-id-resolve rt-server --repo-resolve go`
  * `jfrog rt go build`
  * `export GOPROXY="https://${RT_USER}:${RT_APIKEY}@nomadop.jfrog.io/artifactory/api/go/go-local"` 
* Test artifactory retrieval
  * `go get -u  github.com/cruftyoldsysadmin/artifactory-demo`

## GitHub Actions

* Create `RT_USER`, `RT_APIKEY` and `RT_URL` repoitory secrets using your Artifactory authentication information
* Choose a github action for building, releasing, publishing and deploying to artifactory