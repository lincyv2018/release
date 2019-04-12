pipeline{
    agent{
        label "master"
    }
    parameters {
        string(name: "message" defaultValue: "Release message" description: " start messagee" )
        choise(name: "release type")
    }
    stages{
        stage("Send Notification"){
            steps{
                   
                sh '''
                python /scripts/custom_start.py ${params.message}
                
                '''       
            }
        } 
        stage("geting the server status"){
                steps{
               
                       sh '''
                        web_server_bot=$(curl -s --netrc-file /scripts/rc.netrc https://172.20.6.52:8080/api/3/http/upstreams/web_servers_bot)
                        echo $web_server_bot
                        '''                   
                }
             }
            stage("bring the servers up"){
                steps{
                    echo "bring the servers up"
                }
                }
            stage("removing stack of 4"){
                steps{
                    sh ''' web_server_bot3=$(curl -s --netrc-file /scripts/rc.netrc https://172.20.6.52:8080/api/3/http/upstreams/web_servers_bot)'''
                }
               }
            stage("activating VSTS releases"){
                steps{
                    echo "VSTS pull"
                }
                  }
            stage("bring the next set of server"){
                steps{
                    sh '''web_server_bot5=$(curl -s --netrc-file /scripts/rc.netrc https://172.20.6.52:8080/api/3/http/upstreams/web_servers_bot)'''
                }
                   }
            stage("activating VSTS releases for second set "){
                steps{
                   sh '''web_server_bot6=$(curl -s --netrc-file /scripts/rc.netrc https://172.20.6.52:8080/api/3/http/upstreams/web_servers_bot)'''
                }
                 }
            stage("restoring the server status"){
                steps{
                    sh '''web_server_bot7=$(curl -s --netrc-file /scripts/rc.netrc https://172.20.6.52:8080/api/3/http/upstreams/web_servers_bot)'''
                }
                }
            stage("Completed Notification"){
                steps{
                    sh '''
                    python /scripts/custom_end.py "Release completed. Servers are back in cluster."
                    
                    '''
                }
               }
            

        }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}