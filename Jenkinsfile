node('Ubuntu-Approver-3120')
{

def app
stage('Cloning Git')
{
    /* Let's make sure we have the repository cloned to our workspace */
    checkout scm
}
    
stage('Build-and-Tag')
{
    /* This builds the actual image;
        * This is synonomous to docker build on the command line */
    app = docker.build('loadinq/chat')    
}

stage('Push-to-Dockerhub')
{
    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
    {
        app.push('latest')
    }    
}

stage('Deploy')
{
    sh 'docker-compose down'
    sh 'docker-compose up -d'
}

}