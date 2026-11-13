pipeline{
	agent any
	stages{
		stage('Checkout'){
			steps{
				checkout scm
			}
		}
		stage('Build'){
			steps{
				sh 'python3 -m py_compile app.py'
			}
		}
		stage('Test'){
			steps{
				sh 'python3 -m unittest -v'
			}
		}
		stage('Package'){
			steps{
				sh 'tar -czf "python-app-${BUILD_NUMBER}.tar.gz" app.py test_app.py'
		
				archiveArtifacts artifacts: 'python-app-*.tar.gz', fingerprint:true

			}
		}
	}
	post{
		success{
			echo 'succeeded'
		}
		failure{
			echo 'failed'
		}
	}
}
