node('built-in') {
    stages{
    stage('continous download'){
        git 'https://github.com/sunildevops77/maven.git'
    }
    stage('continous build'){
        sh 'mvn package'
        }
    stage('continous deployment'){
        script{
            sshagent(['Jenkins']){
                sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/pipe1/webapp/target/webapp.war ubuntu@172.31.30.105:/var/lib/tomcat9/webapps/qaenv.war'
        }
    }
    } 
    stage('continous testing'){
        sh 'echo "Testing passed"'
    }
    
     stage('continous delivery '){
        script{
            sshagent(['Jenkins']){
                sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/pipe1/webapp/target/webapp.war ubuntu@172.31.19.241:/var/lib/tomcat9/webapps/prodenv.war'
        }
    }
    }
    }
    post{
        success{
            emailext attachLog: true, body: 'Success', subject: 'Jenkins mail', to: 'kittu.sahana@gmail.com'
        }
        failure{
            emailext attachLog: true, body: 'Failed', subject: 'Jenkins mail', to: 'kittu.sahana@gmail.com'
        }
    }
    
}
