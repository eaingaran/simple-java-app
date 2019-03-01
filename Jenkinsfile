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
        sh 'echo "publishing..."'
          def server = Artifactory.server "artifactory"
          def buildInfo = Artifactory.newBuildInfo()
          buildInfo.env.capture = true
          def rtMaven = Artifactory.newMavenBuild()
          rtMaven.tool = MAVEN_TOOL // Tool name from Jenkins configuration
          rtMaven.opts = "-Denv=dev"
          rtMaven.deployer releaseRepo:'libs-release-local', snapshotRepo:'libs-snapshot-local', server: server
          rtMaven.resolver releaseRepo:'libs-release', snapshotRepo:'libs-snapshot', server: server

          rtMaven.run pom: 'pom.xml', goals: 'clean install', buildInfo: buildInfo

          buildInfo.retention maxBuilds: 10, maxDays: 7, deleteBuildArtifacts: true
          // Publish build info.
          server.publishBuildInfo buildInfo
      }
    }
    stage('deploy') {
      steps {
        sh "java -jar target/my-app-1.0-SNAPSHOT.jar"
      }
    }
  }
}
