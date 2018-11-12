pipeline { 
    agent { label "node1" }
    stages {
        stage('SCM_Chekout') { 
            steps { 
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    doGenerateSubmoduleConfigurations: false, 
                    extensions: [], 
                    submoduleCfg: [], 
                    userRemoteConfigs: [[url: 'https://github.com/ganeshhp/helloworldweb.git']]])
            }
        }
        stage('Build'){
            steps {
                sh 'mvn -f pom.xml clean package' 
            }
        }
	}

    agent { label "node2" }
	
        stage('Deploy') {
            steps {
                wget https://github.com/ganeshhp/helloworldweb/tree/master/target/Helloworldwebapp.war
				sh 'cp ./Helloworldwebapp.war /opt/tomcat/apache-tomcat-7.0.78/webapps/'
                sh '/opt/tomcat/bin/shutdown.sh'
                sh '/opt/tomcat/bin/startup.sh'
            }
        }
    }