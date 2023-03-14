pipeline {
    agent any
    tools{
        maven 'maven3.9.0'
    }

    stages {
        stage('Clone the repository ') {
            steps {
                
             git branch: 'build-and-push-to-jfrog-jenkinsfile', credentialsId: 'Github_credentails', url: 'https://github.com/sdk2022/java-application.git'   
                
            }
        }
       
       stage("Build the code") {
           
           steps{
               sh 'mvn clean install'
           }
       }
      stage('Push the artifacts into Jfrog artifactory') {
            steps {
              rtUpload (
                serverId: 'Jfrog-dev-server',
                spec: '''{
                      "files": [
                        {
                          "pattern": "*.war",
                           "target": "demo-app/"
                        }
                    ]
                }'''
              )
          }
        }
     
        
        
        
    }
}
