
pipeline {
   agent any
   stages{
   stage('Checkout or pull from github'){
       steps{
       git credentialsId: 'b8522e92-ee04-461e-9cf3-fe68e9ac6347', url: 'https://github.com/poornimayo/helloworldwithdocker.git'
       } 
   }
   stage('clean and install dependecies'){
   steps{
   bat label: '', script: 'mvn clean install'
   }
   }
      stage('compile'){
            steps{
               bat label: '', script: '''mvn compile

'''
            }
            }
               
   stage('build'){
       steps{
       bat label: '', script: '''mvn clean package
'''
       }
   }
   stage('unit testing')
   {
       steps{
       bat label: '', script: '''mvn test
'''
       }
   }
   stage('run')
   {
       steps{
       bat label: '', script: '''mvn verify

'''
       }
   }
    stage('deploy or deliver to test server'){
         steps{
            deploy adapters: [tomcat8(credentialsId: '45ca00c2-79ff-4e10-9725-721a8308e37e', path: '', url: 'http://localhost:9090/')], contextPath: 'project2', war: '**/*.war'
         }
      }
       stage('cucumber report'){
          steps{
             cucumber failedFeaturesNumber: -1, failedScenariosNumber: -1, failedStepsNumber: -1, fileIncludePattern: '**/*.json', pendingStepsNumber: -1, skippedStepsNumber: -1, sortingMethod: 'ALPHABETICAL', undefinedStepsNumber: -1 
          }
      }
}
}
