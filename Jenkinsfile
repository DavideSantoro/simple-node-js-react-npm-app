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
		stage('Deploy to Azure') {
			steps {
				withCredentials([azureServicePrincipal(credentialsId: '02102024')]) {
					script {
						// Autenticati su Azure
						sh """
						az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET --tenant $AZURE_TENANT_ID
						# Effettua il deploy specificando la cartella build
						az webapp up --resource-group jenkinsdemo --name frontend-test --location <your_location> --plan <your_app_service_plan> --sku <your_sku> --src-path build
						"""
					}
				}
			}
		}

    }
}
