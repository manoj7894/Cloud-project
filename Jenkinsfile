pipeline{
    agent any
    environment {
        PATH = "$PATH:/opt/apache-maven-3.6.3/bin"
    }
    stages {
         stage('SonarQube analysis') {
            steps{
            withSonarQubeEnv('Sonar-Server-7.8') {          
                sh 'mvn sonar:sonar'
            }
                
            }
        }
        stage('Stage-1 : Clean') { 
            steps {
                sh 'mvn clean'
            }
        }
         stage('Stage-2 : Validate') { 
            steps {
                sh 'mvn validate'
            }
        }
         stage('Stage-3 : Compile') { 
            steps {
                sh 'mvn compile'
            }
        }
         stage('Stage-4 : Test') { 
            steps {
                sh 'mvn test'
            }
        }
        stage('Stage-5 : package') { 
            steps {
                sh 'mvn package'
            }
        }
        stage('Stage-6 : verify') { 
            steps {
                sh 'mvn verify'
            }
        }
        stage('Stage-7 : install') { 
            steps {
                sh 'mvn install'
            }
        }
        stage('Stage-8 : Deploy an Artifact to Artifactory Manager i.e. Nexus/Jfrog') { 
            steps {
                sh 'mvn deploy'
            }
        }
        stage('Stage-9 : Deployment - Deploy a Artifact cloudbinay-3.6.3-SNAPSHOT.war file to Tomcat Server') { 
            steps {
                sh 'curl -u admin:Varma_3003 -T target/**.war "http://13.127.99.76:8080/manager/text/deploy?path=/cloudbinary&update=true"'
            }
        }
        stage('Stage-10 : SmokeTest') { 
            steps {
                sh 'curl --retry-delay 10 --retry 5 "http://13.127.99.76:8080/cloudbinary"'
            }
        } 
    }
}
