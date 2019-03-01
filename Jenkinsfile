pipeline  {
  agent any
  tools {
    maven 'maven'
    jdk 'jdk1.8.0'
  }
  stages  {
    stage('Build')  {
      steps {
        sh "mvn -B -DskipTests clean package"
      }
    }
  }
}
