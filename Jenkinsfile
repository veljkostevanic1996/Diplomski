
def prObject = ""
def repoObject = ""
def repoName = ""

pipeline {
    agent any
    stages {
        stage("Initialize variables") {
            steps {
                script {
                    repoObject = readJSON text: "$repository"
                    repoName = repoObject.name
                    prObject = readJSON text: "$pull_request"
                  
                    repoName = repoName.toLowerCase()
                    currentBuild.displayName = "${BUILD_NUMBER}-repo-${repoName}"

                     
                }
            }
        } 
        stage("Run static_code_analysis job") {
          steps {
            script {

                println("PR: \naction -> $action \nmerged -> $prObject.merged")
                if (action == "closed" && prObject.merged){  
                    build job: "Pakrunner-build"
                }
              
            }
          }
        }
      
    }
}
