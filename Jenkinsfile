node('appserver'){
    stage('Git Checkout'){
        git credentialsId: 'kevinwood75', url: 'https://github.com/kevinwood75/recipe-app-api2.git', branch: 'master'
    }
    stage('Build Docker Image'){
        sh 'docker-compose build'
    }
    stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerhub')]) {
           sh "docker login -u kwood475 -p ${dockerhub}"
        }
        sh 'docker push kwood475/recipeappapi2_app:2.0.0'
        sh 'docker push kwood475/postgres:10-alpine'
    }
    stage('Remove old Container release'){
        sh 'docker stop recipeappapi2_app_1'
        sh 'docker stop recipeappapi2_db_1'
        sh 'docker rm recipeappapi2_app_1'
        sh 'docker rm recipeappapi2_db_1'
    }

    stage('Release Container on Server'){
        sh 'docker-compose up -d'

    }

}
