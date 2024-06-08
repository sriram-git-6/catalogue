pipeline {
    agent { node { label 'AGENT-1' }} // since our project is nodejs project our agent should be installed with nodejs
    environment{
        packageVersion = ''
    }
    stages {
        stage('Get version'){
            steps{
                script{
                    def packageJson = readJson(file: 'package.json')
                    packageVersion = packageJson.version
                    echo "version: ${packageVersion}"
                }
            }
        }
        stage('install dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('unit-testing'){
            steps {
                echo "unit testing is done in this stage"
            }
        }    

        stage('sonar scan') {
            steps {
                sh 'ls -ltr'
                sh 'sonar-scanner' // sonar-project.properties file should be available otherwise it will get an error
            }
        }

        stage('build') {
            steps {
                sh 'ls -ltr'
                sh 'zip -r catalogue.zip ./* --exclude=.git --exclude=.zip'
            }
        }

        // install pipeline utility steps plugin    
         stage('publish artifact') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '172.31.86.24:8081/',
                    groupId: 'com.roboshop',
                    version: "$packageVersion", // read the package.json file and get this version dynamically using pipeline utility steps plugin
                    repository: 'catalogue',
                    credentialsId: 'nexus-auth', // store the nexus credentials in manage jenkins-->credentials-->system-->global creds. now this plugin will automatically get the credentials after storing there.
                    artifacts: [
                        [artifactId: catalogue,
                        classifier: '',
                        file: 'catalogue.zip',
                        type: 'zip']
                    ]
                )
            }
        }
      
      // here i need to configure downstream job. Here i need to pass package version for deployment
      // This job will wait until downstream job is over
        
        stage('Deploy'){
            steps{
                script{
                    echo "Deployment"
                    def params = [
                        string(name: 'version', value: "$packageVersion")
                    ]
                    build job: "../catalogue-deploy", wait:true, parameters: params
               }
            }
        } 
    }      
    
    post{
        always {
            echo "cleaning up workspace"
            deleteDir()
        }
    }    
}        
        
    