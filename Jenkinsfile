stage('Deploy to Azure') {
    steps {
        withCredentials([azureServicePrincipal(credentialsId: '02102024')]) {
            script {
                // Autenticati su Azure
                sh """
                az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET --tenant $AZURE_TENANT_ID
                # Effettua il deploy specificando la cartella build
                az webapp up --resource-group jenkinsdemo --name frontend-test --src-path build
                """
            }
        }
    }
}
