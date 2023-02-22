pipeline {
    agent any
    stages {
       stage("Generating OIDC token and saving it to a file") {
            steps {
                script {
                        sh (script: 'gcloud auth print-identity-token token-creator@tk-project-27068.iam.gserviceaccount.com  --audiences="//iam.googleapis.com/projects/166428984884/locations/global/workloadIdentityPools/jenkins/providers/google-jenkins"  > /usr/share/token/key',returnStdout: true)
                }
            }
        }
        stage ("getting the WIF config file into a variable")
        {
            steps {
                     withCredentials([file(credentialsId: 'wif-config-file', variable: 'WIF')]) 
                        {
                         sh '''
                            gcloud auth login --brief --cred-file=$WIF --quiet
                            gcloud container clusters list
                            gcloud compute instances list
                            '''

                        }
                }
        }
    }    
}