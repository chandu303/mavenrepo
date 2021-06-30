pipeline{
agent {label 'devslave'}
triggers { pollSCM('* * * * *') }
stages{
stage('git'){
steps{
checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: '5c7bae99-7fb3-45fb-b9b3-58f6dd2627f3', url: 'https://github.com/chandu303/mavenrepo.git']]])
}
}
stage('package'){
steps{
    sh 'mvn package'
}
}
stage('sonar'){
steps{
withSonarQubeEnv('sonarqube') {
    sh 'mvn sonar:sonar'
}
}
}
stage('nexus'){
steps{
    sh 'mvn deploy'
}
}
stage('tomcat'){
steps{
    sh 'scp /root/workspace/samplejob/target/studentapp-2.5-SNAPSHOT.war 172.31.35.235:/var/lib/tomcat/webapps'
}
}

}
}
