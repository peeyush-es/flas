node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build & Test image via bash') {
        sh '/space/es-master/build/build.sh'
    }

    /*stage('Test run') {
        app.inside {
            sh 'cd /tmp/ && python test.py'
        }
    }*/
    
    stage('Push image') {	
        /* Finally, we'll push the image with two tags:	
         * First, the incremental build number from Jenkins	
         * Second, the 'latest' tag.	
         * Pushing multiple tags is cheap, as all the layers are reused. */	
        docker.withRegistry('https://dev.exactspace.co') {	
            app.push("${env.BUILD_NUMBER}")	
            app.push("latest")	
        }	
    }

}
