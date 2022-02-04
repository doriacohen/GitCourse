pipeline {
	agent any
	
	sh 'echo "bla bla bla"'
	
	stages {
		stage('Clone Sources') {
			steps {
			        checkout scm          
			} 
		}   
		stage('Log File Event') {
			steps {
			        sh '''
				    cd ${WORKSPACE}/Scripts/
				    touch output.txt
				    date >> output.txt
                                   '''
			}
		}
		stage('Bash script') {
			when{
				expression{ return params.LANGUAGE == 'Bash' || params.LANGUAGE == 'All' }
			}
			steps {      
				sh '''
					cd ${WORKSPACE}/Scripts/
					chmod 755 bash_project.sh
					./bash_project.sh 
					cat bash_project.sh >> output.txt
					else
					echo "Bash file is not selected! "
					fi
					'''
				}
		 }  
		 stage('Python script') {
		 	when{
				expression{ return params.LANGUAGE == 'Python' || params.LANGUAGE == 'All' }
			}
			steps {
				sh '''
					cd ${WORKSPACE}/Scripts/
					chmod 755 python_project.py 
					python3.9 python_project.py
					cat python_project.py >> output.txt
					else
					echo "Python file is not selected! "
					fi
				    '''
				}
			}
		 stage('C file') {
		 	when{
				expression{ return params.LANGUAGE == 'C' || params.LANGUAGE == 'All' }
			}
			steps {
				sh '''
					cd ${WORKSPACE}/Scripts/
					chmod 755 c_project.c
					gcc c_project.c -o c_project_compiled
					./c_project_compiled 
					cat c_project.c >> output.txt
					else
					echo "C file is not selected! "
					fi
					'''
				}
	  		}  
	}
}
