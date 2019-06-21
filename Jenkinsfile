node('rasp'){
    stage('Git Checkout'){
        git credentialsId: 'kevinwood75', url: 'https://github.com/kevinwood75/recipe-app-api2.git', branch: 'master'
    }

    stage('Remove old Container release'){
        sh 'docker-compose down'
    }

    stage('Build Docker Image'){
        sh 'docker-compose build'
    }
    stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerhub')]) {
           sh "docker login -u kwood475 -p ${dockerhub}"
        }
        sh 'docker push kwood475/recipeappapi_app:2.0.0'
    }

    stage('Release Container on Server'){
        sh 'docker-compose up -d'

    }

}
