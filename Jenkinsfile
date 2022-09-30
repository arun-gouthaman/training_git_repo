pipeline {
    agent { label 'instance02' }

    stages {
        stage('GIT') {
            steps {
                echo 'Cloning Git Repo'
                git credentialsId: '003b691b-b230-438e-bc0d-45b860fe0ff1', url: 'https://github.com/arun-gouthaman/training_git_repo.git'
            }
        }
        stage('IMAGE') {
            steps {
                echo 'Building Image'
                sh 'cd /jenkins_dir/workspace/training2_pipeline_job'
                sh 'docker build -t jenkins_job_docker_image:1.0 .'
            }
        }
        stage ('CONTAINER_DELETE') {
            steps {
                script{
                    try {
                        sh 'kubectl delete deploy training-deploy'
                    }
                    catch (err) {
                        echo "Caught: ${err}"
                    }
                }
            }
        }
        stage('CREATE_DEPLOY') {
            steps {
                echo 'Building deployment'
                sh 'kubectl apply -f deploy.yaml'
            }
        }
    }
}

