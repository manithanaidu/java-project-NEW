pipeline {
  agent {
    label 'java-slave'
  }
  tools {
    maven 'maven'
  }
  stages {
    stage('SonarQube Analysis') {
      steps {
        sh 'sonar-scanner -X -Dsonar.sources=. -Dproject.settings=sonar-project.properties -Dsonar.projectKey=java_app -Dsonar.host.url=$SonarQube_URL -Dsonar.login=$SonarQube_Access_Token'
      }
    }
    stage('Build app') {
      steps {
        sh 'mvn clean install package'
      }
    }
    stage('Push Artifact to S3') {
      steps {
        sh 'aws s3 cp webapp/target/webapp.war s3://demomaster3'
      }
    }
    // stage('DockerBuild') {
    //  steps {
    //   sh 'docker build -t java .'
    //  }
    // }
    // stage('Deploy to tomcat') {
    //   steps {
    //     sshagent(['tomcat-server-details']) {
    //     sh 'scp -o "StrictHostKeyChecking=no" webapp/target/webapp.war ubuntu@18.117.85.70:/opt/tomcat/webapps'
    //     }
    //   }
    // }
    // stage('Deploy to tomcat') {
    //   steps {
    //        sh 'sudo scp -i demo.pem -o "StrictHostKeyChecking=no" webapp/target/webapp.war ubuntu@65.0.3.198:/opt/tomcat/webapps'
    // }
    // }
}
// post {
//      always {
//        emailext to: 'lakshmiphanindrarudra@gmail.com',
//        attachLog: true, body: "Dear team pipeline is ${currentBuild.result} please check ${BUILD_URL} or PFA build log", compressLog: false,
//        subject: "Jenkins Build Notification: ${JOB_NAME}-Build# ${BUILD_NUMBER} ${currentBuild.result}"
//     }
// }
}
