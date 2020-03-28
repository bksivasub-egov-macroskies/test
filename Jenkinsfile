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
      expression { BRANCH_NAME ==~ /feature\/[0-9]+\.[0-9]+\.[0-9]+/ }
          
        }
    steps{
    echo "You're in future branch"
  }
}
}}
