## Conexión al servidor remoto:
    
    empi  ~  ssh -l root -o ServerAliveInterval=30 35.196.111.132
    The authenticity of host '35.196.111.132 (35.196.111.132)' can't be established.
    ECDSA key fingerprint is SHA256:LfUxCe2zUvXOI1cYBKKsYs1zBiEVrs0RBkBOtyXnnxk.
    ECDSA key fingerprint is MD5:5c:5d:4d:d6:24:a2:36:55:c9:29:af:2c:4e:f0:b8:6b.
    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added '35.196.111.132' (ECDSA) to the list of known hosts.
    root@35.196.111.132's password: 
    Last login: Fri Jul 28 18:32:43 2017

### Registrando el equipo al Portal Red Hat
    [root@tower ~]# subscription-manager register --username='tu-user' --password='tu-password' 
    Registering to: subscription.rhsm.redhat.com:443/subscription
    The system has been registered with ID: cf0be4f5-f7a2-4f8d-b762-452bc63e1d86 

### Asignando pool de suscripciones

    [root@tower ~]# subscription-manager attach --pool=8a85f9815dbd9297015dbdb8186b428d
    Esta unidad ya tiene ID de grupo correspondiente a la suscripción '8a85f9815dbd9297015dbdb8186b428d'.


## Deshabilitando repositorios innecesarios

    [root@tower ~]# subscription-manager repos --disable="*"
    Repository 'rhel-7-server-openstack-11-devtools-debug-rpms' is disabled for this system.
    Repository 'rhel-7-server-v2vwin-1-debug-rpms' is disabled for this system.
    Repository 'rhel-7-server-openstack-7.0-tools-source-rpms' is disabled for this system.
    ( ... )

## Habilitando repositorios necesarios.
    [root@tower ~]# subscription-manager repos --enable="rhel-7-server-rpms"  --enable="rhel-7-server-extras-rpms" --enable="rhel-7-server-optional-rpms"
    Repository 'rhel-7-server-rpms' is enabled for this system.
    Repository 'rhel-7-server-optional-rpms' is enabled for this system.
    Repository 'rhel-7-server-extras-rpms' is enabled for this system.

