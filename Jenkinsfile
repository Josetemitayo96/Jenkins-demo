
node {
    def commit_id

    stage('preparation'){
        checkout scm
        sh "git rev-parse --short HEAD > .git/commit-id"
        commit_id = readFile('.git/commit-id').trim()
    }

    stage('Test'){
        nodejs(nodeJSInstallationName: 'nodejs'){
            sh 'npm install --only=dev'
            sh 'npm test'
        }
        stage('docker build/push'){
            docker.withRegistry('https://index.docker.io/v1/', 'dockerhub'){
                def app = docker.build("tayo96/docker-node-app:${commit_id}", '.').push()
            }
        }
    }
}

