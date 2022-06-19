node{
    def maven_Home=tool  name:'maven'
    stage ('Pull from Github'){
        git branch: 'main', credentialsId: 'githubID', url: ''
        git credentialsId: 'githubID', url: ''
    }
    
    stage ('Build'){
        sh " '${maven_Home}/bin/mvn' clean install package"
    }

    // stage ('Deploy to Container'){
        deploy adapters: [tomcat8(credentialsId: 'TOMCAT', path: '', url: 'http://52.90.127.229:8080/')], contextPath: null, war: '**/*.war'
     }
    
    stage ('Docker Build'){
        sh " docker build -t tawfiq15/aws:${BUILD_NUMBER} . "
        sh " docker images "
        sh " bash /var/lib/jenkins/bb.sh "
    }

    stage ('Docker Login'){
        sh "cat /var/lib/jenkins/dockker.txt > /var/lib/jenkins/.docker/config.json "
                   
        }
        
    }

    stage ( 'Docker push'){
        sh "docker push tawfiq15/aws:${BUILD_NUMBER}"
        
    }
    stage ('Docker image Remove'){
        sh " bash /var/lib/jenkins/bassh.sh"
    }
    
}
