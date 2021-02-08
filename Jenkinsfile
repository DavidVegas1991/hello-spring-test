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
		stage('spotbugs'){
			steps{
				withGradle{
					sh './gradlew check'
				}
			}
			post{
				always{
					recordIssues enabledForFailure = true,
					tool: [java(), spotbugs (pattern: 'build/reports/spotbugs/*.xml', reportEncoding: 'UTF-8')]
				
				}
			}
			
		}	
	
	}
}