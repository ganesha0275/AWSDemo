pipeline {
     agent any
     stages {
          stage("Compile") {
               steps {
                    sh "/opt/homebrew/bin/mvn compile"
               }
          }
          stage("Unit test") {
               steps {
                    sh "/opt/homebrew/bin/mvn test"
               }
          }
     
    
stage("Package") {
     steps {
          sh "/opt/homebrew/bin/mvn package"
     }
}
stage("Docker build") {
     steps {
      
          sh "docker build -t deepak_tomcat ."
     }
}

stage("Deploy to staging") {
     steps {
          
          sh "docker stop \$(docker ps -qa)"
          sh "docker rm \$(docker ps -qa)"
          sh "docker run -d -it -v /var/lib/jenkins/workspace/jenkins-docker-demo-pipeline/target/:/usr/local/tomcat/webapps/ -p 8091:8080 --name Testtomcat deepak_tomcat"
     }
}

     }
  post {
     always {
          sh "echo 'I did It'"
     }
}
}
