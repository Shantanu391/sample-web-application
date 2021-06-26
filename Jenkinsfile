pipeline{

    agent any
    tools{
        maven "maven_3_5_0"
    }
   
stages{
    stage('sonar')
        {
      steps{
          script{
              withSonarQubeEnv('sonar') { 
          sh "mvn sonar:sonar"
              }
                }
            }
         }
    
      stage('Quality Gate Statuc Check'){
          steps{
              script{
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                   error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
            }
          }
        }  
      }
      stage('build')
        {
      steps{
          script{
           sh 'mvn clean install'
                }
            }
         }
       }
    

}
