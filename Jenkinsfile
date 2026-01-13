pipeline{
  agent any
  stages{
    stage('Checkout'){
      steps{
        echo 'fetchingcode'
          checkout scm
    }
    }
     stage('Code quality check!'){
       steps{
         echo 'checking code quality'
         bat '''
         findstr GOOD quality.txt>nul
         if errorlevel 1(
           echo Code Quality Failed
           exit 1
          ) else(
          echo Code Quality Passed
          )
          '''
         
       }
     }
    stage('Generate Report'){
      steps{
        echo 'generating report'
        bat '''
        mkdir reports
        echo Build Successful > reports\\build-report.txt
        '''
    }
    }
    stage('Archive artifacts'){
      steps{
        echo 'archiving reports'
        archiveArtifacts artifacts: 'reports/*.txt', fingerprint: true
    }
    }
  }
  post{
    success{
      echo 'Pipeline completed successfully'
    }
    failure{
      echo 'Pipeline failed-code blocked'
    }
  }
}
