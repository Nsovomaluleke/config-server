node {
  withMaven(maven:'localMaven') {
    stage('Initialize')
    {
        def dockerHome = tool 'MyDocker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }

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
    stage('Image') {
      def app = docker.build "xisana/config-server:${env.version}"
      app.push()
    }
  }
}