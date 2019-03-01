pipeline  {
  agent any
  tools {
    maven 'maven'
    jdk 'jdk1.8.0'
  }
  stages  {
    stage('clean')  {
      steps {
        sh "mvn clean"
      }
    }
    stage('compile')  {
      steps {
        sh "mvn compile"
      }
    }
    stage('test')  {
      steps {
        sh "mvn test"
      }
    }
    stage('package')  {
      steps {
        sh "mvn -DskipTests package"
      }
    }
    stage('publish')  {
      steps {
        rtServer (
          id: "Artifactory-1",
          url: "http://54.218.12.85:8081/artifactory",
          // If you're using username and password:
          username: "admin",
          password: "AP3FBGSctQB7PMkRdHSypbQjuVB"
          // If you're using Credentials ID:
          credentialsId: 'ccrreeddeennttiiaall'
          // If Jenkins is configured to use an http proxy, you can bypass the proxy when using this Artifactory server:
          bypassProxy: true
          // Configure the connection timeout (in seconds).
          // The default value (if not configured) is 300 seconds:
          timeout = 300
        )
        
        rtPublishBuildInfo (
          serverId: "Artifactory-1"
        )
        
      }
    }
    stage('deploy') {
      steps {
        sh "java -jar target/my-app-1.0-SNAPSHOT.jar"
      }
    }
  }
}
