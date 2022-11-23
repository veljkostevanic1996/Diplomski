
def prObject = ""
def repoObject = ""
def repoName = ""
def state = ""
//List<Map> parametersStatic = new ArrayList<Map>()

pipeline {
    agent any
    stages {
        stage("Initialize variables") {
            steps {
                script {
                    repoObject = readJSON text: "$repository"
                    repoName = repoObject.name
                    prObject = readJSON text: "$pull_request"
                    state = prObject.merged
                  
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
                
                println(prObject.merged)
                if (action == "closed" && prObject.merged){  
                    build job: "Pakrunner-build"
                }
              
            }
          }
        }
      
    }
}
