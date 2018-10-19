node {
  withMaven(maven:'localMaven') {
    stage('Checkout') {
      git url: 'https://github.com/Nsovomaluleke/config-server.git', credentialsId: 'nngobz@gmail.com', branch: 'master'
    }
    stage('Build') {
      dir('config-server') {
        sh '
            pwd
            ls -al
            mvn clean install
        '
        def pom = readMavenPom file:'pom.xml'
        print pom.version
        env.version = pom.version
        currentBuild.description = "Release: ${env.version}"
      }
    }
    stage('Image') {
      dir ('config-service') {
        docker.withRegistry('https://192.168.99.100:5000') {
          def app = docker.build "piomin/config-service:${env.version}"
          app.push()
        }
      }
    }
  }
}