def dockerImage;

node('docker'){
	stage('SCM'){
		checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Tomassito/JenkinsDocker']]]);
	}
	stage('build'){
		dockerImage = docker.build('thewayedinburgh/agent-dnc:v' + env.BUILD_NUMBER, './dotnetcore');
	}
	stage('push'){
		docker.withRegistry('https://index.docker.io/v1/', 'dockerhubcreds'){
			dockerImage.push();
		}
	}
}
