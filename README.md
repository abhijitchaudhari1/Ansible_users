# ADD bulk users to linux machines

1. Update hosts file with your servers something like this 

     prod-app-1 ansible_ssh_host=192.168.1.2 ansible_ssh_user=ubuntu ansible_ssh_key=/<PATH_TO_SSH_KEY>/
     prod-app-2 ansible_ssh_host=192.168.1.3 ansible_ssh_user=ubuntu ansible_ssh_key=/<PATH_TO_SSH_KEY>/
     
  NOTE: If the private key has passphrase, then in order to use it with ansible you have to add that key to ssh-agent
        to do that on any linux machines, from which you are going to run the ansible, follow the steps metioned below
        
        1. $ eval `ssh-agent`
        2. $ ssh-add SSH_PRIVATE_KEY_PATH
        
        
2. Update the vari.yml file according to your requirement.
              
    **groups** can comma seperated list of groups for the user    
    **key**  will add public key mentioned { here  "/Users/abhijit/local_conf/abhi.pub" } to user's authorized_keys file without affecting current contents.    
    **sudo_access**  defines the sudo access the user will have after its creation  
    
    **NOTE**  If you do not want to set any of the above variable like groups, keys leave it blank
    
    
This playbook assumes that to get root access on remote machine, sudo is used. 

In a scinario where  it requires **su** to get root access, please change **become_method** from sudo to **su** 


TO run this playbook against your infra, 

    ansible-playbook -i hosts site.yml -e @vari.yml --ask-become-pass
    
    
    
