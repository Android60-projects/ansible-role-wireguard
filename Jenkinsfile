pipeline {
    agent {
        node {
            label 'molecule-test'
        }
    }
    options {
        skipStagesAfterUnstable()
    }
    environment {
        PATH = "$HOME/.local/bin:$PATH"
    }

    stages {
        stage('Test RedHat-like') {
            parallel {
                stage('Test CentOS 8'){
                    agent { label 'molecule-test' }
                    steps {
                        script {
                            sh "MOLECULE_DISTRO=centos8 molecule test --parallel"
                        }
                    }

                post {
                    success {
                        updateGitlabCommitStatus name: 'Test CentOS 8', state: 'success'
                    }
                    failure {
                        updateGitlabCommitStatus name: 'Test CentOS 8', state: 'failed'
                    }
                } 
                }
                stage('Test Rocky Linux 8'){
                    agent { label 'molecule-test' }
                    steps {
                        script {
                            sh "MOLECULE_DISTRO=rockylinux8 molecule test --parallel"
                        }
                    }

                    post {
                        success {
                            updateGitlabCommitStatus name: 'Test Rocky Linux 8', state: 'success'
                        }
                        failure {
                            updateGitlabCommitStatus name: 'Test Rocky Linux 8', state: 'failed'
                        }
                    } 
                }
            }
        }
        
        stage('Test Debian-like') {
            parallel {
                stage('Test Debian 10'){
                    agent { label 'molecule-test' }
                    steps {
                        script {
                            sh "MOLECULE_DISTRO=debian10 molecule test --parallel"
                        }
                    }

                    post {
                        success {
                            updateGitlabCommitStatus name: 'Test Debian 10', state: 'success'
                        }
                        failure {
                            updateGitlabCommitStatus name: 'Test Debian 10', state: 'failed'
                        }
                    } 
                }
                stage('Test Ubuntu 22.04'){
                    agent { label 'molecule-test' }
                    steps {
                        script {
                            sh "MOLECULE_DISTRO=ubuntu2204 molecule test --parallel"
                        }
                    }

                    post {
                        success {
                            updateGitlabCommitStatus name: 'Test Ubuntu 22.04', state: 'success'
                        }
                        failure {
                            updateGitlabCommitStatus name: 'Test Ubuntu 22.04', state: 'failed'
                        }
                    }
                }
            }
        }
    }
        
    post {
        success {
            updateGitlabCommitStatus name: 'Pipeline', state: 'success'
        }
        failure {
            updateGitlabCommitStatus name: 'Pipeline', state: 'failed'
        }
    } 
 }

