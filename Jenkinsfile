pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                // 您可以在這裡添加 Maven 或其他構建工具的命令
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                // 在這裡添加部署到 OpenShift 的命令，例如：
                sh 'oc apply -f ibus-super.yaml'
                sh 'oc apply -f ibus-super-svc.yaml'
                sh 'oc apply -f ibus-super-route.yaml'
                sh 'oc apply -f ingress.yaml'
            }
        }
    }
}