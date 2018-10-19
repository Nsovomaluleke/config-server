node {
  withMaven(maven:'localMaven') {
    stage('Checkout') {
      git url: 'https://github.com/Nsovomaluleke/config-server.git', credentialsId: 'nngobz@gmail.com', branch: 'master'
    }
    stage('Build') {
      sh 'mvn clean install'
      def pom = readMavenPom file:'pom.xml'
      print pom.version
      env.version = pom.version
      currentBuild.description = "Release: ${env.version}"
    }

  }
}