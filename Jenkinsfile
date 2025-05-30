pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/PrathushaK10/8.2CDevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        bat 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        bat 'cmd /c "npm test || exit /b 0"'
      }
    }

    stage('NPM Audit') {
      steps {
        bat 'cmd /c "npm audit || exit /b 0"'
      }
    }
  }

  post {
    always {
      emailext (
        subject: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
        body: """
          <h3>Build Summary</h3>
          <ul>
            <li><b>Project:</b> ${env.JOB_NAME}</li>
            <li><b>Build Number:</b> ${env.BUILD_NUMBER}</li>
            <li><b>Status:</b> ${currentBuild.result}</li>
            <li><b>Console Output:</b> <a href="${env.BUILD_URL}console">${env.BUILD_URL}console</a></li>
          </ul>
        """,
        mimeType: 'text/html',
        to: 'prathushakarade2001@gmail.com',
        attachLog: true
      )
    }
  }
}
