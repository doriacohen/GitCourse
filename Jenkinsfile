pipeline {
  agent { node { label 'slave01' } }

   stages {
      stage('Clone Sources') {
        steps {
          checkout scm
        } 
      }
      stage('Build') {
         steps {
            echo 'Build process..'            
            sh '''
                cd "${WORKSPACE}/bash/"
                chmod 755 *
            '''
         }
      }      
        stage("Env Variables") {
            steps {
                sh "printenv"
            }
        }    
      stage('Test') {
         steps {
            echo 'Test process..'
            sh '''
              echo "Testing input string $BASH" 
              cd "${WORKSPACE}/scripts"
              ./reverse.sh $BASH
              ./reverse.sh $BASH > results
            '''
         }
      }
      stage('Saving Results') {
         steps {
            echo 'Saving Results process..'
            sh '''
	      report_file="${HOME}/Documents/Deployment/report"
              mkdir -p ${HOME}/Documents/Deployment/              
              if [ -f "${report_file}" ]; then
                echo "file ${report_file} exists"
              else
	              touch ${report_file}
              fi
	      date >> ${report_file}
	      echo "USER=$USER JOB_NAME=$JOB_NAME" >> ${report_file}
              echo "Build Number $BUILD_NUMBER" >> ${report_file}
              cat "${WORKSPACE}/scripts/results" >> ${report_file}
	      echo "#############################" >> ${report_file}
            '''
         }
      }
      
   }
}
		success {   
			sh 'echo "BUILD_NUMBER=$BUILD_NUMBER success" >> report' 
		}   
		failure {
			sh 'echo "BUILD_NUMBER=$BUILD_NUMBER failed" >> report'   
		}   
		unstable {   
			echo 'I will only get executed if this is unstable'   
		}   
   }
}
