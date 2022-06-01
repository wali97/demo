pipeline {
    
	  agent any
  tools {nodejs "node"}

	environment{
	registry="mrchelsea"
	registryCredential='dockerhub'
	dockerImage=''
	}
    
	stages{
	stage('Git') {
		steps{
		git 'https://github.com/rahulguptaft9/demo123'
		}	
	}
		
	/*stage('Build'){
		steps{
		//sh 'cd $JENKINS_HOME/workspace/serverclienttesting/client'
		sh 'npm cache clean -force'
		sh 'cd $JENKINS_HOME/workspace/serverclienttesting/client &&  npm install'
		sh 'cd $JENKINS_HOME/workspace/serverclienttesting/client && npm install -g jest'
		sh 'cd $JENKINS_HOME/workspace/serverclienttesting/client && npm  run build'
		
		}
	}*/	
		
	/*stage('Code Coverage'){
		steps{	
			script{
		sh 'npm run test-cov'
		}
		step([$class: 'CoberturaPublisher', coberturaReportFile: 'output/coverage/jest/cobertura-coverage.xml'])	
		}
	}*/
		
	/*stage('SonarQube'){
		tools{
		jdk "jdk11"
		}
		steps{
		script {
          	scannerHome = tool 'sonar_coverage';
        	}
		withSonarQubeEnv('sonar_coverage'){
		sh '''
		/var/lib/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/sonar_coverage/bin/sonar-scanner \
		-Dsonar.host.url=http://192.168.122.141:9004/sonarqube \
		-Dsonar.login=443b17ef84fc21dfd66dba03fc8fe3299edae9de \
		-Dsonar.projectKey=rahul \
		-Dsonar.projectName=rahul					
		'''

		}		
		}
	
	}*/	
		
	
	stage('Building image for front end') {
		steps{
			script{
				sh 'docker build -f Dockerfile -t $registry/rahulg123 .'
               
			}
		}
	}
		
	stage('Registring image for front end') {
		steps{
			script{
				docker.withRegistry('',registryCredential){
				sh 'docker push $registry/rahulg123'
                       		
				}
			}
		}
	}	
	/*stage('Registring image for front end') {
		steps{
			script{
				docker.withRegistry('',registryCredential){
				dockerImage.push()
				}
			}
		}
	}*/
	}
		post{
			always{
			emailext body: 'A Test Email', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
			}
		}
	

}
