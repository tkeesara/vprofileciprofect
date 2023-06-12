pipeline {
    
	agent any
	
	tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }
	
    environment {
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = "admin"
        NEXUS_PASS = "admin123"
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUSIP = '172.31.35.232'
        NEXUSPORT = '8081'
        NEXUS_GRP_REPO = 'vpro-maven-group'
	    NEXUS_CREDENTIAL_ID = "nexuslogin"
        
            }
	
    stages{
        
        stage('BUILD'){
            steps {
                sh 'mvn clean install -DskipTests install'
            }
           post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('UNIT TEST'){
            steps {
                sh 'mvn test'
            }
        }
       stage ('CODE ANALYSIS WITH CHECKSTYLE'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            } 
       }

   }
}
	