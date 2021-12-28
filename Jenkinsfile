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
            sh 'echo "My first pipeline"'
            sh '''
                echo "By the way, I can do more stuff in here"
                ls -la ~
		touch report
            '''
         }
      }
      stage('Test') {
         steps {
            echo 'Test process..'
	    sh 'exit 0'
         }
      }
      stage('Deploy') {
         steps {
            echo 'Deploy process..'
         }
      }
      
   }
   post {   
		always {
			sh 'printenv'   
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
