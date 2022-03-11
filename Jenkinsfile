pipeline
{
    agent any
    stages
    {
        stage('ContinousDownload')
        {
            steps
            {
                script
                {
                    try
                    {
                    git 'https://github.com/selenium-saikrishna/maven.git'    
                    }
                    catch(Exception e1)
                    {
                    mail bcc: '', body: 'Jenkins bis unable to download the development code from the github repo', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'git.admin@gmail.com'    
                    exit(1)
                    }
                }
            }
        }
            stage('ContinousBuild')
        {
            steps
            {
                script
                {
                    try
                    {
                      sh 'mvn package'   
                    }
                    catch(Exception e2)
                    {
                     mail bcc: '', body: 'jenkins build failed', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'dev.team@outlook.com'
                     exit(1)
                    }
                }
               
            }
        }
        stage('ContinousDeployment')
        {
            steps
            {
                script
                {
                    try
                    {
                    deploy adapters: [tomcat9(credentialsId: '31e81552-c19f-46ad-b1a1-71178d95bde2', path: '', url: 'http://172.31.86.183:8080')], contextPath: 'mytestapp', war: '**/*.war'     
                    }
                    catch(Exception e3)
                    {
                    mail bcc: '', body: 'Configuring and deployment stage failed o n QA server', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'middleware.team@outlook.com'    
                    }
                }
            }
        }
        stage('ContinousTesting')
        {
            steps
            {
                script
                {
                    try
                    {
                      git 'https://github.com/marys111/FunctionalTesting.git'
                      sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline22/testing.jar'   
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'selenium scripts are failing', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'testing.team@outlook.com'
                    }
                }
              
            }
        }
        stage('continousDelivery')
        {
            steps
            {
                script
                {
                    try
                    {
                    deploy adapters: [tomcat9(credentialsId: '31e81552-c19f-46ad-b1a1-71178d95bde2', path: '', url: 'http://18.233.150.35:8080')], contextPath: 'prodapp', war: '**/*.war'    
                    }
                    catch(Exception e5)
                    {
                     mail bcc: '', body: 'Delivery failed', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'deliveryteam@outlook.com'   
                    }
                }
            }
        }
    }  
}    

