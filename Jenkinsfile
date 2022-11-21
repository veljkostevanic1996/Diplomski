
def prObject = ""
def repoObject = ""
def rcVersion = ""
def repoName = ""


pipeline {
    agent any
    stages {
        stage("Initialize variables") {
            steps {
                script {
                    repoObject = readJSON text: "$repository"
                    repoName = repoObject.name
                    rcVersion = ref
                    
                    if (repoName.contains("-")) {
                        repoName = repoName.replace("-", "_")
                    }
                    
                    repoName = repoName.toLowerCase()
                    currentBuild.displayName = "${BUILD_NUMBER}-repo-${repoName}-rc-${rcVersion}"

                     
                }
            }
        } // end
        stage("Run static_code_analysis job") {
          steps {
            script {
                parametersStatic.add([$class: 'StringParameterValue', name: 'REPO', value: repoName])
                parametersStatic.add([$class: 'StringParameterValue', name: 'BRANCH', value: "master"])
                parametersStatic.add([$class: 'StringParameterValue', name: 'VERSION', value: rcVersion])

                build job: test
              
            }
          }
        }
      
    }
}
