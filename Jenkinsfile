pipeline{
    agent any
    tools{
           maven "Maven3.6.3"
		   jdk "JDK"
    }
    stages{
        stage ('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to tomcat server') {
            steps{
                script{
                    readProp = readProperties file: 'build.properties'
                }
                echo "This is running on ${readProp['deploy.type']}"
                deploy adapters: [tomcat9(credentialsId: 'tomcat-admin', path: '', url: 'http://10.97.72.168:8888')], contextPath: null, war: '**/*.war'
            }
        }
    }
}