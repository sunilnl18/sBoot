pipeline {
	agent any
	stages {
	    stage ('clean up') {
	        steps {
	            cleanWs()
	        }
	    }
	    
	    stage ('clone') {
			steps {
				sh 'git clone https://github.com/sunilnl18/sBoot.git'
			}
	    }
		stage ('build') {
			steps {
			    dir ('sBoot'){
				    sh 'mvn clean install -DskipTests'
			    }
			}
		
		}
		stage ('test') {
			steps {
			    dir ('sBoot') {
				    sh 'mvn test'
			    }
			}
			post {
				always {
				    dir ('sBoot') {
					    junit 'target/surefire-reports/*.*xml'
					    archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
				    }
				}
			}
		}
	}	
}	
