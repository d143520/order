//这个是一个申明式的，以pipeline开头 这个是jenkins2.0之后推荐的方式
pipeline {
    //代理，环境，工具等的配置
    agent any

    //阶段
    stages {
        stage('Hello') {
            //阶段中的步骤
            steps {
                //所有本阶段要做的步骤
                echo 'Hello World'
            }
        }

        stage('pull code') {
            //阶段中的步骤
            steps {
                echo 'pull code'

                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'ea01adcf-0f2c-4b38-9fe9-9f15c7ae862a', url: 'git@github.com:d143520/order.git']]])
            }
        }

        stage('build code') {
            steps {
                echo 'build code'

                sh 'mvn clean package'
            }
        }
        stage('publish code') {
            //阶段中的步骤
            steps {
                echo 'publish code'

                deploy adapters: [tomcat9(credentialsId: 'cb48045d-8796-49c1-86b1-5569ed6f886a', path: '', url: 'http://192.168.18.198:8090')], contextPath: '/myoder', war: 'target/*.war'

            }


        }

    }
}