## Actualizando Sistemas
    [root@tower ~]# yum update -y
    Complementos cargados:product-id, search-disabled-repos, subscription-manager
    rhel-7-server-extras-rpms                                                                                                                                                                   | 3.4 kB  00:00:00     
    rhel-7-server-optional-rpms                                                                                                                                                                 | 3.5 kB  00:00:00     
    rhel-7-server-rpms                                                                                                                                                                          | 3.5 kB  00:00:00     
    (1/9): rhel-7-server-extras-rpms/x86_64/updateinfo                                                                                                                                          | 191 kB  00:00:00     
    (2/9): rhel-7-server-extras-rpms/x86_64/group                                                                                                                                               |  104 B  00:00:00     
    (3/9): rhel-7-server-extras-rpms/x86_64/primary_db                                                                                                                                          | 277 kB  00:00:00     
    (4/9): rhel-7-server-optional-rpms/7Server/x86_64/updateinfo                                                                                                                                | 1.7 MB  00:00:00     
    (5/9): rhel-7-server-optional-rpms/7Server/x86_64/group                                                                                                                                     |  24 kB  00:00:00     
    (6/9): rhel-7-server-rpms/7Server/x86_64/group                                                                                                                                              | 709 kB  00:00:00     
    (7/9): rhel-7-server-optional-rpms/7Server/x86_64/primary_db                                                                                                                                | 5.9 MB  00:00:00     
    (8/9): rhel-7-server-rpms/7Server/x86_64/updateinfo                                                                                                                                         | 2.3 MB  00:00:00     
    (9/9): rhel-7-server-rpms/7Server/x86_64/primary_db                                                                                                                                         |  42 MB  00:00:01     

    Resolviendo dependencias
    --> Ejecutando prueba de transacción
    ---> Paquete NetworkManager.x86_64 1:1.4.0-12.el7 debe ser obsoleto
    ---> Paquete NetworkManager.x86_64 1:1.8.0-9.el7 debe ser obsoleto
    ( ... )
    --> Ejecutando prueba de transacción
    ---> Paquete libcap-ng.i686 0:0.7.5-4.el7 debe ser instalado
    ---> Paquete libstdc++.i686 0:4.8.5-16.el7 debe ser instalado
    --> Resolución de dependencias finalizada

    Dependencias resueltas

    Resumen de la transacción
    ===================================================================================================================================================================================================================
    Instalar     11 Paquetes (+30 Paquetes dependientes)
    Actualizar  198 Paquetes

    Tamaño total de la descarga: 214 M
    Downloading packages:                                                                                                                                    | 242 kB  00:00:00     
    ...                                                                                                                                                    | 109 kB  00:00:00     
    (237/239): yum-3.4.3-154.el7.noarch.rpm                                                                                                                                                     | 1.2 MB  00:00:00     
    (238/239): yum-rhn-plugin-2.0.1-9.el7.noarch.rpm                                                                                                                                            |  81 kB  00:00:00     
    (239/239): zlib-1.2.7-17.el7.i686.rpm                                                                                                                                                       |  91 kB  00:00:00     
    -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    Total                                                                                                                                                                              5.1 MB/s | 214 MB  00:00:42     

    Sustituido(s):
      NetworkManager.x86_64 1:1.4.0-12.el7        grub2.x86_64 1:2.02-0.44.el7        grub2-tools.x86_64 1:2.02-0.44.el7        pygobject3-base.x86_64 0:3.14.0-3.el7        rdma.noarch 0:7.3_4.7_rc2-5.el7       

    ¡Listo!
## Desempaquetando Tower

    [root@tower ansible-tower]# tar xvfz ansible-tower-setup-latest.tar.gz 
    ansible-tower-setup-3.1.4/
    ansible-tower-setup-3.1.4/restore.yml
    ansible-tower-setup-3.1.4/roles/

    ( ... )

    ansible-tower-setup-3.1.4/licenses/redis.txt
    ansible-tower-setup-3.1.4/README.md
    ansible-tower-setup-3.1.4/inventory
    ansible-tower-setup-3.1.4/backup.yml
    
