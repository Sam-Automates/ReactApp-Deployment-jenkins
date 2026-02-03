pipeline {
    agent any

    environment {
        BRANCH = "${env.GIT_BRANCH}".replace("origin/", "")
    }

    stages {

        // ============================
        // 🌍 ENVIRONMENT SELECTION
        // ============================
        stage('🌍 Select Environment') {
            steps {
                script {
                    if (BRANCH == 'main') {
                        echo "🚀 Production Deployment"
                        env.HOST    = credentials('PROD_HOST')
                        env.USER    = credentials('PROD_USER')
                        env.SSH_KEY = 'PROD_SSH_KEY'
                        env.APP_DIR = '/var/www/html/react-prod-app'
                    } else {
                        echo "🧪 Staging Deployment"
                        env.HOST    = credentials('STAGING_HOST')
                        env.USER    = credentials('STAGING_USER')
                        env.SSH_KEY = 'STAGING_SSH_KEY'
                        env.APP_DIR = '/var/www/html/react-staging-app'
                    }
                }
            }
        }

        // ============================
        // 🚀 DEPLOY APPLICATION
        // ============================
        stage('🚀 Deploy React App (Zero Downtime)') {
            steps {
                sshagent(credentials: [env.SSH_KEY]) {
                    sh """
                    set -e

                    ssh -o StrictHostKeyChecking=no ${USER}@${HOST} << 'EOF'
                      set -e

                      cd ${APP_DIR}

                      git config --global --add safe.directory ${APP_DIR}

                      if [ ! -d ".git" ]; then
                        git clone https://${GH_PAT}@github.com/${GH_USERNAME}/react-app.git .
                      fi

                      git fetch origin
                      git checkout -B ${BRANCH} origin/${BRANCH}
                      git reset --hard origin/${BRANCH}

                      npm install
                      npm run build

                      test -f dist/index.html

                      mv build build_old || true
                      mv dist build
                      rm -rf build_old

                      echo "🎉 Deployment successful"
                    EOF
                    """
                }
            }
        }
    }

    // ============================
    // 🧹 CLEAN JENKINS WORKSPACE
    // ============================
    post {
        always {
            echo "🧹 Cleaning Jenkins workspace"
            cleanWs()
        }

        success {
            echo "✅ Pipeline completed successfully 🚀"
        }

        failure {
            echo "❌ Pipeline failed — check logs 🔥"
        }
    }
}
