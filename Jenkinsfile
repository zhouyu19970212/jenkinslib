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
                        tools.PrintMes("获取代码!",'red')
                        git branch: 'master', // 分支名  
                            url: 'https://github.com/zhouyu19970212/xxx.git' // 你的GitHub仓库URL  
                        // credentialsId: 'zhouyu19970212' // Jenkins中配置的GitHub凭据ID  
                        tools.PrintMes("获取成功!",'red')
                    }
                }
            }
        }
        
        // 构建
        stage("Build") {
            steps {
                timeout(time: 20, unit: "MINUTES") {
                    script {
                        tools.PrintMes("应用打包!",'blue')
                    }
                }
            }
        }
        
        // 代码扫描
        stage("CodeScan") {
            steps {
                timeout(time: 30, unit: "MINUTES") {
                    script {
                        tools.PrintMes("代码扫描!",'green')
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
