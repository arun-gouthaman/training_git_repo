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
        stage ('CONTINER_DELETE') {
            steps {
                script{
                    try {
                        sh 'docker rm -f jenkins_job_container'
                    }
                    catch (err) {
                        echo "Caught: ${err}"
                    }
                }
            }
        }
        stage('CREATE_CLUSTER') {
            steps {
                script {
                    try {
                        sh 'kind create cluster --config cluster_configfile'
                    } 
                    catch (err) {
                        echo "Caught: ${err}"
                    }
                }
            }
        }
}

