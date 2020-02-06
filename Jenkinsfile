node
{
    def mavenhd = tool name: "maven"
  
    stage("checkout code")
    {
        git url: 'https://github.com/hareesh-boddapati/maven-stage.git',branch: 'dev'
    }
    stage("build")
    {
        sh "${mavenhd}/bin/mvn clean package"
    }
    stage("deployment")
    {
        /*sshagent(['deployapptom']) {
        sh "scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.127.158.118:/opt/tomcat/tomcat9/webapps/"
*/
deploy adapters: [tomcat9(credentialsId: 'b8b9f833-619c-420e-ad49-56b61ccda728', path: '', url: 'http://13.127.158.118:8080/')], contextPath: null, war: '**/*.war'



    
    }
}
