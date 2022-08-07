pipeline
{
 agent any
 stages
 {
      stage("Fetching the Code")
      {
        steps
        {
            git branch: 'main', url: 'https://github.com/varunpasumarthi/Nodejs-project.git'
        }
      }
      stage("Build Docker image")
      {
        steps
        {
            sh 'docker build -t varunpasumarthi/nodejsapp .'
        }
      }
      stage("Pushing the Docker image")
      {
        steps
        {
           withCredentials([string(credentialsId: 'varunpasumarthi', variable: 'dockerhubpwd')]) 
           {
             sh 'docker login -u varunpasumarthi -p ${dockerhubpwd}'
           }
           sh 'docker push varunpasumarthi/nodejsapp'
        }
      }
      stage('Deploying App to Kubernetes') 
      {
        steps 
        {
          script 
          {
          kubernetesDeploy(configs: "nodejs-application.yml", kubeconfigId: "kubeconfig")
          }
        }
      }  
  }
}
