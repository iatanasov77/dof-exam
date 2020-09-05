def imagetag = new Date().format('yyyyMMdd.HHmmss')
def image1 = "iatanasov77/dof-exam-nginx:${imagetag}"
def image2 = "iatanasov77/dof-exam-php:${imagetag}"
def appRoot = "/vagrant/jenkins.d/slaves/docker_host/workspace/RetakeExam-Application"

node(label: 'k8s-master')
{
    stage('Checkout')
    {
        echo 'Cloning sources ...'
        
        sh 'if [ "$(ls -A .)" ]; then git pull origin master; else git clone https://github.com/iatanasov77/dof-exam.git .; fi'
        
    }
    
    stage('Build and Push new Docker images') 
    {
      sh 'runuser -l  vagrant -c "docker build /opt/jenkins_slave/workspace/RetakeExam-Application/nginx -t ${image1} ."'
      sh 'runuser -l  vagrant -c "docker push ${image1}"'
      
      sh 'runuser -l  vagrant -c "docker build /opt/jenkins_slave/workspace/RetakeExam-Application/php -t ${image2} ."'
      sh 'runuser -l  vagrant -c "docker push ${image2}"'
    }
    
    stage('Kubernetes Deploy')
    {
        echo 'Deploy to Kubernetes ...'
        
        //sh "sed 's/%APP_ROOT%/${appRoot}/g' -i kubernetes.yml"
        //sh "sed 's/%IMAGE1-PLACEHOLDER%/${imagetag}/g' -i kubernetes.yml"
        
        //sh 'runuser -l  vagrant -c "kubectl delete -f /opt/jenkins_slave/workspace/RetakeExam-Application/kubernetes.yml"'
        //sh 'runuser -l  vagrant -c "kubectl create -f /opt/jenkins_slave/workspace/RetakeExam-Application/kubernetes.yml"'
        
        
        //sh 'runuser -l  vagrant -c "kubectl delete -f /vagrant/app/kubernetes.yml"'
        sh 'runuser -l  vagrant -c "kubectl create -f /vagrant/app/kubernetes.yml"'
    }
}
