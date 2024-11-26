pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    openshift.withCluster() {
                        openshift.withProject() {
                            // 部署 nginx 來服務 HTML 檔案
                            def app = openshift.newApp('nginx~https://github.com/bbbbbear/Jenkins-test.git')
                            
                            // 建立路由
                            openshift.selector("svc", "jenkins-test").expose()
                        }
                    }
                }
            }
        }
    }
}