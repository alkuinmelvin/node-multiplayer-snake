node ('jenkins-agent-1'){  
    def app
    stage('Cloning Git') {
        /* Let's make sure we have the repository cloned to our workspace */
       checkout scm      /*The checkout step will checkout code from source control, scm is a special variable which instructs the checkout step to clone the specific revision which triggered this Pipeline run.*/
    }  
}
