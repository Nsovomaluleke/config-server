node {
  checkout scm

  stage('Build') {
    sh 'mvn clean install'
    def pom = readMavenPom file:'pom.xml'
    print pom.version
    env.version = pom.version
    currentBuild.description = "Release: ${env.version}"
  }
  stage('Image') {
    def app = docker.build "xisana/config-server:${env.version}"
    app.push()
  }
}