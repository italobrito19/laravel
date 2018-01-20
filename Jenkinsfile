node('php'){
    stage('Clean'){
        deleteDir()
        sh 'ls -la'
    }
    
    stage('Fetch') {
        checkout scm
    }
    
    stage('Build'){
        sh 'composer install --no-scripts --prefer-dist --no-dev --ignore-platform-reqs'
    }
    
    stage('config') {
        parallel(
            'config cache': {
                echo 'tarefa paralela'
            },
            'config route': {
                echo 'tarefa paralela'
            }
        )
    }
    stage('Docker Build') {
        sh 'docker build -t italobrito19/laravel:$BUILD_NUMBER .'
    }
    
    stage('Docker Ship') {
        sh 'docker push italobrito19/laravel:$BUILD_NUMBER'
    }
}
