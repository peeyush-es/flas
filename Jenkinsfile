node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build & Test image via bash') {
        sh '/space/es-master/exact-dev-build/auth-middleware/build.sh'
    }

    /*stage('Test run') {
        app.inside {
            sh 'cd /tmp/ && python test.py'
        }
    }*/
    
    stage('Push image') {	

        docker.withRegistry('https://dev.exactspace.co') {	
            app.push("${env.BUILD_NUMBER}")	
            app.push("latest")	
        }	
    }

}
