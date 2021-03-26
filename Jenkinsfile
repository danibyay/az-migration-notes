pipeline {
    environment {
        ARM_SUBSCRIPTION_ID = ""
        ARM_TENANT_ID = ""
        ARM_CLIENT_ID = ""
        ARM_CLIENT_SECRET = credentials('tf_client_secret')
        TF_VAR_password_external_pfx = credentials('tf_int_pw')
        TF_VAR_qa_password_external_pfx = credentials('tf_qa_pw')
        VAULT_PASS_INT = credentials('vault-pass-int')
        VAULT_PASS_QA = credentials('vault-pass-qa')
        PEM_FILE = credentials('private_ssh_key')
    }
    agent any
    stages {
        stage ('init') {
    steps {  
        sh '''
                terraform init
                '''      
    }
}
        stage ('validate and fmt') {
            steps {
                sh '''
                terraform validate
                terraform fmt
                '''
            }
        }
        /*stage ('ensure clone repos') {
            steps {
                sh '''
                terraform taint null_resource.clone_repos
                '''
            }
        }*/
        stage ('plan') {
            steps {
                sh '''
                terraform plan -no-color
                '''
            }
        }
        stage ('apply') {
            steps {
                sh '''
                terraform apply -auto-approve
                '''
            }
        }
        stage ('ansible') {
            steps {
 
                sh '''
                echo "hello"
                #ansible-playbook -e "TARGET_HOST=$HOST" --vault-password-file $VAULT_PASS_INT -e @roles/int-inventory/host_vars/$HOST.net.yml ansible_templates/publisher-install.yml --private-key $PEM_FILE
                #ansible-playbook -e "TARGET_HOST=$HOST" --vault-password-file $VAULT_PASS_INT -e @roles/int-inventory/host_vars/$HOST.net.yml ansible_templates/publisher-ssl.yml --private-key $PEM_FILE
                #ansible-playbook -e "TARGET_HOST=$HOST" --vault-password-file $VAULT_PASS_INT -e @roles/int-inventory/host_vars/$HOST.net.yml ansible_templates/dispatcher-install.yml --private-key $PEM_FILE
                '''
            }
        }
 
    }
 
}
