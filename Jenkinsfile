node ('jenkins-agent-1'){  
    def app
    stage('Cloning Git') {
        /* Let's make sure we have the repository cloned to our workspace */
       checkout scm      /*The checkout step will checkout code from source control, scm is a special variable which instructs the checkout step to clone the specific revision which triggered this Pipeline run.*/
    }  
    /*stage('SAST'){
        build 'SECURITY-SAST-SNYK'
    } */
    
    //stage('Build-and-Tag') {
    /* This builds the actual image; synonymous to
         * docker build on the command line */
    //    app = docker.build("alkuinmelvin/snake:new")
    //}
    /*stage('Post-to-dockerhub') {
    
     docker.withRegistry('https://registry.hub.docker.com', 'Github and Jenkins Credential') {
            app.push("latest")
        			}
         }*/
    /*stage('SECURITY-IMAGE-SCANNER'){
        build 'SECURITY-IMAGE-SCANNER-AQUAMICROSCANNER'
    }*/
  
    
    /*stage('Pull-image-server') {
    
         sh "docker-compose down"
         sh "docker-compose up -d"	
      }*/
    
    /*stage('DAST')
        {
        build 'SECURITY-DAST-OWASP_ZAP'
        } */
 
}
