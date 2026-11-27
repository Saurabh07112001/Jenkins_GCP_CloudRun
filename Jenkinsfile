pipeline {
    agent any
    tools {
	jdk 'jdk21'
	maven 'maven387'
    }
    environment {
	IMAGE_NAME = "java-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
	GCP_PROJECT_ID = "focal-dock-440200-u5"
	FULL_IMAGE_NAME = "us-docker.pkg.dev/${GCP_PROJECT_ID}/java-app-repo-02/${IMAGE_NAME}:${IMAGE_TAG}"
	SERVICE_NAME = "java-app-service"
	REGION = "us-central1"
    }
    stages {
        stage('Initialize Pipeline'){
            steps {
                echo 'Initializing Pipeline ...'
		sh 'java -version'
		sh 'mvn -version'
		echo 'Initializing Pipeline ...'
        sh 'echo "JAVA_HOME=$JAVA_HOME"'
        sh 'echo "PATH=$PATH"'
        sh 'ls -l $JAVA_HOME/bin/java || echo "java NOT FOUND at JAVA_HOME"'
        sh 'java -version'
        sh 'mvn -version'
            }
        }
        stage('Checkout GitHub Codes'){
            steps {
                echo 'Checking out GitHub Codes ...'
		        checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'jenkins-gcp-cloudrun', url: 'https://github.com/Saurabh07112001/Jenkins_GCP_CloudRun.git']])
            }
        }
        stage('Maven Build'){
            steps {
                echo 'Building Java App with Maven'
            }
        }
        stage('JUnit Test of Java App'){
            steps {
                echo 'JUnit Testing'
            }
        }
        stage('SonarQube Analysis'){
            steps {
                echo 'Running Static Code Analysis with SonarQube'
            }
        }
        stage('Trivy FS Scan'){
            steps {
                echo 'Scanning File System with Trivy FS ...'
            }
        }
        stage('Build & Tag Docker Image'){
            steps {
                echo 'Building the Java App Docker Image'
            }
        }
        stage('Trivy Security Scan'){
            steps {
                echo 'Scanning Docker Image with Trivy'
            }
        }
	stage('Authenticate with GCP, Tag & Push to Artifact Registry') {
            steps {
		echo 'Authenticate with GCP, tag and Push Image to Artifact Registry'
            }
        }
	stage('Deploy to Cloud Run') {
		steps {
			echo 'Deploying Image to Google Cloud Run'
				}
			}
	stage('Get Cloud Run Service URL') {
            steps {
			echo 'Getting Cloud Run Service URL'
            		}
       	 	}
	}
}
