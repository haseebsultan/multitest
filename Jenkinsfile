pipeline {
    
   agent{
    node {
label 'linux'
    }   }   
   

    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
             //   sh 'npm install'
              //  emailext body: 'buil done', subject: 'testemail', to: 'nida.hayat@systemsltd.com'
                echo 'building'
            }
        }
        stage('Test') {
            steps {
         //       sh './jenkins/scripts/test.sh'
                echo 'test'
            }
        }
       
        stage('aproval qa')
            {
            agent none
            steps {
            emailext (
  subject: "Waiting for your Approval! Job: '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
  body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
              <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
  to: 'nida.hayat@systemsltd.com'
)
                 input message: 'Finished using the web site? (Click "Proceed" to continue)'
        }
            }
        
         stage('D development') {
             
             steps{
             
             echo 'deploying'
             }
             
             
             
         }
        stage('Deliver for development') {
            when {
                branch 'development'
            }
            steps {
              //  sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {
                sh './jenkins/scripts/deploy-for-production.sh'
            
            }
        }
    }
}
