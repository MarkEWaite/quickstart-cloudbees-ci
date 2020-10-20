pipeline {
    agent {
        label '!windows && git-1.9+' // !windows so I can run a shell command after checkout
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/submodule-experiment']], 
                    extensions: [
                        [$class: 'SubmoduleOption', parentCredentials: true, recursiveSubmodules: true, threads: 3]
                    ],
                    userRemoteConfigs: [
                        [credentialsId: 'MarkEWaite-github-rsa-private-key', url: 'git@github.com:MarkEWaite/quickstart-cloudbees-ci.git']]
                ])
                echo 'Should list 4 submodules quickstart-amazon-eks, quickstart-amazon-eks-cluster-resource-provider, quickstart-aws-vpc, and quickstart-linux-bastion'
                sh 'git submodule foreach --recursive git remote -v | grep fetch'
            }
        }
    }
}

