pipeline {
  agent any

    tools {
    nodejs 'Node_23'
    }

    environment {
    DOCKER_IMAGE_PREFIX = "ecom"
        VERSION = "v1.0.${BUILD_NUMBER}"
    }

    stages {
    stage('Prepare') {
      steps {
        echo "🔄 Code récupéré automatiquement si Git configuré"
      }
    }


        stage('Frontend Build') {
      steps {
        echo "🖌️ Building frontend Angular..."
                    sh '''
                        npm install
                        npm run build -- --configuration=development --no-watch --no-progress
                    '''
            }
        }

        stage('Docker Build') {
      steps {
        echo "🐳 Building Docker images version ${VERSION}..."
        		sh '''
        		  echo "Building frontend (Angular)..."
            	docker build -t $DOCKER_IMAGE_PREFIX-frontend:$VERSION .
        		'''
    		}
		}

    }

    post {
    always {
      echo '🎯 Pipeline terminé !'
        }
        failure {
      echo '💥 Échec du pipeline.'
        }
    }
}
