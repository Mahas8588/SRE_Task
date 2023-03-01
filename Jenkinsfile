node{

                 stage('Clone repo'){
                 git branch: 'main', credentialsId: 'Githubcredentials', url: 'https://github.com/Mahas8588/SRE_Task.git'
                }

                stage('Maven Build'){
                def mavenHome = tool name: "Maven-3.9.0", type: "maven"
                def mavenCMD = "${mavenHome}/bin/mvn"
                sh "${mavenCMD} clean package"
                }

                stage('SonarQube analysis') {
                withSonarQubeEnv('Sonar-Server-9.6.1') {
                def mavenHome = tool name: "Maven-3.9.0", type: "maven"
                def mavenCMD = "${mavenHome}/bin/mvn"
                sh "${mavenCMD} sonar:sonar"
                }
        }

                stage('upload war to nexus'){
                        nexusArtifactUploader artifacts: [
                        [
                                artifactId: 'raviproject',
                                classifier: '',
                                file: 'target/raviproject.war',
                                type: 'war'
                                ]
                        ],
                                credentialsId: 'nexus3',
                                groupId: 'in.ravi',
                                nexusUrl: 'http://18.190.160.50:8081/repository/Sidgsrelease/',
                                nexusVersion: 'nexus3',
                                repository: 'Sidgsrelease/',
                                protocol: 'http',
                                version: '2.0.0'
                        }
        }
