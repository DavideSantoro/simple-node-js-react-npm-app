pipeline {
    agent any
    stages {
		stage('Clone Repository') {
			steps {
				git 'https://github.com/DavideSantoro/simple-node-js-react-npm-app.git'
			}
		}
		stage('Build React App') {
			steps {
				script {
					// Installa dipendenze e build
					sh 'npm install'
					sh 'npm run build'
				}
			}
		}
		stage ('Zip Build') {
			steps {
				sh 'zip -r /var/lib/jenkins/build.zip build'
			}
		}
		stage('Deploy to Azure') {
			steps {
				withCredentials([azureServicePrincipal(credentialsId: '02102024')]) {
					sh """
					# Autenticati su Azure
					az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET --tenant $AZURE_TENANT_ID

					# Effettua il deploy sul servizio App
					az webapp deployment source config-zip --resource-group jenkinsdemo --name frontend-test --src /var/lib/jenkins/build.zip
					"""
				}
			}
	}


    }
}