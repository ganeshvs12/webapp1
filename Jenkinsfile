pipeline {
  agent any 
  tools {
    maven 'Maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }    
      
    }
    
     stage ('Check-Git-Secrets') {
      steps {
        sh 'rm trufflehog || true'
        sh 'docker run gesellix/trufflehog --json https://github.com/ganeshvs12/webapp.git > trufflehog'
        sh 'cat trufflehog'
      }
    }
    
  
    
       stage ('Build') {
      steps {
      sh 'mvn clean package'
       }
    }
    
   
  
    stage ('DAST') {
      steps {
        sshagent(['zap']) {
         sh 'ssh -o  StrictHostKeyChecking=no ubuntu@54.234.49.62 "docker run -t owasp/zap2docker-stable zap-baseline.py -t http://100.26.112.43:8080/webapp/" || true'
        }
      }
    }
    
    
    
  }
}
