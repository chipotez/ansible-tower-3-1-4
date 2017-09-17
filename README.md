### Deploy Ansible Tower 3.1.4-1

Para poder realizar exitosamente el deploy mediante el playbook es necesario tomar las siguientes consideraciones:

1 .- Se asume que cuenta con el fingerprint del servidor remoto, caso contrario edite la variable en el siguiente archivo:

     /etc/ansible/ansible.cfg
     [defaults]
     host_key_checking = False
2 .- Se asume que cuenta con autenticación SSH basada en keys, caso contrario puede usar las opciones de conexión:

    - --ask-pass
3 .- Modifique las variables acorde a sus necesidades dentro del playbook:
                
    - tower_admin_pass: password
    - rhn_username: tu-user
    - rhn_pass: tu-password
    - hostname_full: hostname-full (identificador en RHN)

*Ejemplos de ejecución:

### Con Fingerprint y Keys:

    $ ansible-playbook deploy.yml
    
### Con Variables :
    
    $ export ANSIBLE_HOST_KEY_CHECKING=False
    $ ansible-playbook deploy.yml --ask-pass --extra-vars "tower_admin_pass: password rhn_username=tu-user rhn_pass=tu-password hostname_full: hostname-full"
