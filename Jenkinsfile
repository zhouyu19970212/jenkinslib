#! groovy

@Library('jenkinslib') _

def tools = new org.devops.tools()

String workspace = "/opt/jenkins/workspace"

//Pipeline
pipeline {
    agent { node {  label "built-in" //指定运行节点的标签或者名称
                    customWorkspace "${workspace}"
            }
    }
    
    options {
        timestamps() //日志会有时间
        skipDefaultCheckout() //删除隐式checkout scm语句
        disableConcurrentBuilds() //禁止并行
        timeout(time: 1, unit: "HOURS") //流水线超时设置1h
    }
    
    stages {
        // 下载代码
        stage("GetCode") { //阶段名称
            steps {
                timeout(time: 5, unit: "MINUTES") { //步骤超时时间
                    script {
                        println('获取代码')
                    }
                }
            }
        }
        
        // 构建
        stage("Build") {
            steps {
                timeout(time: 20, unit: "MINUTES") {
                    script {
                        println('应用打包')
                    }
                }
            }
        }
        
        // 代码扫描
        stage("CodeScan") {
            steps {
                timeout(time: 30, unit: "MINUTES") {
                    script {
                        println('代码扫描')
                        tools.PrintMes("This is my lib!")
                    }
                }
            }
        }
        
    }
    
    // 构建后操作
    post {
        always {
            script {
                println('always')
            }
        }
        
        success {
            script {
                currentBuild.description = "\n success!"
            }
        }
        
        failure {
            script {
                currentBuild.description = "\n fail!"
            }
        }
        
        aborted {
            script {
                currentBuild.description = "\n abort!"
            }
        }
    }
}
