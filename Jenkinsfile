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
					tool: pmdParser(pattern: 'build/reports/pmd/*.xml')
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
					junit 'build/test-results/test/TEST-*.xml'
					recordIssues enabledForFailure: true,
					tool: pmdParser(pattern: 'build/reports/pmd/*.xml')
				}
			}
		}	
	
	}
}
