
def prObject = ""
def repoObject = ""
def rcVersion = ""
def repoName = ""
//List<Map> parametersStatic = new ArrayList<Map>()

pipeline {
    agent any
    stages {
        stage("Initialize variables") {
            steps {
                script {
                    repoObject = readJSON text: "$repository"
                    repoName = repoObject.name
                    //rcVersion = ref
                    
                    if (repoName.contains("-")) {
                        repoName = repoName.replace("-", "_")
                    }
                    
                    repoName = repoName.toLowerCase()
                    currentBuild.displayName = "${BUILD_NUMBER}-repo-${repoName}"

                     
                }
            }
        } // end
        stage("Run static_code_analysis job") {
          steps {
            script {
                //parametersStatic.add([$class: 'StringParameterValue', name: 'REPO', value: repoName])
                //parametersStatic.add([$class: 'StringParameterValue', name: 'BRANCH', value: "master"])
                //parametersStatic.add([$class: 'StringParameterValue', name: 'VERSION', value: rcVersion])

                build job: test
              
            }
          }
        }
      
    }
}
