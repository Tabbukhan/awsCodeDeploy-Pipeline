pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main ', url: 'https://github.com/Tabbukhan/awsCodeDeploy-Pipeline.git'
            }
        }
        stage('Package') {
            steps {
                sh 'zip -r PipelineDeployment.zip *'
                archiveArtifacts artifacts: 'PipelineDeployment.zip'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    def codedeploy = awsCodeDeploy(
                        applicationName: 'PipelineDeployment',
                        deploymentGroupName: 'CICD-deploymentGroup',
                        s3bucket: 'tabasumkhanmsa.com',
                        s3prefix: 'PipelineDeployment/',
                        artifactBundle: 'PipelineDeployment.zip',
                        region: 'ap-south-1'
                    )
                }
            }
        }
    }
}
