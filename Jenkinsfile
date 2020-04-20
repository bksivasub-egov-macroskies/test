def boolean hasChangesIn(String module) {
    if (env.CHANGE_TARGET == null) {
        return true;
    }

    def MASTER = sh(
        returnStdout: true,
        script: "git rev-parse origin/${env.CHANGE_TARGET}"
    ).trim()

    // Gets commit hash of HEAD commit. Jenkins will try to merge master into
    // HEAD before running checks. If this is a fast-forward merge, HEAD does
    // not change. If it is not a fast-forward merge, a new commit becomes HEAD
    // so we check for the non-master parent commit hash to get the original
    // HEAD. Jenkins does not save this hash in an environment variable.
    def HEAD = sh(
        returnStdout: true,
        script: "git show -s --no-abbrev-commit --pretty=format:%P%n%H%n HEAD | tr ' ' '\n' | grep -v ${MASTER} | head -n 1"
    ).trim()

    return sh(
        returnStatus: true,
        script: "git diff --name-only ${MASTER}...${HEAD} | grep ^${module}/"
    ) == 0
}

pipeline{
agent any
stages{
  stage('test'){
     steps{
        sh 'echo "Hello"'
}
}
  stage('branch'){
    when {
      expression {
      return hasChangesIn('my-dir')
//      expression { BRANCH_NAME ==~ /feature\/[0-9]+\.[0-9]+\.[0-9]+/ }
          
        }
    }
    steps{
    echo "You're in future branch"
  }
}
}}
