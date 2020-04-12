pipeline { 
    agent any
    triggers{
     cron('H*/1 * * *')
    }
   
  stages {
     stage('Print hello') {
      steps {
        echo 'hello'

    }

    tools {
        maven 'M2_HOME'
    }
    stages {
      stage('Build'){
        steps {
          echo "Build step"
          sh 'mvn clean'
          sh 'mvn install'
          sh 'mvn package'
        }
      
      
      }
        stage('test '){
        steps {
          echo "test step"
          sh 'mvn test'
        }
      
      
      }
        stage('deploy'){
        steps {
           
          sshPublisher(publishers: [sshPublisherDesc(configName: 'Docker', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'docker rmi elise66/texasreview:1.0; docker build -t elise66/texasreview:1.0 .; docker push elise66/texasreview:1.0', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: 'webapp/target', sourceFiles: '**/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
        }
      
      
      }
    
    }
    post {
        always {
            echo "always display this message"
        }
          failure {
             echo "job failed"
            
        }
        success {
          echo "successfully run"
        }
        
        unstable {
           echo " the job is unstable"
        }
        
        
        
    }

}