## Ejecutando Instalador

    [root@tower ansible-tower-setup-3.1.4]# ./setup.sh 
    Complementos cargados:product-id, search-disabled-repos, subscription-manager
    epel-release-latest-7.noarch.rpm                                                                                                                                                            |  14 kB  00:00:00     
    Examinando /var/tmp/yum-root-mwNkNi/epel-release-latest-7.noarch.rpm: epel-release-7-10.noarch
    Marcando /var/tmp/yum-root-mwNkNi/epel-release-latest-7.noarch.rpm para ser instalado
    Resolviendo dependencias
    --> Ejecutando prueba de transacción
    ---> Paquete epel-release.noarch 0:7-10 debe ser instalado
    --> Resolución de dependencias finalizada

    Dependencias resueltasRUNNING HANDLER [supervisor : Stop supervisor.] *******************************************************************************************************************************************************************
    changed: [localhost] => {"changed": true, "name": "supervisord", "state": "stopped", "status": {"ActiveEnterTimestamp": "vie 2017-08-25 18:12:18 CDT", "ActiveEnterTimestampMonotonic": "2370907543", "ActiveExitTimestampMonotonic": "0", "ActiveState": "active", "After": "rc-local.service systemd-journald.socket basic.target system.slice", "AllowIsolate": "no", "AmbientCapabilities": "0", "AssertResult": "yes", "AssertTimestamp": "vie 2017-08-25 18:12:18 CDT", "AssertTimestampMonotonic": "2370808205", "Before": "multi-user.target shutdown.target", "BlockIOAccounting": "no", "BlockIOWeight": "18446744073709551615", "CPUAccounting": "no", "CPUQuotaPerSecUSec": "infinity", "CPUSchedulingPolicy": "0", "CPUSchedulingPriority": "0", "CPUSchedulingResetOnFork": "no", "CPUShares": "18446744073709551615", "CanIsolate": "no", "CanReload": "no", "CanStart": "yes", "CanStop": "yes", "CapabilityBoundingSet": "18446744073709551615", "ConditionResult": "yes", "ConditionTimestamp": "vie 2017-08-25 18:12:18 CDT", "ConditionTimestampMonotonic": "2370808205", "Conflicts": "shutdown.target", "ControlGroup": "/system.slice/supervisord.service", "ControlPID": "0", "DefaultDependencies": "yes", "Delegate": "no", "Description": "Process Monitoring and Control Daemon", "DevicePolicy": "auto", "ExecMainCode": "0", "ExecMainExitTimestampMonotonic": "0", "ExecMainPID": "31604", "ExecMainStartTimestamp": "vie 2017-08-25 18:12:18 CDT", "ExecMainStartTimestampMonotonic": "2370907510", "ExecMainStatus": "0", "ExecStart": "{ path=/usr/bin/supervisord ; argv[]=/usr/bin/supervisord -c /etc/supervisord.conf ; ignore_errors=no ; start_time=[n/a] ; stop_time=[n/a] ; pid=0 ; code=(null) ; status=0/0 }", "FailureAction": "none", "FileDescriptorStoreMax": "0", "FragmentPath": "/usr/lib/systemd/system/supervisord.service", "GuessMainPID": "yes", "IOScheduling": "0", "Id": "supervisord.service", "IgnoreOnIsolate": "no", "IgnoreOnSnapshot": "no", "IgnoreSIGPIPE": "yes", "InactiveEnterTimestampMonotonic": "0", "InactiveExitTimestamp": "vie 2017-08-25 18:12:18 CDT", "InactiveExitTimestampMonotonic": "2370808648", "JobTimeoutAction": "none", "JobTimeoutUSec": "0", "KillMode": "control-group", "KillSignal": "15", "LimitAS": "18446744073709551615", "LimitCORE": "18446744073709551615", "LimitCPU": "18446744073709551615", "LimitDATA": "18446744073709551615", "LimitFSIZE": "18446744073709551615", "LimitLOCKS": "18446744073709551615", "LimitMEMLOCK": "65536", "LimitMSGQUEUE": "819200", "LimitNICE": "0", "LimitNOFILE": "4096", "LimitNPROC": "14715", "LimitRSS": "18446744073709551615", "LimitRTPRIO": "0", "LimitRTTIME": "18446744073709551615", "LimitSIGPENDING": "14715", "LimitSTACK": "18446744073709551615", "LoadState": "loaded", "MainPID": "31604", "MemoryAccounting": "no", "MemoryCurrent": "18446744073709551615", "MemoryLimit": "18446744073709551615", "MountFlags": "0", "Names": "supervisord.service", "NeedDaemonReload": "no", "Nice": "0", "NoNewPrivileges": "no", "NonBlocking": "no", "NotifyAccess": "none", "OOMScoreAdjust": "0", "OnFailureJobMode": "replace", "PermissionsStartOnly": "no", "PrivateDevices": "no", "PrivateNetwork": "no", "PrivateTmp": "no", "ProtectHome": "no", "ProtectSystem": "no", "RefuseManualStart": "no", "RefuseManualStop": "no", "RemainAfterExit": "no", "Requires": "basic.target", "Restart": "no", "RestartUSec": "100ms", "Result": "success", "RootDirectoryStartOnly": "no", "RuntimeDirectoryMode": "0755", "SameProcessGroup": "no", "SecureBits": "0", "SendSIGHUP": "no", "SendSIGKILL": "yes", "Slice": "system.slice", "StandardError": "inherit", "StandardInput": "null", "StandardOutput": "journal", "StartLimitAction": "none", "StartLimitBurst": "5", "StartLimitInterval": "10000000", "StartupBlockIOWeight": "18446744073709551615", "StartupCPUShares": "18446744073709551615", "StatusErrno": "0", "StopWhenUnneeded": "no", "SubState": "running", "SyslogLevelPrefix": "yes", "SyslogPriority": "30", "SystemCallErrorNumber": "0", "TTYReset": "no", "TTYVHangup": "no", "TTYVTDisallocate": "no", "TasksAccounting": "no", "TasksCurrent": "18446744073709551615", "TasksMax": "18446744073709551615", "TimeoutStartUSec": "1min 30s", "TimeoutStopUSec": "1min 30s", "TimerSlackNSec": "50000", "Transient": "no", "Type": "forking", "UMask": "0022", "UnitFilePreset": "disabled", "UnitFileState": "enabled", "WantedBy": "multi-user.target", "Wants": "system.slice", "WatchdogTimestamp": "vie 2017-08-25 18:12:18 CDT", "WatchdogTimestampMonotonic": "2370907525", "WatchdogUSec": "0"}}

    RUNNING HANDLER [supervisor : Wait for supervisor to stop.] *******************************************************************************************************************************************************
    ok: [localhost] => {"attempts": 1, "changed": false, "stat": {"exists": false}}

    ( ... ) 

    RUNNING HANDLER [supervisor : Start supervisor.] ******************************************************************************************************************************************************************
    changed: [localhost] => {"changed": true, "nhttps://www.google.com.mx/search?q=estilos+ehttps://www.google.com.mx/search?q=estilos+ehttps://www.google.com.mx/search?q=estilos+ehttps://www.google.com.mx/search?q=estilos+ehttps://www.google.com.mx/search?q=estilos+en+git&ie=utf-8&oe=utf-8&client=firefox-b&gfe_rd=cr&ei=qrWgWaWWM6z-8Ae42LDQDgn+git&ie=utf-8&oe=utf-8&client=firefox-b&gfe_rd=cr&ei=qrWgWaWWM6z-8Ae42LDQDgn+git&ie=utf-8&oe=utf-8&client=firefox-b&gfe_rd=cr&ei=qrWgWaWWM6z-8Ae42LDQDgn+git&ie=utf-8&oe=utf-8&client=firefox-b&gfe_rd=cr&ei=qrWgWaWWM6z-8Ae42LDQDgn+git&ie=utf-8&oe=utf-8&client=firefox-b&gfe_rd=cr&ei=qrWgWaWWM6z-8Ae42LDQDgame": "supervisord", "state": "started", "status": {"ActiveEnterTimestamp": "vie 2017-08-25 18:12:18 CDT", "ActiveEnterTimestampMonotonic": "2370907543", "ActiveExitTimestamp": "vie 2017-08-25 18:13:06 CDT", "ActiveExitTimestampMonotonic": "2418101033", "ActiveState": "inactive", "After": "rc-local.service systemd-journald.socket basic.target system.slice", "AllowIsolate": "no", "AmbientCapabilities": "0", "AssertResult": "yes", "AssertTimestamp": "vie 2017-08-25 18:12:18 CDT", "AssertTimestampMonotonic": "2370808205", "Before": "multi-user.target shutdown.target", "BlockIOAccounting": "no", "BlockIOWeight": "18446744073709551615", "CPUAccounting": "no", "CPUQuotaPerSecUSec": "infinity", "CPUSchedulingPolicy": "0", "CPUSchedulingPriority": "0", "CPUSchedulingResetOnFork": "no", "CPUShares": "18446744073709551615", "CanIsolate": "no", "CanReload": "no", "CanStart": "yes", "CanStop": "yes", "CapabilityBoundingSet": "18446744073709551615", "ConditionResult": "yes", "ConditionTimestamp": "vie 2017-08-25 18:12:18 CDT", "ConditionTimestampMonotonic": "2370808205", "Conflicts": "shutdown.target", "ControlPID": "0", "DefaultDependencies": "yes", "Delegate": "no", "Description": "Process Monitoring and Control Daemon", "DevicePolicy": "auto", "ExecMainCode": "1", "ExecMainExitTimestamp": "vie 2017-08-25 18:13:11 CDT", "ExecMainExitTimestampMonotonic": "2423909893", "ExecMainPID": "31604", "ExecMainStartTimestamp": "vie 2017-08-25 18:12:18 CDT", "ExecMainStartTimestampMonotonic": "2370907510", "ExecMainStatus": "0", "ExecStart": "{ path=/usr/bin/supervisord ; argv[]=/usr/bin/supervisord -c /etc/supervisord.conf ; ignore_errors=no ; start_time=[n/a] ; stop_time=[n/a] ; pid=0 ; code=(null) ; status=0/0 }", "FailureAction": "none", "FileDescriptorStoreMax": "0", "FragmentPath": "/usr/lib/systemd/system/supervisord.service", "GuessMainPID": "yes", "IOScheduling": "0", "Id": "supervisord.service", "IgnoreOnIsolate": "no", "IgnoreOnSnapshot": "no", "IgnoreSIGPIPE": "yes", "InactiveEnterTimestamp": "vie 2017-08-25 18:13:11 CDT", "InactiveEnterTimestampMonotonic": "2423910000", "InactiveExitTimestamp": "vie 2017-08-25 18:12:18 CDT", "InactiveExitTimestampMonotonic": "2370808648", "JobTimeoutAction": "none", "JobTimeoutUSec": "0", "KillMode": "control-group", "KillSignal": "15", "LimitAS": "18446744073709551615", "LimitCORE": "18446744073709551615", "LimitCPU": "18446744073709551615", "LimitDATA": "18446744073709551615", "LimitFSIZE": "18446744073709551615", "LimitLOCKS": "18446744073709551615", "LimitMEMLOCK": "65536", "LimitMSGQUEUE": "819200", "LimitNICE": "0", "LimitNOFILE": "4096", "LimitNPROC": "14715", "LimitRSS": "18446744073709551615", "LimitRTPRIO": "0", "LimitRTTIME": "18446744073709551615", "LimitSIGPENDING": "14715", "LimitSTACK": "18446744073709551615", "LoadState": "loaded", "MainPID": "0", "MemoryAccounting": "no", "MemoryCurrent": "18446744073709551615", "MemoryLimit": "18446744073709551615", "MountFlags": "0", "Names": "supervisord.service", "NeedDaemonReload": "no", "Nice": "0", "NoNewPrivileges": "no", "NonBlocking": "no", "NotifyAccess": "none", "OOMScoreAdjust": "0", "OnFailureJobMode": "replace", "PermissionsStartOnly": "no", "PrivateDevices": "no", "PrivateNetwork": "no", "PrivateTmp": "no", "ProtectHome": "no", "ProtectSystem": "no", "RefuseManualStart": "no", "RefuseManualStop": "no", "RemainAfterExit": "no", "Requires": "basic.target", "Restart": "no", "RestartUSec": "100ms", "Result": "success", "RootDirectoryStartOnly": "no", "RuntimeDirectoryMode": "0755", "SameProcessGroup": "no", "SecureBits": "0", "SendSIGHUP": "no", "SendSIGKILL": "yes", "Slice": "system.slice", "StandardError": "inherit", "StandardInput": "null", "StandardOutput": "journal", "StartLimitAction": "none", "StartLimitBurst": "5", "StartLimitInterval": "10000000", "StartupBlockIOWeight": "18446744073709551615", "StartupCPUShares": "18446744073709551615", "StatusErrno": "0", "StopWhenUnneeded": "no", "SubState": "dead", "SyslogLevelPrefix": "yes", "SyslogPriority": "30", "SystemCallErrorNumber": "0", "TTYReset": "no", "TTYVHangup": "no", "TTYVTDisallocate": "no", "TasksAccounting": "no", "TasksCurrent": "18446744073709551615", "TasksMax": "18446744073709551615", "TimeoutStartUSec": "1min 30s", "TimeoutStopUSec": "1min 30s", "TimerSlackNSec": "50000", "Transient": "no", "Type": "forking", "UMask": "0022", "UnitFilePreset": "disabled", "UnitFileState": "enabled", "WantedBy": "multi-user.target", "Wants": "system.slice", "WatchdogTimestampMonotonic": "0", "WatchdogUSec": "0"}}

    RUNNING HANDLER [nginx : restart nginx] ***************************************************************************************************************************************************************************
    changed: [localhost] => {"changed": true, "name": "nginx", "state": "started", "status": {"ActiveEnterTimestamp": "vie 2017-08-25 18:12:33 CDT", "ActiveEnterTimestampMonotonic": "2385921853", "ActiveExitTimestampMonotonic": "0", "ActiveState": "active", "After": "-.mount basic.target remote-fs.target tmp.mount nss-lookup.target system.slice network.target systemd-journald.socket", "AllowIsolate": "no", "AmbientCapabilities": "0", "AssertResult": "yes", "AssertTimestamp": "vie 2017-08-25 18:12:33 CDT", "AssertTimestampMonotonic": "2385870303", "Before": "multi-user.target shutdown.target", "BlockIOAccounting": "no", "BlockIOWeight": "18446744073709551615", "CPUAccounting": "no", "CPUQuotaPerSecUSec": "infinity", "CPUSchedulingPolicy": "0", "CPUSchedulingPriority": "0", "CPUSchedulingResetOnFork": "no", "CPUShares": "18446744073709551615", "CanIsolate": "no", "CanReload": "yes", "CanStart": "yes", "CanStop": "yes", "CapabilityBoundingSet": "18446744073709551615", "ConditionResult": "yes", "ConditionTimestamp": "vie 2017-08-25 18:12:33 CDT", "ConditionTimestampMonotonic": "2385870302", "Conflicts": "shutdown.target", "ControlGroup": "/system.slice/nginx.service", "ControlPID": "0", "DefaultDependencies": "yes", "Delegate": "no", "Description": "The nginx HTTP and reverse proxy server", "DevicePolicy": "auto", "ExecMainCode": "0", "ExecMainExitTimestampMonotonic": "0", "ExecMainPID": "31936", "ExecMainStartTimestamp": "vie 2017-08-25 18:12:33 CDT", "ExecMainStartTimestampMonotonic": "2385921802", "ExecMainStatus": "0", "ExecReload": "{ path=/bin/kill ; argv[]=/bin/kill -s HUP $MAINPID ; ignore_errors=no ; start_time=[n/a] ; stop_time=[n/a] ; pid=0 ; code=(null) ; status=0/0 }", "ExecStart": "{ path=/usr/sbin/nginx ; argv[]=/usr/sbin/nginx ; ignore_errors=no ; start_time=[vie 2017-08-25 18:12:33 CDT] ; stop_time=[vie 2017-08-25 18:12:33 CDT] ; pid=31933 ; code=exited ; status=0 }", "ExecStartPre": "{ path=/usr/sbin/nginx ; argv[]=/usr/sbin/nginx -t ; ignore_errors=no ; start_time=[vie 2017-08-25 18:12:33 CDT] ; stop_time=[vie 2017-08-25 18:12:33 CDT] ; pid=31930 ; code=exited ; status=0 }", "FailureAction": "none", "FileDescriptorStoreMax": "0", "FragmentPath": "/usr/lib/systemd/system/nginx.service", "GuessMainPID": "yes", "IOScheduling": "0", "Id": "nginx.service", "IgnoreOnIsolate": "no", "IgnoreOnSnapshot": "no", "IgnoreSIGPIPE": "yes", "InactiveEnterTimestampMonotonic": "0", "InactiveExitTimestamp": "vie 2017-08-25 18:12:33 CDT", "InactiveExitTimestampMonotonic": "2385871402", "JobTimeoutAction": "none", "JobTimeoutUSec": "0", "KillMode": "process", "KillSignal": "3", "LimitAS": "18446744073709551615", "LimitCORE": "18446744073709551615", "LimitCPU": "18446744073709551615", "LimitDATA": "18446744073709551615", "LimitFSIZE": "18446744073709551615", "LimitLOCKS": "18446744073709551615", "LimitMEMLOCK": "65536", "LimitMSGQUEUE": "819200", "LimitNICE": "0", "LimitNOFILE": "4096", "LimitNPROC": "14715", "LimitRSS": "18446744073709551615", "LimitRTPRIO": "0", "LimitRTTIME": "18446744073709551615", "LimitSIGPENDING": "14715", "LimitSTACK": "18446744073709551615", "LoadState": "loaded", "MainPID": "31936", "MemoryAccounting": "no", "MemoryCurrent": "18446744073709551615", "MemoryLimit": "18446744073709551615", "MountFlags": "0", "Names": "nginx.service", "NeedDaemonReload": "no", "Nice": "0", "NoNewPrivileges": "no", "NonBlocking": "no", "NotifyAccess": "none", "OOMScoreAdjust": "0", "OnFailureJobMode": "replace", "PIDFile": "/run/nginx.pid", "PermissionsStartOnly": "no", "PrivateDevices": "no", "PrivateNetwork": "no", "PrivateTmp": "yes", "ProtectHome": "no", "ProtectSystem": "no", "RefuseManualStart": "no", "RefuseManualStop": "no", "RemainAfterExit": "no", "Requires": "basic.target -.mount", "RequiresMountsFor": "/var/tmp", "Restart": "no", "RestartUSec": "100ms", "Result": "success", "RootDirectoryStartOnly": "no", "RuntimeDirectoryMode": "0755", "SameProcessGroup": "no", "SecureBits": "0", "SendSIGHUP": "no", "SendSIGKILL": "yes", "Slice": "system.slice", "StandardError": "inherit", "StandardInput": "null", "StandardOutput": "journal", "StartLimitAction": "none", "StartLimitBurst": "5", "StartLimitInterval": "10000000", "StartupBlockIOWeight": "18446744073709551615", "StartupCPUShares": "18446744073709551615", "StatusErrno": "0", "StopWhenUnneeded": "no", "SubState": "running", "SyslogLevelPrefix": "yes", "SyslogPriority": "30", "SystemCallErrorNumber": "0", "TTYReset": "no", "TTYVHangup": "no", "TTYVTDisallocate": "no", "TasksAccounting": "no", "TasksCurrent": "18446744073709551615", "TasksMax": "18446744073709551615", "TimeoutStartUSec": "1min 30s", "TimeoutStopUSec": "5s", "TimerSlackNSec": "50000", "Transient": "no", "Type": "forking", "UMask": "0022", "UnitFilePreset": "disabled", "UnitFileState": "enabled", "WantedBy": "multi-user.target", "Wants": "system.slice", "WatchdogTimestampMonotonic": "0", "WatchdogUSec": "0"}}

    PLAY RECAP ********************************************************************************************************************************************************************************************************
    localhost                  : ok=123  changed=60   unreachable=0    failed=0   

    The setup process completed successfully.
    Setup log saved to /var/log/tower/setup-2017-08-25-18:00:47.log

## Variables de Password
    [root@tower ansible-tower-setup-3.1.4]# cat inventory 
    [all:vars]
    admin_password='password'
    pg_password='password'
    rabbitmq_password='password'
