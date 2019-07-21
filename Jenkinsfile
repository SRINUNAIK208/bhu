node(){
    
    def mvnHome = tool name: '3.6.0',type: 'maven'
    
    stage('checkout'){
        
       git credentialsId: 'a2de7279-4408-460f-842b-97cd5f9cb763', url: 'https://github.com/SRINUNAIK208/bhu.git' 
    }
    stage('build'){
        sh "${mvnHome}/bin/mvn clean package"
    }
    stage('sonarreport'){
        sh "${mvnHome}/bin/mvn clean sonar:sonar"
    }
    stage('deploynexus'){
        
        sh "${mvnHome}/bin/mvn clean deploy"
        
    }
    stage ('tomcat'){
        
        sshagent(['tomcatserver']) {
          sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.127.12.169:/opt/apache-tomcat-9.0.20/webapps/maven-web-application.war"
        }
    
    }
}
    
        
        

