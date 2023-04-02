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
                    echo "Maven_HOME = ${Maven_HOME}"
            ''' 
      }
    }
    
    
  }
}
