node{
    def MavenHome=tool name: "maven3.8.1"
    stage('checkout source code from git'){
       git branch: 'UAT', credentialsId: 'a17f2ca5-fcfd-41be-b9c4-d6242242527f', url: 'https://github.com/Mana-org/maven-web-application.git'
    }
    stage('artifact creation using maven tool'){
       sh "${MavenHome}/bin/mvn clean package"
    }
     stage('upload artifact into artifact repository'){
       sh "${MavenHome}/bin/mvn clean deploy"
    }
    stage ('Deploying into tomcat server'){
        sshagent(['52448da1-d988-4f98-975a-650bf42b3d24']) {
    sh " scp -o StrictHostKeyChecking=no target/maven-web-application.war  ec2-user@35.154.237.195:/opt/apache-tomcat-9.0.46/webapps"
}
}
    stage('Email Triggering'){
        emailext body: '''Hi Everyone,

Successfully deployed the build.

Thanks & Regards,
------------------------
Vasavi Tallapaka''', subject: 'Build got over', to: 'tallapakavasavi2121@gmail.com,harikishore.eee@gmail.com'
    }
}
