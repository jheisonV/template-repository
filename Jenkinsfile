pipeline {
    agent any

    stages {
        stage('Create Repository') {
            steps {
                script {
                    def repoName = 'nombre_del_repositorio'
                    def repoDescription = 'descripción_del_repositorio'
                    def githubCredentials = 'github-credentials' // Nombre de las credenciales configuradas en Jenkins para acceder a GitHub

                    // Clonar el repositorio Jenkinsfile desde el repositorio de plantilla
                    git 'https://github.com/tu_usuario/template-repo.git'

                    // Autenticación con GitHub
                    withCredentials([usernamePassword(credentialsId: githubCredentials, usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh 'curl -u $USERNAME:$PASSWORD -X POST https://api.github.com/user/repos -d \'{"name": "' + repoName + '", "description": "' + repoDescription + '"}\''
                    }
                }
            }
        }

        stage('Set Branch Protection') {
            steps {
                script {
                    def githubCredentials = 'github-credentials' // Nombre de las credenciales configuradas en Jenkins para acceder a GitHub

                    // Autenticación con GitHub
                    withCredentials([usernamePassword(credentialsId: githubCredentials, usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh 'curl -u $USERNAME:$PASSWORD -X PUT https://api.github.com/repos/tu_usuario/nombre_del_repositorio/branches/main/protection -d \'{"required_status_checks": {"strict": true, "contexts": ["continuous-integration"]}, "enforce_admins": true, "required_pull_request_reviews": {"dismissal_restrictions": {"users": ["usuario1", "usuario2"], "teams": ["equipo1"]}, "dismiss_stale_reviews": true, "require_code_owner_reviews": true, "required_approving_review_count": 2}, "restrictions": null}\''
                    }
                }
            }
        }
    }
}
