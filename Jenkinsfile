pipeline {
    agent any
    
    triggers {
        pollSCM('* * * * *') // Her 1 dakikada bir GitHub deposunu kontrol et
    }
    
    stages {
        stage('Clone repository') {
            steps {
                git 'https://github.com/ErginTIRAVOGLU/JenkinsTestMvc.git'
            }
        }
        stage('Build') {
            steps {
                sh 'dotnet build'
            }
        }
        stage('Test') {
            steps {
                sh 'dotnet test'
            }
        }
        stage('Publish') {
            steps {
                sh 'dotnet publish -c Release -o ./publish'
            }
        }
        stage('Deploy to IIS') {
            steps {
                // Belirli bir IIS websitesini durdurma
                bat 'appcmd stop site /site.name:"YourWebsiteName"'
                
                // Dosyaları yayınlama
                bat 'xcopy /s/y ./publish/* C:\\inetpub\\wwwroot\\yayinlananProje'
                
                // IIS websitesini yeniden başlatma
                bat 'appcmd start site /site.name:"YourWebsiteName"'
            }
        }
    }
    
    post {
        success {
            echo 'Proje başarıyla derlendi, test edildi ve IIS üzerinde yayınlandı!'
        }
        failure {
            echo 'Proje derlenirken hata oluştu veya testler başarısız oldu.'
        }
    }
}