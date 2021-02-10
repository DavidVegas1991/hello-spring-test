pipeline{
	agent any
	stages{
		stage('Test'){
			steps{
				withGradle{
					sh './gradlew clean test check'
				}
			}
			post{
				always{
					junit 'build/test-results/test/TEST-*.xml'
					recordIssues enabledForFailure: true,
					tool: spotBugs(pattern: 'build/reports/spotbugs/*.xml')
				}
			}
	
		}
		stage('QA'){
			steps{
				withGradle{
					sh './gradlew check'
				}
			}
			
			post{
				always{
					
					recordIssues enabledForFailure: true,
					tool: pmdParser(pattern: 'build/reports/pmd/*.xml')

				}
			}
		}	
		
		stage('owaps'){
			
			steps{
				sh './gradlew clean dependencyCheckAnalyze'
			

                dependencyCheckPublisher pattern: 'build/reports/dependency-check-report.xml'
			}
			
		}

		stage('publish'){
			steps{
				
				//withCredentials([string(credentialsId: 'gitLabPrivateToken', variable: 'TOKEN')]){
				//	sh './gradlew publish'
				//}
				withCredentials([usernamePassword(credentialsId: 'ApacheArchiva', passwordVariable: 'Password', usernameVariable: 'Username')]){
					sh './gradlew publish'
				}
			}
			

		}

	
	}
}