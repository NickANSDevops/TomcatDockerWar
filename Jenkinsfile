pipeline {
     agent any
     stages {
          stage("Compile") {
               steps {
                    sh "/usr/bin/mvn clean compile"
               }
          }
          stage("Unit test") {
               steps {
                    sh "/usr/bin/mvn test"
               }
          }
     
    
stage("Package") {
     steps {
          sh "/usr/bin/mvn package"
     }
}
stage("Docker build") {
     steps {
      
          sh "docker build -t nicky_tomcat ."
     }
}

stage("Deploy to staging") {
     steps {
          
          sh "docker run --name check -d ubuntu"
          sh "docker stop \$(docker ps -qa)"
          sh "docker rm \$(docker ps -qa)"
          sh "docker run -d -it -v /var/lib/jenkins/workspace/docker_pipeline/target/:/usr/local/tomcat/webapps/ -p 8091:8080 --name Testtomcat nicky_tomcat"
     }
}

     }
  post {
     always {
          sh "echo 'I did It'"
     }
}
}
