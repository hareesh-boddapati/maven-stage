node
{
    def mvnHome = tool name: "maven3.6.3"
    stage("check out code")
    {
       git 'https://github.com/hareesh-boddapati/maven-stage.git' 
    }
    stage("build the code")
    {
        sh "${mvnHome}/bin/mvn clean package"
    }
    stage("docker build")
    {
        sh "docker build -t hareeshdock/app:1 ."
    }
    stage("push docker image")
    {
        withCredentials([string(credentialsId: 'docker_hub_passwd', variable: 'docker_hub_pwd')])
        {
             sh "docker login -u hareeshdock -p ${docker_hub_pwd}"
             sh "docker push hareeshdock/app:1"
        }
    }
    stage("deploy docker image into deployment server")
    {
        def dockerRun = "docker run -d -p 8080:8080 --name containername  hareeshdock/app:1 "
        sshagent(['ubuntu-docker']) 
        {
            sh "ssh -o StrictHostKeyChecking=no ubuntu@13.233.157.133"
           
            sh "ssh ubuntu@13.233.157.133 ${dockerRun}"
        }
    }
    
}
