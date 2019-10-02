node {
    stage('git clone/pull'){
        git changelog: false, credentialsId: 'github_id', poll: false, url: 'https://github.com/reechasoni/python-app.git'
    }
    stage('image-build'){
        sh "docker build -t reechasoni/python-app:1.2 ."
        withCredentials([string(credentialsId: 'reechasoni', variable: 'hello')]) {
    sh "docker login -u reechasoni -p ${hello}"
     } 
        sh "docker push reechasoni/python-app:1.2"
        sh "ssh -o StrictHostKeyChecking=no -i /var/lib/jenkins/dev.pem ec2-user@172.31.89.26 docker run -d -p 8081:5000 reechasoni/python-app:1.2"
    }
}
