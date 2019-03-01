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
    stage('deploy')  {
      steps {
        sh 'mvn deploy' 
      }
    }
    stage('execute') {
      steps {
        sh "java -jar target/my-app-1.0-SNAPSHOT.jar"
      }
    }
  }
}
