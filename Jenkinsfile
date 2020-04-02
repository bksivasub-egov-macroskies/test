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
      expression { BRANCH_NAME ==~ /[0-9]+\.[0-9]+\.x*/ }
          
        }
    steps{
    echo "You're in X.some branch"
  }
}
}}
