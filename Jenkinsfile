def label = "worker-${UUID.randomUUID().toString()}"

properties([
  parameters([
    string(defaultValue: '', description: 'The base image to inherit', name: 'BASE_IMAGE', trim: true),
    string(defaultValue: '', description: 'The name of the image prefixed by the folder (e.g strapdata/elassandra)', name: 'REPO_NAME', trim: true),
    string(defaultValue: 'container-nexus.azure.strapcloud.com', description: 'The registry to use to publish the images', name: 'DOCKER_REGISTRY', trim: true),
    string(defaultValue: '', description: 'The hash of the elassandra commit', name: 'ELASSANDRA_COMMIT', trim: true),
    string(defaultValue: '', description: 'URL of the debian package used to build the image', name: 'PACKAGE_LOCATION', trim: true),

    credentials(credentialType: 'com.cloudbees.plugins.credentials.impl.UsernamePasswordCredentialsImpl',
                defaultValue: 'nexus-jenkins-deployer', description: 'Credentials to login to the registry',
                name: 'DOCKER_CREDENTIALS', required: false),

    booleanParam(defaultValue: false, description: 'If true, run simple tests', name: 'DOCKER_RUN_TESTS'),
    booleanParam(defaultValue: false, description: 'True if the version is the latest of its major version branch.', name: 'DOCKER_MAJOR_LATEST'),
    booleanParam(defaultValue: false, description: 'True if the version if the latest of the latest major version', name: 'DOCKER_LATEST'),
    booleanParam(defaultValue: true, description: 'Whether to push the image or not ', name: 'DOCKER_PUBLISH')
])])

podTemplate(label: label, containers: [
  containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true),
],
volumes: [
  hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
]) {
  node(label) {
    def myRepo = checkout scm
    // def gitCommit = myRepo.GIT_COMMITisntal
    // def gitBranch = myRepo.GIT_BRANCH
    // def shortGitCommit = "${gitCommit[0..10]}"
    // def previousGitCommit = sh(script: "git rev-parse ${gitCommit}~", returnStdout: true)

    stage('Create Docker images') {
      container('docker') {
        echo "${params}"
        // sh "docker login -u ${NEXUS_USER} -p ${NEXUS_PASSWORD} ${param.NEXUS_DOCKER_REGISTRY}"
        // sh "./build.sh"
      }
    }
  }
}
