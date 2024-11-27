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
                    try {
                        openshift.withCluster() {
                            openshift.withProject() {
                                // 使用簡單的部署方式
                                def app = openshift.newApp('nginx~https://github.com/bbbbbear/Jenkins-test.git')
                                
                                // 等待部署完成
                                def dc = openshift.selector("dc", "jenkins-test")
                                dc.rollout().status()
                                
                                // 創建路由
                                openshift.selector("svc", "jenkins-test").expose()
                            }
                        }
                    } catch (e) {
                        echo "部署過程中發生錯誤: ${e.getMessage()}"
                        error "部署失敗"
                    }
                }
            }
        }
    }
}