pipeline {
   environment {
     git_url = "https://github.com/tejStb/java-project.git"
     git_branch = "master"
   }

  agent {label 'dev'}
 
  stages {
    stage('Pull Source') {
      steps {
        git credentialsId: '15652fd5-ba1e-46ef-941d-a884fe4dc92b	', branch: "${git_branch}", url: "${git_url}"
       
      }
     }
    
    stage('Maven Build') {
     steps { 
          sh "mvn clean package && cp target/*.jar . "
     }
    }
     
     stage('Docker Image Build') {     
        steps {
              sh 'sudo docker build -t myimg:1 . '
               }
             }
        stage('Docker image push') {
           steps {
                 withCredentials([usernamePassword(credentialsId: '595bd370-dd46-4e6b-b3bd-cdda21e241d8', passwordVariable: 'Password', usernameVariable: 'Username')]) {
                 sh "sudo docker login -u ${env.Username} -p ${env.Password}"
                 sh "sudo docker image tag saitejstb/myimgubuntu:tagname"
                 sh "sudo docker image pushsaitejstb/myimgubuntu:tagname" 
               } 
             }  
          }
   //   stage('Deploy app') {
   //      steps {
    //        sh 'kubectl apply -f app-deploy.yaml'
    //     }
     // }
    }

//  post {
//    always {
//      deleteDir() /* cleanup the workspace */
//    }
//  }
  }
