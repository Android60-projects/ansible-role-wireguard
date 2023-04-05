pipeline {
    agent {
        node {
            label 'molecule-virtualbox'
        }
    }
    options {
        skipStagesAfterUnstable()
    }
    environment {
        PATH = "$HOME/.local/bin:$PATH"
    }

    stages {
        stage('Test I') {
            parallel {
                stage('Test Ubuntu 20.04'){
                    agent { label 'molecule-virtualbox' }
                    steps {
                        catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                            retry(2) {
                                // retry code block
                                script {
                                    sh "MOLECULE_DISTRO=geerlingguy/ubuntu2004 molecule test --parallel"
                                }
                            }
                        }
                    }

                post {
                    success {
                        updateGitlabCommitStatus name: 'Test Ubuntu 20.04', state: 'success'
                    }
                    failure {
                        updateGitlabCommitStatus name: 'Test Ubuntu 20.04', state: 'failed'
                    }
                } 
                }
                stage('Test Rocky Linux 8'){
                    agent { label 'molecule-virtualbox' }
                    steps {
                        catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                            retry(2) {
                                // retry code block
                                script {
                                    sh "MOLECULE_DISTRO=geerlingguy/rockylinux8 molecule test --parallel"
                                }
                            }
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
        
        stage('Test II') {
            parallel {
                stage('Test Debian 11'){
                    agent { label 'molecule-virtualbox' }
                    steps {
                        catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                            retry(2) {
                                // retry code block
                                script {
                                    sh "MOLECULE_DISTRO=geerlingguy/debian11 molecule test --parallel"
                                }
                            }
                        }
                    }

                    post {
                        success {
                            updateGitlabCommitStatus name: 'Test Debian 11', state: 'success'
                        }
                        failure {
                            updateGitlabCommitStatus name: 'Test Debian 11', state: 'failed'
                        }
                    } 
                }
                stage('Test Ubuntu 18.04'){
                    agent { label 'molecule-virtualbox' }
                    steps {
                        catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                            retry(2) {
                                // retry code block
                                script {
                                    sh "MOLECULE_DISTRO=geerlingguy/ubuntu1804 molecule test --parallel"
                                }
                            }
                        }
                    }

                    post {
                        success {
                            updateGitlabCommitStatus name: 'Test Ubuntu 18.04', state: 'success'
                        }
                        failure {
                            updateGitlabCommitStatus name: 'Test Ubuntu 18.04', state: 'failed'
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

