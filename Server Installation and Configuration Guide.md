# KeyCloak��������װ������ָ�� {#Server Installation and Configuration Guide}

[ԭ�ĵ�ַ: https://www.keycloak.org/docs/latest/server_installation/index.html](https://www.keycloak.org/docs/latest/server_installation/index.html)

## 1. ָ�ϸ��� {#Guide Overview}

��ָ�ϵ�Ŀ���ǽ������״�����Keycloak������֮ǰ��Ҫ��ɵĲ��衣�����ֻ�������Keycloak���������������Լ���Ƕ��ʽ�ͱ������ݿ⿪�伴�á����ڽ�Ҫ���������������е�ʵ�ʲ�������Ҫ�������������ʱ�������������(��������ģʽ)��ΪKeycloak�洢���ù������ݿ⣬���ü��ܺ�HTTPS���������Keycloak�ڼ�Ⱥ�����С���ָ�Ͻ���ϸ���ܲ��������֮ǰ������е��κ�Ԥ�������ߺ����õĸ������档

��Ҫ�ر�ע���һ���ǣ�Keycloak������WildFlyӦ�ó��������������Keycloak����෽�涼Χ����WildFly����Ԫ�ء�������������˽����ϸ�ڣ���ָ��ͨ���Ὣ�������ֲ�֮����ĵ���

### 1.1. ���������ⲿ�ĵ� {#Recommended Additional External Documentation}

Keycloak������WildFlyӦ�÷�����֮�ϣ���������Ŀ����Infinispan(���ڻ���)��Hibernate(���ڳ־���)����ָ��ֻ���ǻ�����ʩ�����õĻ���֪ʶ��ǿ�ҽ�������ϸ�Ķ�WildFly��������Ŀ���ĵ����������ĵ�����:

- [*WildFly 16 Documentation*](http://docs.wildfly.org/16/Admin_Guide.html)

## 2. ��װ {#Installation}


  ��װKeycloak�ǳ��򵥣�ֻ�����ز���ѹ�����ɡ����»ع���ϵͳ�������Լ����а��Ŀ¼�ṹ��

### 2.1. ϵͳ���� {#System Requirements}

����������Keycloak�����֤��������Ҫ��:

- ������Java���κβ���ϵͳ
- Java 8 JDK
- zip ���� gzip �� tar
- ����512M�ڴ�
- At least 1G of diskspace
- ������ⲿ���ݿ⣬��PostgreSQL��MySQL��Oracle�ȡ����Ҫ�ڼ�Ⱥ�����У�Keycloak��Ҫһ���ⲿ�������ݿ⡣�йظ�����Ϣ������ı�ָ�ϵ�[���ݿ�����](https://www.keycloak.org/docs/latest/server_installation/index.html#_database)���֡�
- ��������ڼ�Ⱥ�����У���ü�����ϵ�����֧�ֶಥ��Keycloak������û�жಥ������¼�Ⱥ����������Ҫ���������ø��ġ��йظ�����Ϣ����μ���ָ�ϵ�[��Ⱥ](https://www.keycloak.org/docs/latest/server_installation/index.html#_clustering)���֡�
- ��Linux�ϣ�����ʹ��`/dev/urandom`��Ϊ������ݵ���Դ���Է�ֹ����ȱ�ٿ��õ��ض�������Կ���ع��𣬳������İ�ȫ����ǿ��ʹ��`/dev/random`��Ҫ��Oracle JDK 8��OpenJDK 8��ʵ����һ�㣬������ `java.security.egd`ϵͳ����Ϊ` file:/dev/urandom`��

### 2.2. ��װ�ֲ�ʽ�ļ� {#Installing Distribution Files}

Keycloak�����������������صķ��а�:

- 'keycloak-6.0.0.[zip|tar.gz]'
- 'keycloak-overlay-6.0.0.[zip|tar.gz]'
- 'keycloak-demo-6.0.0.[zip|tar.gz]'

'keycloak-6.0.0.[zip|tar.gz]'�ļ��Ƿ�����Ψһ�ķ��а档��ֻ��������Keycloak�������Ľű��Ͷ������ļ���Ҫ��ѹ������ļ���ֻ�����в���ϵͳ��`unzip`��`gunzip`��`tar`ʵ�ó���

'keycloak-overlay-6.0.0.[zip|tar.gz]'�ļ���һ��WildFly����������������е�WildFly���а��ϰ�װKeycloak�����������ǲ�֧���û�ϣ����ͬһ������ʵ��������Ӧ�ó����Keycloak��Ҫ��װKeycloak�������ֻ�轫���ѹ��WildFly���а�ĸ�Ŀ¼�У���shell�е�binĿ¼������`./jboss-cli.[sh|bat] --file=keycloak-install.cli`��

'keycloak-demo-6.0.0.[zip|tar.gz]' �����������������ļ��������ĵ�������ʾ������Ԥ��������OIDC��SAML�ͻ���Ӧ�ó����������������ڲ������κ����õ�����¿��伴�õز����κηַ�ʾ�����˷ַ���ֻ������Щ��Ҫ����Keycloak���û�ʹ�á����ǲ�֧���û�������������������ʾ���а档

Ҫ��ѹ����Щ�ļ���������`unzip`��`gunzip`��`tar`ʵ�ó���

### 2.3. �ֲ�ʽĿ¼�ṹ {#Distribution Directory Structure}

���½����ܷ������ַ����Ŀ¼�ṹ��

�ֲ�ʽĿ¼�ṹ

![distribution](assets/files.png)

����������������һЩĿ¼����;:

- *bin/*

  ���������ֽű�������������������Ҳ�����ڷ�������ִ���������������

- *domain/*

  ����[��ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_domain-mode)������Keycloakʱ�������������ļ��͹���Ŀ¼��

- *modules/*

  ��Щ���Ƿ�����ʹ�õ�����Java�⡣

- *providers/*

  ���������Ϊkeycloak��д��չ�����Խ���չ��������й��ⷽ��ĸ�����Ϣ����μ�[������������Աָ��](https://www.keycloak.org/docs/6.0/server_development/)��

- *standalone/*

  ����������ļ��͹���Ŀ¼ʱ������Keycloak��[����ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_standalone-mode)��

- *themes/*

  ��Ŀ¼�������ڷ�������ʾ���κ�UI����Ҫ������html����ʽ��JavaScript�ļ���ͼ��������������޸����е�����򴴽��Լ������⡣�й��ⷽ��ĸ�����Ϣ����μ�[������������Աָ��](https://www.keycloak.org/docs/6.0/server_development/)��

## 3. ѡ����ģʽ {#Choosing an Operating Mode}

�����������в���Keycloak֮ǰ������Ҫ����ʹ���������͵Ĳ���ģʽ�������ڼ�Ⱥ������Keycloak��?����Ҫһ�ּ��еķ�ʽ�����������������?��ѡ��Ĳ���ģʽ��Ӱ��������������ݿ⡢���û��棬�������������������

> Keycloak������WildFlyӦ�÷�����֮�ϡ���ָ��ֻ�������ض�ģʽ�²���Ļ���֪ʶ����������˽��ⷽ��ľ�����Ϣ����õ�ȥ����[*WildFly 16 Documentation*](http://docs.wildfly.org/16/Admin_Guide.html).  

### 3.1. ����ģʽ {#Standalone Mode}

�����Ĳ���ģʽֻ����ϣ������һ���ҽ�����һ��Keycloak������ʵ��ʱ�����á����������ڼ�Ⱥ���𣬶������л��涼�ǷǷֲ�ʽ�ģ�����ֻ�ڱ���ʹ�á� ��������������ʹ�ö���ģʽ����Ϊֻ��һ�����ϵ㡣������ĵ���ģʽ������崻����û����޷���¼������ģʽֻ�����ڲ���������ʹ��Keycloak�Ĺ���.

#### 3.1.1. �����������ű� {#Standalone Boot Script}

���Զ���ģʽ���з�����ʱ������Ҫ����һ���ض��Ľű�����������������ȡ�������Ĳ���ϵͳ����Щ�ű�λ�ڷ������ַ���� *bin/* Ŀ¼�С�

�����������ű�

![standalone boot files](assets/standalone-boot-files.png)

����������:

Linux/Unix

```
$ .../bin/standalone.sh
```

Windows

```
> ...\bin\standalone.bat
```

#### 3.1.2. ���������� {#Standalone Configuration}

��ָ�ϵĴ󲿷����ݽ�ָ�����������Keycloak�Ļ�����ʩ�����档 ��Щ�������������ļ������õģ��������ļ��ض���Keycloak������Ӧ�ó�����������ڶ�������ģʽ�£����ļ�λ�� *.. / independent /configuration/standalone.xml* �С� ���ļ������������ض���Keycloak����ķǻ�����ʩ��������ݡ�

�����������ļ�

![standalone config file](assets/standalone-config-file.png)

> �ڷ���������ʱ�Ը��ļ��������κθ��Ķ�������Ч���������ܱ����������ǡ�����ʹ�������нű���WildFly��web����̨�� ������Ϣ�μ�[*WildFly 16 Documentation*](http://docs.wildfly.org/16/Admin_Guide.html)��                     

### 3.2. �����ļ�Ⱥģʽ {#Standalone Clustered Mode}

����ϣ���ڼ�Ⱥ������Keycloakʱ������ʹ�ö�����Ⱥ����ģʽ����ģʽҪ����ϣ�����з�����ʵ����ÿ̨������϶���Keycloak�ַ���ĸ���������ģʽ��������ײ��𣬵��ǻ����൱�鷳��Ҫ�������ø��ģ��������޸�ÿ̨�����ϵ�ÿ�����а档���ڴ��ͼ�Ⱥ������ܻ�ķ�ʱ�䲢���׳���

#### 3.2.1. �����ļ�Ⱥ���� {#Standalone Clustered Configuration}

�÷��а���һ����ҪԤ���õ�app�����������ļ��������ڼ�Ⱥ�����С��������������硢���ݿ⡢����ͷ��ֵ������ض�������ʩ���á����ļ�פ���� *��/standalone/configuration/standalone-ha.xml*. ���������ȱ��һЩ��������������ù������ݿ����ӣ��Ͳ����ڼ�Ⱥ������Keycloak��������Ҫ�ڼ�Ⱥǰ�沿��ĳ�����͵ĸ��ؾ������� ��ָ�ϵ�[��Ⱥ](https://www.keycloak.org/docs/latest/server_installation/index.html#_clustering)  �� [���ݿ�](https://www.keycloak.org/docs/latest/server_installation/index.html#_database) ���ֽ�ָ�����˽���Щ���ݡ�

��׼HA����

![standalone ha config file](assets/standalone-ha-config-file.png)

> �ڷ���������ʱ�Ը��ļ��������κθ��Ķ�������Ч���������ܱ����������ǡ�����ʹ�������нű���WildFly��web����̨�� ������Ϣ�μ� [*WildFly 16 Documentation*](http://docs.wildfly.org/16/Admin_Guide.html)                                  |

#### 3.2.2. ������Ⱥ�����ű� {#Standalone Clustered Boot Script}

ʹ�����ڶ���ģʽ����ͬ�������ű�����Keycloak����֮ͬ�����ڣ���������һ������ı�־��ָ��HA�����ļ���

������Ⱥ�����ű�

![standalone boot files](https://www.keycloak.org/docs/latest/server_installation/keycloak-images/standalone-boot-files.png)

����������:

Linux/Unix

```
$ .../bin/standalone.sh --server-config=standalone-ha.xml
```

Windows

```
> ...\bin\standalone.bat --server-config=standalone-ha.xml
```

### 3.3. ��Ⱥģʽ {#}

��ģʽ��һ�ּ��й���ͷ������������õķ�����

�ڱ�׼ģʽ�����м�Ⱥ�����ż�Ⱥ��ģ��������Ѹ�ٶ񻯡�ÿ����Ҫ��������ʱ���������ڼ�Ⱥ�е�ÿ���ڵ���ִ�С� ��ģʽ������������ͨ���ṩһ������λ�ô洢�ͷ������á� �������������൱���ӣ���������ֵ�õġ�������ܱ����õ�WildFlyӦ�÷������У�Keycloak���Ǵ����Ӧ�÷����������ġ�

> ��ָ�Ͻ�������ģʽ�Ļ���֪ʶ����������ڼ�Ⱥ��������ģʽ����ϸ����Ӧ�ô�[*WildFly 16 Documentation*](http://docs.wildfly.org/16/Admin_Guide.html). ��á�

����������ģʽ�����е�һЩ�������

- �������

  ���������һ�����̣�����洢������ͷ�����Ⱥ��ÿ���ڵ��һ�����á���������Ǽ�Ⱥ�еĽڵ��ȡ�����õ����ĵ㡣

- ����������

  ������������������ض������ϵķ�����ʵ���� ����������Ϊ����һ������������ʵ�������������������ÿ̨�����ϵ���������������������Ⱥ�� Ϊ�˼������н��̵�����������������䵱�������л����ϵ�������������

- �������ļ�

  �������ļ���һ�������������ļ����ɹ����������������� ����������Զ��岻ͬ������ʹ�õĶ���������ļ���

- ��������

  ���������Ƿ������ļ��ϡ����Ǳ���������Ϊһ���������Խ�һ���������ļ������һ���������飬�����е�ÿ�����񶼽�ʹ�ø��������ļ���Ϊ���ǵ����á�

����ģʽ�£������ڵ������������������Ⱥ������λ����������С� ����������Ⱥ���е�ÿ̨����������������������� ÿ��������������������ָ�����ڸü������������Keycloak������ʵ������ ����������������ʱ����������Keycloak������ʵ��������ʱһ���ࡣ��Щ������ʵ���������������ȡ���á�

#### 3.3.1. ������ {#}

��ָ�ϵ��������½���������������ݿ⡢HTTP�������ӡ�����������������ʩ��ص����ݡ� ��Ȼ����ģʽʹ�� *standalone.xml* �ļ���������Щ���ݣ�����ģʽʹ�� *.../domain/configuration/domain.xml* �����ļ��� ���ﶨ����Keycloak ���������������ļ��ͷ������顣

domain.xml

![domain file](assets/domain-file.png)

> �������������ʱ�Ը��ļ��������κθ��Ķ�������Ч���������ܱ����������ǡ�����ʹ�������нű���WildFly��web����̨�� ������Ϣ�μ�[*WildFly 16 Documentation*](http://docs.wildfly.org/16/Admin_Guide.html)

������������� *domain.xml* �ļ���ĳЩ���ݡ� `auth-server-standalone` �� `auth-server-clustered` `profile` XML���������д������þ��ߵĵط��� �����ڴ˴������������ӣ���������ݿ����ӵ����ݡ�

auth-server����

```
    <profiles>
        <profile name="auth-server-standalone">
            ...
        </profile>
        <profile name="auth-server-clustered">
            ...
        </profile>
```

`auth-server-standalone`�����ǷǼ�Ⱥ���á� `auth-server-clustered`�����Ǽ�Ⱥ���á�

������һ�����¹�������ῴ�������˸���`socket-binding-groups`��

socket-binding-groups

```
    <socket-binding-groups>
        <socket-binding-group name="standard-sockets" default-interface="public">
           ...
        </socket-binding-group>
        <socket-binding-group name="ha-sockets" default-interface="public">
           ...
        </socket-binding-group>
        <!-- load-balancer-sockets should be removed in production systems and replaced with a better software or hardware based one -->
        <socket-binding-group name="load-balancer-sockets" default-interface="public">
           ...
        </socket-binding-group>
    </socket-binding-groups>
```

�����ö���ʹ��ÿ��Keycloak������ʵ���򿪵ĸ�����������Ĭ�϶˿�ӳ�䡣 ����`$ {...}`���κ�ֵ���ǿ�������������ʹ��`-D`������д��ֵ������:

```
$ domain.sh -Djboss.http.port=80
```

Keycloak��������Ķ���λ�� `server-groups` XML���С� ��ָ������������������ʵ��ʱʹ�õ��������ļ�(`default`)�Լ�Java VM��һЩĬ������������ ������`socket-binding-group`�󶨵��������顣

server group

```
    <server-groups>
        <!-- load-balancer-group should be removed in production systems and replaced with a better software or hardware based one -->
        <server-group name="load-balancer-group" profile="load-balancer">
            <jvm name="default">
                <heap size="64m" max-size="512m"/>
            </jvm>
            <socket-binding-group ref="load-balancer-sockets"/>
        </server-group>
        <server-group name="auth-server-group" profile="auth-server-clustered">
            <jvm name="default">
                <heap size="64m" max-size="512m"/>
            </jvm>
            <socket-binding-group ref="ha-sockets"/>
        </server-group>
    </server-groups>
```

#### 3.3.2. �������������� {#}

Keycloak�������������������������ļ�������λ�� *.../domain/configuration/* Ŀ¼�У�*host-master.xml* �� *host-slave.xml*�� *host-master.xml* ����Ϊ����������������ؾ�������һ��Keycloak������ʵ���� *host-slave.xml* ����Ϊ���������ͨ�Ų�����һ��Keycloak������ʵ����

> ���ؾ��������Ǳ���ķ��� ���Ĵ���ʹ���������ɵ��ڿ���������ϲ���������Ⱥ���� ��Ȼ������������ʹ�ã��������Ҫʹ����������Ӳ��������ĸ��ؾ������������ѡ���滻����

��������������

![host files](assets/host-files.png)

Ҫ���ø��ؾ�����������ʵ������༭ *host-master.xml* ��ע�͵���ɾ�� `"load-balancer"` ��Ŀ��

```
    <servers>
        <!-- remove or comment out next line -->
        <server name="load-balancer" group="loadbalancer-group"/>
        ...
    </servers>
```

���ڴ��ļ�����һ����Ȥ�����������������֤������ʵ���� ����һ��`port-offset`���á� *domain.xml*`socket-binding-group`����������ж�����κ�����˿ڶ������`port-offset`��ֵ�� ���ڴ�ʾ�������ã�����ִ�д˲������Ա㸺��ƽ�����������򿪵Ķ˿ڲ����������������֤������ʵ����ͻ��

```
    <servers>
        ...
        <server name="server-one" group="auth-server-group" auto-start="true">
             <socket-bindings port-offset="150"/>
        </server>
    </servers>
```

#### 3.3.3. ������ʵ������Ŀ¼ {#}

�����ļ��ж����ÿ��Keycloak������ʵ���� *��/domain/servers/{SERVER NAME}* �´���һ������Ŀ¼�����������н����������ã����ҷ�����ʵ����Ҫ�򴴽����κ���ʱ����־�������ļ�Ҳ���Է������ ÿ��������Ŀ¼�Ľṹ���տ��������κ�����WildFly�����ķ�������

����Ŀ¼

![domain server dir](assets/domain-server-dir.png)

#### 3.3.4. �������ű� {#}

����ģʽ�����з�����ʱ���������Ĳ���ϵͳ����Ҫ�����ض��Ľű��������������� ��Щ�ű�λ�ڷ������ַ��� *bin/* Ŀ¼�С�

�������ű�

![domain boot files](assets/domain-boot-files.png)

����������:

Linux/Unix

```
$ .../bin/domain.sh --host-config=host-master.xml
```

Windows

```
> ...\bin\domain.bat --host-config=host-master.xml
```

���������ű�ʱ������Ҫͨ��`--host-config`���ش�������Ҫʹ�õ��������������ļ���

#### 3.3.5. ��Ⱥ��ʾ�� {#}

������ʹ�ÿ��伴�õ� *domain.xml* ���ò�����������Ⱥ�����ʾ������������һ̨���������в�������:

- 1���������
- 1��HTTP���ؾ�����
- 2��Keycloak������ʵ��

Ҫģ������̨����������м�Ⱥ����������`domain.sh`�ű��������������������������������� ��һ�������������������������������������HTTP����ƽ������һ��Keycloak��֤������ʵ���� �ڶ����Ǵ�����������������ֻ����һ����֤������ʵ����

##### ���ô������������������������ {#}

������֮ǰ�����������ô����������������Ա������԰�ȫ�����������ͨ�š��������������������������޷������������ȡ����ʽ���á� Ҫ���ð�ȫ���ӣ������봴������������Ա�û��ͽ������������ʹӷ�����֮�乲�����Կ�� ������ͨ������ `��/bin/add-user.sh` �ű�����ɴ˲�����

�������нű�ʱ��ѡ�� `Management User` ���ش� `yes` ������ѯ�����Ƿ����û�����һ��AS���������ӵ���һ��AS����ʱ�� �⽫����һ������ֵ������Ҫ������в�ճ���� *��/domain/configuration/host-slave.xml* �ļ��С�

���: App Server Admin

```bash
$ add-user.sh
 What type of user do you wish to add?
  a) Management User (mgmt-users.properties)
  b) Application User (application-users.properties)
 (a): a
 Enter the details of the new user to add.
 Using realm 'ManagementRealm' as discovered from the existing property files.
 Username : admin
 Password recommendations are listed below. To modify these restrictions edit the add-user.properties configuration file.
  - The password should not be one of the following restricted values {root, admin, administrator}
  - The password should contain at least 8 characters, 1 alphabetic character(s), 1 digit(s), 1 non-alphanumeric symbol(s)
  - The password should be different from the username
 Password :
 Re-enter Password :
 What groups do you want this user to belong to? (Please enter a comma separated list, or leave blank for none)[ ]:
 About to add user 'admin' for realm 'ManagementRealm'
 Is this correct yes/no? yes
 Added user 'admin' to file '/.../standalone/configuration/mgmt-users.properties'
 Added user 'admin' to file '/.../domain/configuration/mgmt-users.properties'
 Added user 'admin' with groups to file '/.../standalone/configuration/mgmt-groups.properties'
 Added user 'admin' with groups to file '/.../domain/configuration/mgmt-groups.properties'
 Is this new user going to be used for one AS process to connect to another AS process?
 e.g. for a slave host controller connecting to the master or for a Remoting connection for server to server EJB calls.
 yes/no? yes
 To represent the user add the following to the server-identities definition <secret value="bWdtdDEyMyE=" />
```

> add-user.sh���Ὣ�û���ӵ�Keycloak��������������ӵ�����JBoss��ҵӦ�ó���ƽ̨�� �����ű���ʹ�ú����ɵ�ƾ�ݽ�����ʾ��Ŀ�ġ� ��ʹ��ϵͳ�����ɵġ�   

���ڽ�����ֵ���в�ճ���� *��/domain/configuration/host-slave.xml* �ļ��У�������ʾ��

```xml
     <management>
         <security-realms>
             <security-realm name="ManagementRealm">
                 <server-identities>
                     <secret value="bWdtdDEyMyE="/>
                 </server-identities>
```

������Ҫ�� *��/domain/configuration/host-slave.xml* �ļ�������Ѵ����û��� *username*��

```xml
     <remote security-realm="ManagementRealm" username="admin">
```

##### ���������ű� {#}

����������һ̨����������ģ��˫�ڵ㼯Ⱥ����������������������ű���

���� ��

```
$ domain.sh --host-config=host-master.xml
```

���� ����

```
$ domain.sh --host-config=host-slave.xml
```

Ҫ������������������ת�� <http://localhost:8080/auth>��

### 3.4. ���������ĸ���ģʽ {#}

���������ĸ���ģʽ��������ϣ���������������ڼ�Ⱥ������Keycloak����õ���ʹ��λ�ڲ�ͬ�����������������վ�㡣 ʹ�ô�ģʽʱ��ÿ���������Ķ����Լ���Keycloak��������Ⱥ��

���ĵ�����������ʾ����ϵ�ṹͼ��˵���������򵥵Ŀ��������ĸ���������

ʾ���ܹ�ͼ

![cross dc architecture](assets/cross-dc-architecture.png)

#### 3.4.1. �Ⱦ����� {#}

��������һ���߼����⣬���ǽ����������Ķ��������ݣ������ṩ�˱���ı���֪ʶ��

- [��Ⱥ��Keycloak](https://www.keycloak.org/docs/6.0/server_installation/#_clustering) ���ÿ��������ĸ���ʱ������ʹ�ø��������Keycloak��Ⱥ������������˽⼯Ⱥ�Ĺ�����ʽ�Լ����������Ҫ�����縺��ƽ�⣬�������ݿ�Ͷಥ��
- [JBoss����������������ĸ���](https://access.redhat.com/documentation/en-us/red_hat_data_grid/7.3/html/red_hat_data_grid_user_guide/x_site_replication) Keycloakʹ��JBoss Data Grid��JDG������������֮�临��Infinispan���ݡ�

#### 3.4.2. ����ϸ�� {#}

���ڽ�����������Keycloak���������ĸ��Ƶĸ������ϸ��Ϣ��

Data(����)

Keycloak����״̬��Ӧ�ó��� ��ʹ��������Ϊ����Դ��

- ���ݿ����ڱ����������ݣ������û���Ϣ��
- Infinispan�������ڻ����������ݿ�ĳ־������ݣ������ڱ���һЩ���ں�Ƶ�����ĵ�Ԫ���ݣ����������û��Ự�� Infinispanͨ�������ݿ��ö࣬����ʹ��Infinispan��������ݲ��������Եģ�����Ԥ�Ʋ����ڼ�Ⱥ�����ڼ�������ڡ�

�����ǵ�ʾ���ܹ��У���������Ϊ `site1` �� `site2` ���������ġ� ���ڿ��������ĸ��ƣ����Ǳ���ȷ����������Դ���ɿ��ع������������� `site1` ��Keycloak�����������ܹ���ȡ`site2`�ϵ�Keycloak��������������ݡ�

���ݻ�����������ѡ���Ƿ�Ը�⣺

- �ɿ��� - ͨ������ `��/��` ģʽ�� д��`site1`�ϵ����ݱ���������`site2`�Ͽɼ���
- ���� - ͨ������ `��/��`ģʽ�� д��`site1`�ϵ����ݲ���Ҫ������`site2`�Ͽɼ��� ��ĳЩ����£����ݿ�����`site2`�ϸ������ɼ���

For more details, see [Modes](https://www.keycloak.org/docs/latest/server_installation/index.html#modes).

#### 3.4.3. ������ {#}

�����û����������[ǰ�˸��ؾ�����](https://www.keycloak.org/docs/6.0/server_installation/#_setting-up-a-load-balancer-or-proxy)����HTTP���� �˸��ؾ�����ͨ����HTTPD��WildFly������mod_cluster��NGINX��HA��������ĳЩ�������͵������Ӳ�����ؾ�������

Ȼ�󣬸��ؾ�����������յ�HTTP����ת��������Keycloakʵ������Щʵ�������ڶ����������֮�䴫���� ����ƽ����ͨ��Ϊ[ճ�ԻỰ](https://www.keycloak.org/docs/6.0/server_installation/#sticky-sessions)�ṩ֧��, ����ζ�Ÿ��ؾ������ܹ�ʼ�ս�����ͬһ�û�������HTTP����ת����ͬһ���������ڵ�ͬһKeycloakʵ����

�ӿͻ���Ӧ�ó����͵����ؾ�������HTTP�����Ϊ������ͨ�����󡱡��ն��û�����������ῴ����Щ����˲�����Ϊ�û��͸���ƽ����֮���ճ�ԻỰ��һ���֡� ���ڷ����ŵ����󣬸��ؾ��������Խ�HTTP����ת�����κ����������е��κ�Keycloakʵ���� �������ս�ԣ���ΪһЩOpenID Connect��һЩSAML����Ҫ�����û���Ӧ�ó���Ķ��HTTP���� �������ǲ��ܿɿ�������ճ�ԻỰ��ǿ�ƽ�������������͵�ͬһ���������е�ͬһ��Keycloakʵ����������Ǳ�����������ĸ���һЩ���ݣ��Ա����ض����ڼ��ɺ���HTTP����鿴���ݡ�

#### 3.4.4. Modes (ģʽ) {#}

��������Ҫ�󣬿��������ĸ��������ֻ�������ģʽ��

- ��/�� - ����û��Ϳͻ���Ӧ�ó�����������͵������������ĵ�Keycloak�ڵ㡣 �ڶ����������Ľ������������ݵ�`����`�� ������������ĳ��ֹ��ϣ�ͨ�����Դӵڶ����������Ļָ����ݡ�
- ��/�� - ����û��Ϳͻ���Ӧ�ó��������͵������������ĵ�Keycloak�ڵ㡣 ����ζ��������Ҫ����������վ���Ͽɼ������ҿ�������������վ���ϵ�Keycloak��������ʹ�á� ���Keycloak��������`site1`��д��һЩ���ݣ�����Ҫ����`site1`�ϵ�д����ɺ���������ͨ��`site2`�ϵ�Keycloak��������ȡ���ݡ�

`����/����`ģʽ�����ܸ��á� �й����Ϊ��һģʽ���ø��ٻ������ϸ��Ϣ������ģ�[SYNC��ASYNC����](https://www.keycloak.org/docs/latest/server_installation/index.html#backups).

#### 3.4.5. ���ݿ� {#}

Keycloakʹ�ù�ϵ���ݿ����ϵͳ(RDBMS)���־ñ����й����򣬿ͻ��ˣ��û��ȵ�һЩԪ���ݡ� �й���ϸ��Ϣ������ķ�������װָ�ϵ�[����](https://www.keycloak.org/docs/6.0/server_installation/#_database)�� �ڿ��������ĸ��������У����Ǽ��������������Ķ���ͬһ�����ݿ�ͨ�ţ�����ÿ���������Ķ����Լ������ݿ�ڵ㣬�����������ݿ�ڵ�����������֮��ͬ�����ơ� ������������£���`site1`�ϵ�Keycloak�������־ñ���ĳЩ���ݲ��ύ����ʱ��Ҫ����Щ����������`site2`�ϵĺ������ݿ������пɼ���

���ݿ����õ�ϸ�ڳ�����Keycloak�ķ�Χ��������MariaDB��Oracle���������RDBMS��Ӧ�̶��ṩ�˸������ݿ��ͬ�����ơ� ��������Щ��Ӧ��һ�����Keycloak��

- Oracle Database 12c Release 1 (12.1) RAC
- Galera 3.12 cluster for MariaDB server version 10.1.19-MariaDB

#### 3.4.6. Infinispan���� {#}

�������Ƚ���Infinispan����ĸ߼������� �����ǻ������õĸ���ϸ�ڡ�

Authentication sessions (��֤�Ự)

��Keycloak�У���������֤�Ự�ĸ�� ��һ����Ϊ `authenticationSessions` �Ķ���Infinispan�����������ض��û��������֤�ڼ䱣�����ݡ� ���Դ˻��������ͨ��ֻ�漰�������Keycloak��������������Ӧ�ó��� ��������ǿ�������ճ�ԻỰ����ʹ������`��/��` ģʽ��Ҳ����Ҫ���������ĸ��� `authenticationSessions` �������ݡ�

Action tokens (��������)

���ǻ���[��������](https://www.keycloak.org/docs/6.0/server_development/#_action_token_spi)�ĸ�� ͨ�������û���Ҫͨ�������ʼ��첽��ȷ�ϲ����ĳ��������磬�ڡ��������롱���ڼ䣬`actiontoken`Infinispan�������ڸ����йز������Ƶ�Ԫ���ݣ������Ѿ�ʹ�����ĸ��������ƣ���˲��ܵڶ������á���ͨ����Ҫ���������ĸ��ơ�

�־����ݵĻ����ʧЧ

Keycloakʹ��Infinispan������־����ݣ��Ա�������ݿ����಻��Ҫ������ ������������ܣ����������˶������ս�� ��ĳЩKeycloak�����������κ�����ʱ���������������е���������Keycloak����������Ҫ֪������������ǻ�ʹ�仺���е��ض�������Ч�� Keycloakʹ�ó�Ϊ`realms` ��`users` �� `authorization` �ı���Infinispan����������־����ݡ�

����ʹ�õ����Ļ��� `work`�������������������и��ơ� �������汾���Ỻ���κ�ʵ�����ݡ� ����������Ⱥ���ڵ����������֮�䷢��ʧЧ��Ϣ�� ���仰˵������������ʱ�������û�`john`��Keycloak�ڵ㽫ʧЧ��Ϣ���͵�ͬһ�������ĵ�����������Ⱥ�ڵ��Լ����������������ġ� �յ���Ч֪ͨ��ÿ���ڵ㶼����䱾�ػ�����ʹ��Ӧ��������Ч��

User sessions (�û��Ự)

Infinispan�����Ϊ `sessions`, `clientSessions`, `offlineSessions` �� `offlineClientSessions`��������Щ����ͨ������Ҫ���������Ľ��и��ơ� ��Щ�������ڱ����й��û��Ự�����ݣ���Щ���ݶ��û���������Ự������Ч�� ������봦�����������û���Ӧ�ó����HTTP���� �����������ڴ�ʵ�����޷��ɿ���ʹ��ճ�ԻỰ����������ϣ��ȷ������HTTP������Բ鿴�������ݡ� ��ˣ�����ͨ������������֮�临�ơ�

Brute force protection (ǿ������)

���`loginFailures` �������ڸ����й�ʧ�ܵ�¼�����ݣ������û�`john` �����������Ĵ����� ��ϸ˵��[�˴�](https://www.keycloak.org/docs/6.0/server_admin/#password-guess-brute-force-attacks)�� ����Ա�Ƿ�Ӧ�ÿ��������ĸ��ƴ˻��档 Ҫ׼ȷ�����¼ʧ�ܴ�������Ҫ���и��ơ� ��һ���棬�����ƴ����ݿ��Խ�ʡһЩ���ܡ� ��ˣ�������ܱ�׼ȷ�ĵ�¼ʧ�ܼ�������Ҫ������Ա��⸴�ơ�

�й�������ø��ٻ���ĸ�����ϸ��Ϣ�������[����JDG���ٻ�������](https://www.keycloak.org/docs/latest/server_installation/index.html#tuningcache)��

#### 3.4.7. ͨ��ϸ�� {#}

keycoverʹ�ö��������Infinispan���漯Ⱥ��ÿ��Keycloak �ڵ㶼����ͬ���������е�����Keycloak �ڵ��ڼ�Ⱥ�У�����������ͬ�������ĵ�Keycloak�ڵ㡣 Keycloak�ڵ㲻ֱ�������Բ�ͬ�������ĵ�Keycloak�ڵ�ͨ�š� Keycloak�ڵ�ʹ���ⲿJDG��ʵ������Infinispan�����������������Ľ���ͨ�š� ����ʹ��[Infinispan HotRodЭ��](http://infinispan.org/docs/8.2.x/user_guide/user_guide.html#using_hot_rod_server)��

Keycloak���ϵ�Infinispan�����������Ϊ[remoteStore](http://infinispan.org/docs/8.2.x/user_guide/user_guide.html#remote_store)����ȷ�����ݱ����浽Զ�̻����С�JDG������֮���е�����Infinispan��Ⱥ����˱����� `site1` �ϵ�JDG1�ϵ����ݱ����Ƶ� `site2`�ϵ�JDG2�ϡ�

��󣬽���JDG������ͨ���ͻ���������֪ͨ��Ⱥ�е�Keycloak������������HotRodЭ���һ�����ԡ�Ȼ��������ǵ�Infinispan���棬�ض����û��ỰҲ������ `site2` ��Keycloak�ڵ��Ͽ�����

�йظ���ϸ�ڣ���μ�[ʾ���ܹ�ͼ](https://www.keycloak.org/docs/latest/server_installation/index.html#archdiagram)��

#### 3.4.8. �������� {#}

�ڱ����У�����������ʹ�������������ģ�`site1` �� `site2`�� ÿ������������1��Infinispan��������2��Keycloak��������ɡ� �������ս�ӵ��2̨Infinispan��������4̨Keycloak��������

- `Site1` ��Infinispan��������`jdg1` ��2��Keycloak��������`node11` �� `node12` ��ɡ�
- `Site2` ��Infinispan��������`jdg2` ��2��Keycloak��������`node21` �� `node22` ��ɡ�
- Infinispan������ `jdg1` �� `jdg2` ͨ�� RELAY2 Э��� `backup` ��Infinispan�����໥���ӣ��䷽ʽ��[JDG�ĵ�](https://access.redhat.com/documentation/en-us/red_hat_data_grid/7.3/html/red_hat_data_grid_user_guide/x_site_replication)�����������ơ�
- Keycloak������ `node11` �� `node12` �˴��γ�һ����Ⱥ�������ǲ�ֱ���� `site2` �е��κη�����ͨ�š� ����ʹ��HotRodЭ�飨Զ�̻��棩��Infinispan������ `jdg1` ����ͨ�š� �й���ϸ��Ϣ�������[ͨ����ϸ��Ϣ](https://www.keycloak.org/docs/latest/server_installation/index.html#communication)��
- ͬ����ϸ�������� `node21` �� `node22`�����Ǳ˴˼�Ⱥ����ʹ��HotRodЭ����`jdg2`������ͨ�š�

���ǵ�ʾ�����üٶ�����4��Keycloak����������ͬһ�����ݿ�ͨ�š� �������У����������ݿ���ʹ�õ�����ͬ���������ݿ⣬��[���ݿ�](https://www.keycloak.org/docs/latest/server_installation/index.html#database)��������

##### Infinispan���������� {#}

�밴�����²�������Infinispan��������

1. ����Infinispan 9.4.8����������ѹ������ѡ���Ŀ¼�� ��λ�ý��ں���Ĳ����г�Ϊ `JDG1_HOME` ��

2. ��JGroups��ϵͳ�������и��� `JDG1_HOME/standalone/configuration/clustered.xml`�е���Щ���ݣ�

   1. �� `channels` Ԫ������� `xsite` ͨ��������ʹ��`tcp` ��ջ��

      ```xml
      <channels default="cluster">
          <channel name="cluster"/>
          <channel name="xsite" stack="tcp"/>
      </channels>
      ```

   2. �� `udp` ��ջ��ĩβ��� `relay` Ԫ�ء� ���ǽ������ǵ�վ��Ϊ `site1` �ķ�ʽ�������������ǽ����ݵ���һ��վ���� `site2` ��

      ```xml
      <stack name="udp">
          ...
          <relay site="site1">
              <remote-site name="site2" channel="xsite"/>
              <property name="relay_multicasts">false</property>
          </relay>
      </stack>
      ```

   3. ����`tcp`��ջʹ��`TCPPING`Э�������'MPING`�� ɾ��`MPING`Ԫ�ز������滻Ϊ`TCPPING`�� `initial_hosts`Ԫ��ָ������`jdg1`��`jdg2`��

      ```xml
      <stack name="tcp">
          <transport type="TCP" socket-binding="jgroups-tcp"/>
          <protocol type="TCPPING">
              <property name="initial_hosts">jdg1[7600],jdg2[7600]</property>
              <property name="ergonomics">false</property>
          </protocol>
          <protocol type="MERGE3"/>
          ...
      </stack>
      ```

      > ��ֻ��һ���ó���������е�ʾ�����á��������У�JGroups ' RELAY2 '����Ҫʹ��' tcp 'ջ�� ���������������κ�������ջ�����磬�����������֮�������֧�ֶಥ������ʹ��Ĭ�ϵ�udp��ջ�� ֻҪȷ��Infinispan��Keycloak��Ⱥ���໥���ɷ��ֵġ� ͬ����������Ҫʹ�� `TCPPING` ��Ϊ����Э�顣 �������У�����ܲ���ʹ��`TCPPING`��Ϊ���Ǿ�̬�ġ� ���վ������Ҳ�ǿ����õġ� �������ϸ�����õ���ϸ��Ϣ������Keycloak�ĵ��ķ�Χ�� �йظ�����ϸ��Ϣ�������Infinispan�ĵ���JGroups�ĵ���

3. ������ӵ���Ϊ`clustered`�Ļ��������µ�`JDG1_HOME/standalone/configuration/clustered.xml`�У�

   ```xml
   <cache-container name="clustered" default-cache="default" statistics="true">
           ...
           <replicated-cache-configuration name="sessions-cfg" mode="SYNC" start="EAGER" batching="false">
               <locking acquire-timeout="0" />
               <backups>
                   <backup site="site2" failure-policy="FAIL" strategy="SYNC" enabled="true">
                       <take-offline min-wait="60000" after-failures="3" />
                   </backup>
               </backups>
           </replicated-cache-configuration>
   
           <replicated-cache name="work" configuration="sessions-cfg"/>
           <replicated-cache name="sessions" configuration="sessions-cfg"/>
           <replicated-cache name="clientSessions" configuration="sessions-cfg"/>
           <replicated-cache name="offlineSessions" configuration="sessions-cfg"/>
           <replicated-cache name="offlineClientSessions" configuration="sessions-cfg"/>
           <replicated-cache name="actionTokens" configuration="sessions-cfg"/>
           <replicated-cache name="loginFailures" configuration="sessions-cfg"/>
   
   </cache-container>
   ```

   > �й� `replicated-cache-configuration` �е�����ѡ�����ϸ��Ϣ�������[����JDG��������](https://www.keycloak.org/docs/latest/server_installation/index.html#tuningcache)�����а�����Ϣ ���ڵ�������һЩѡ�

   > ����ǰ�İ汾��ͬ��Infinispan������ `replicated-cache-configuration` ��Ҫ��û�� `transaction` Ԫ�ص�����½������á� �й���ϸ��Ϣ�������[�����ų�](https://www.keycloak.org/docs/latest/server_installation/index.html#troubleshooting) ��

4. ��ͨ����������ܱ����Ļ���֮ǰ��ĳЩInfinispan�������汾��Ҫ��Ȩ��

   > �����ʹ���Ƽ���Infinispan 9.4.8����������Ӧ�ÿ����κ����⣬���ҿ��ԣ�����Ӧ�ã����Դ˲��衣 ����Ȩ��ص�������ܽ�������Infinispan��������ĳЩ�����汾��

   Keycloak��Ҫ���°����ű��� `___ script_cache` ���档 ������ʴ˻���ʱ��������Ҫ�� `clustered.xml` ������������Ȩ������������

   1. �� `<management>` �����У����һ����ȫ����

      ```xml
      <management>
          <security-realms>
              ...
              <security-realm name="AllowScriptManager">
                  <authentication>
                      <users>
                          <user username="___script_manager">
                              <password>not-so-secret-password</password>
                          </user>
                      </users>
                  </authentication>
              </security-realm>
          </security-realms>
      ```

   2. �ڷ�����������ϵͳ�У���� `<security>` ��������ʾ��

      ```xml
      <subsystem xmlns="urn:infinispan:server:core:8.4">
          <cache-container name="clustered" default-cache="default" statistics="true">
              <security>
                  <authorization>
                      <identity-role-mapper/>
                      <role name="___script_manager" permissions="ALL"/>
                  </authorization>
              </security>
              ...
      ```

   3. �ڶ˵���ϵͳ�У��������֤������ӵ�Hot Rod��������

      ```xml
      <subsystem xmlns="urn:infinispan:server:endpoint:8.1">
          <hotrod-connector cache-container="clustered" socket-binding="hotrod">
              ...
              <authentication security-realm="AllowScriptManager">
                  <sasl mechanisms="DIGEST-MD5" qop="auth" server-name="keycloak-jdg-server">
                      <policy>
                          <no-anonymous value="false" />
                      </policy>
                  </sasl>
              </authentication>
      ```

5. �����������Ƶ��ڶ���λ�ã��Ժ󽫳�֮Ϊ `JDG2_HOME`��

6. �� `JDG2_HOME/standalone/configuration/clustered.xml`����`site1`��`site2`����֮��Ȼ����JGroups��ϵͳ�е� `relay` ���ú�cache-subsystem�� `backups` �����á� ���磺

   1. `relay`Ԫ��Ӧ������ʾ��

      ```xml
      <relay site="site2">
          <remote-site name="site1" channel="xsite"/>
          <property name="relay_multicasts">false</property>
      </relay>
      ```

   2. ��������`backups`Ԫ�أ�

      ```xml
                  <backups>
                      <backup site="site1" ....
                      ...
      ```

      ����Infinispan��ϵͳ��֧���ñ��ʽ�滻վ���������Ŀǰ��ҪΪ����վ���ϵ�JDG�������ṩ��ͬ�������ļ����й���ϸ��Ϣ����μ�[this issue](https://issues.jboss.org/browse/WFLY-9458)��

7. ���������� `jdg1`:

   ```bash
   cd JDG1_HOME/bin
   ./standalone.sh -c clustered.xml -Djava.net.preferIPv4Stack=true \
     -Djboss.default.multicast.address=234.56.78.99 \
     -Djboss.node.name=jdg1 -b PUBLIC_IP_ADDRESS
   ```

8. ����������`jdg2`�����ڴ��ڲ�ͬ���鲥��ַ�����`jdg1`��`jdg2`����������ֱ�Ӽ�Ⱥ��һ��;�෴������ֻ��ͨ��RELAY2Э�����ӣ�TCP JGroups��ջ��������֮���ͨ�š�����������������:

   ```bash
   cd JDG2_HOME/bin
   ./standalone.sh -c clustered.xml -Djava.net.preferIPv4Stack=true \
     -Djboss.default.multicast.address=234.56.78.100 \
     -Djboss.node.name=jdg2 -b PUBLIC_IP_ADDRESS
   ```

9. Ҫ��֤��ʱͨ���Ƿ�������������Ҫʹ��JConsole�����ӵ��������е�`JDG1`��`JDG2`������������ʹ��MBean `jgroups:type=protocol,cluster="cluster",protocol=RELAY2`�Ͳ���`printRoutes`ʱ��Ӧ�ûῴ���������:

   ```
   site1 --> _jdg1:site1
   site2 --> _jdg2:site2
   ```

   ����ʹ��MBean  `jgroups:type=protocol,cluster="cluster",protocol=GMS` ʱ����Ӧ�ÿ������Գ�Աֻ����һ����Ա:

   1. ��`JDG1`��Ӧ����������:

      ```
      (1) jdg1
      ```

   2. ��JDG2����������:

      ```
      (1) jdg2
      ```

      > �������У���������ÿ����������ӵ�и���Infinispan�������� ��ֻ��Ҫȷ��ͬһ���������ڵ�Infinispan������ʹ����ͬ�Ķಥ��ַ�����仰˵��������ʱʹ����ͬ�� `jboss.default.multicast.address` ���� Ȼ����`GMS` Э����ͼ��jconsole�У�����������ǰ��Ⱥ�����г�Ա��

##### Keycloak���������� {#}

1. ��Keycloak�������ַ���ѹ������ѡ���λ�á� �����ں����Ϊ `NODE11`��

2. ΪKeycloakDS����Դ���ù������ݿ⡣ ����ʹ��MySQL��MariaDB���в��ԡ� �й���ϸ��Ϣ�������[���ݿ�](https://www.keycloak.org/docs/latest/server_installation/index.html#database)��

   �������У���������Ҫ��ÿ���������Ķ���һ�����������ݿ�������������������ݿ������Ӧ��ͬ�����Ƶ��˴ˡ� ��ʾ�������У�����ֻʹ��һ�����ݿⲢ������4��Keycloak���������ӵ�����

3. �༭ `NODE11/standalone/configuration/standalone-ha.xml` :

   1. ������`site`��ӵ�JGroups UDPЭ�飺

      ```xml
                        <stack name="udp">
                            <transport type="UDP" socket-binding="jgroups-udp" site="${jboss.site.name}"/>
      ```

   2. ����Ϊ`keycloak`��`cache-container`Ԫ����������`module`���ԣ�

      ```xml
       <cache-container name="keycloak" module="org.keycloak.keycloak-model-infinispan">
      ```

   3. ��`work`���������`remote-store`��

      ```xml
      <replicated-cache name="work">
          <remote-store cache="work" remote-servers="remote-cache" passivation="false" fetch-state="false" purge="false" preload="false" shared="true">
              <property name="rawValues">true</property>
              <property name="marshaller">org.keycloak.cluster.infinispan.KeycloakHotRodMarshallerFactory</property>
          </remote-store>
      </replicated-cache>
      ```

   4. ��`sessions`���������������`remote-store`��

      ```xml
      <distributed-cache name="sessions" owners="1">
          <remote-store cache="sessions" remote-servers="remote-cache" passivation="false" fetch-state="false" purge="false" preload="false" shared="true">
              <property name="rawValues">true</property>
              <property name="marshaller">org.keycloak.cluster.infinispan.KeycloakHotRodMarshallerFactory</property>
          </remote-store>
      </distributed-cache>
      ```

   5. ����`offlineSessions`��`clientSessions`��`offlineClientSessions`��`loginFailures`��`actionTokens`����ִ����ͬ�Ĳ�������`sessions`�����Ψһ������`cache`����ֵ��ͬ����

      ```xml
      <distributed-cache name="offlineSessions" owners="1">
          <remote-store cache="offlineSessions" remote-servers="remote-cache" passivation="false" fetch-state="false" purge="false" preload="false" shared="true">
              <property name="rawValues">true</property>
              <property name="marshaller">org.keycloak.cluster.infinispan.KeycloakHotRodMarshallerFactory</property>
          </remote-store>
      </distributed-cache>
      
      <distributed-cache name="clientSessions" owners="1">
          <remote-store cache="clientSessions" remote-servers="remote-cache" passivation="false" fetch-state="false" purge="false" preload="false" shared="true">
              <property name="rawValues">true</property>
              <property name="marshaller">org.keycloak.cluster.infinispan.KeycloakHotRodMarshallerFactory</property>
          </remote-store>
      </distributed-cache>
      
      <distributed-cache name="offlineClientSessions" owners="1">
          <remote-store cache="offlineClientSessions" remote-servers="remote-cache" passivation="false" fetch-state="false" purge="false" preload="false" shared="true">
              <property name="rawValues">true</property>
              <property name="marshaller">org.keycloak.cluster.infinispan.KeycloakHotRodMarshallerFactory</property>
          </remote-store>
      </distributed-cache>
      
      <distributed-cache name="loginFailures" owners="1">
          <remote-store cache="loginFailures" remote-servers="remote-cache" passivation="false" fetch-state="false" purge="false" preload="false" shared="true">
              <property name="rawValues">true</property>
              <property name="marshaller">org.keycloak.cluster.infinispan.KeycloakHotRodMarshallerFactory</property>
          </remote-store>
      </distributed-cache>
      
      <distributed-cache name="actionTokens" owners="2">
          <object-memory size="-1"/>
          <expiration max-idle="-1" interval="300000"/>
          <remote-store cache="actionTokens" remote-servers="remote-cache" passivation="false" fetch-state="false" purge="false" preload="true" shared="true">
              <property name="rawValues">true</property>
              <property name="marshaller">org.keycloak.cluster.infinispan.KeycloakHotRodMarshallerFactory</property>
          </remote-store>
      </distributed-cache>
      ```

   6. ��Զ�̴洢�ĳ�վ�׽��ְ���ӵ�`socket-binding-group`Ԫ�������У�

      ```xml
      <outbound-socket-binding name="remote-cache">
          <remote-destination host="${remote.cache.host:localhost}" port="${remote.cache.port:11222}"/>
      </outbound-socket-binding>
      ```

   7. �ֲ�ʽ����`authenticationSessions`��������������ñ��ֲ��䡣

   8. ����ѡ����`logging`��ϵͳ������DEBUG��־��¼��

      ```xml
      <logger category="org.keycloak.cluster.infinispan">
          <level name="DEBUG"/>
      </logger>
      <logger category="org.keycloak.connections.infinispan">
          <level name="DEBUG"/>
      </logger>
      <logger category="org.keycloak.models.cache.infinispan">
          <level name="DEBUG"/>
      </logger>
      <logger category="org.keycloak.models.sessions.infinispan">
          <level name="DEBUG"/>
      </logger>
      ```

4. ��`NODE11`���Ƶ�3������Ŀ¼�������Ϊ`NODE12`��`NODE21`��`NODE22`��

5. ���� `NODE11` :

   ```bash
   cd NODE11/bin
   ./standalone.sh -c standalone-ha.xml -Djboss.node.name=node11 -Djboss.site.name=site1 \
     -Djboss.default.multicast.address=234.56.78.1 -Dremote.cache.host=jdg1 \
     -Djava.net.preferIPv4Stack=true -b PUBLIC_IP_ADDRESS
   ```

6. ���� `NODE12` :

   ```bash
   cd NODE12/bin
   ./standalone.sh -c standalone-ha.xml -Djboss.node.name=node12 -Djboss.site.name=site1 \
     -Djboss.default.multicast.address=234.56.78.1 -Dremote.cache.host=jdg1 \
     -Djava.net.preferIPv4Stack=true -b PUBLIC_IP_ADDRESS
   ```

   Ӧ�����Ӽ�Ⱥ�ڵ㡣���������Ķ���Ӧ��ͬʱ������NODE11��NODE12����־��:

   ```
   Received new cluster view for channel keycloak: [node11|1] (2) [node11, node12]
   ```

   > ��־�е�ͨ�����ƿ��ܲ�ͬ��

7. ���� `NODE21` :

   ```bash
   cd NODE21/bin
   ./standalone.sh -c standalone-ha.xml -Djboss.node.name=node21 -Djboss.site.name=site2 \
     -Djboss.default.multicast.address=234.56.78.2 -Dremote.cache.host=jdg2 \
     -Djava.net.preferIPv4Stack=true -b PUBLIC_IP_ADDRESS
   ```

   ����Ӧ��ʹ��`NODE11`��`NODE12`���ӵ���Ⱥ�����Ƿֿ�һ����

   ```
   Received new cluster view for channel keycloak: [node21|0] (1) [node21]
   ```

8. ���� `NODE22` :

   ```bash
   cd NODE22/bin
   ./standalone.sh -c standalone-ha.xml -Djboss.node.name=node22 -Djboss.site.name=site2 \
     -Djboss.default.multicast.address=234.56.78.2 -Dremote.cache.host=jdg2 \
     -Djava.net.preferIPv4Stack=true -b PUBLIC_IP_ADDRESS
   ```

   ��Ӧ������`NODE21`�ļ�Ⱥ�У�

   ```
   Received new cluster view for channel keycloak: [node21|1] (2) [node21, node22]
   ```

   > ��־�е�ͨ�����ƿ��ܲ�ͬ�� 

9. ����:

   1. ת�� `http://node11:8080/auth/` ��������ʼ����Ա�û���

   2. ת�� `http://node11:8080/auth/admin` ����admin��ݵ�¼�������̨��

   3. �򿪵ڶ����������ת���κνڵ� `http://node12:8080/auth/admin` ��`http://node21:8080/auth/admin` ��  `http://node22:8080/auth/admin` �� ��¼����Ӧ���ܹ�������4̨�������ϵ��ض��û����ͻ��˻�����ġ��Ự��ѡ��п�����ͬ�ĻỰ��

   4. �ڶ�Keycloak�������̨�����κθ��ĺ����磬����ĳЩ�û���ĳЩ���򣩣�����Ӧ������4���ڵ��е��κ�һ���Ͽɼ�����Ϊ����Ӧ���κεط���ȷ��Ч��

   5. �����Ҫ������server.logs�� ��¼��ע������������ϢӦ�������нڵ��� `NODEXY/standalone/log/server.log`��

      ```
      2017-08-25 17:35:17,737 DEBUG [org.keycloak.models.sessions.infinispan.remotestore.RemoteCacheSessionListener] (Client-Listener-sessions-30012a77422542f5) Received event from remote store.
      Event 'CLIENT_CACHE_ENTRY_REMOVED', key '193489e7-e2bc-4069-afe8-f1dfa73084ea', skip 'false'
      ```

#### 3.4.9. ��DC����Ĺ��� {#}

���ڰ�������������ĸ�����ص�һЩ��ʾ��ѡ�

- ��������������������Keycloak������ʱ�� ��Ҫ�� `KeycloakDS` ����Դ�����õ����ݿ��Ѿ��ڸ��������������в����á� `outbound-socket-binding`���õ�Infinispan������Ҳ�Ǳ�Ҫ�ģ� ��Infinispan����`remote-store`Ԫ�����õ�,�Ѿ������С�����Keycloak���������޷�������
- ���Ҫ֧�����ݿ����ת�ƺ͸��ߵĿɿ��ԣ�ÿ���������Ķ�����ӵ�и������ݿ�ڵ㡣 �й���������ݿ�˽��������Լ������Keycloak������`KeycloakDS`����Դ����ϸ��Ϣ����������ݿ��JDBC����������ĵ���
- ÿ���������Ķ������ڼ�Ⱥ�����и���Infinispan�������� �������ҪһЩ����ת�ƺ͸��õ��ݴ��������⽫�ǳ����á� ����Infinispan��������Keycloak������֮��ͨ�ŵ�HotRodЭ��������¹��ܣ�Infinispan���������Զ���Keycloak�����������й�InfinispanȺ�����ĵ������ˣ� ��ˣ�Keycloak�˵�Զ�̴洢��֪�����������ӵ��ĸ�Infinispan���������Ķ�Infinispan��WildFly�ĵ��˽����ϸ�ڡ�
- ǿ�ҽ���������**�κ�**վ���е�Keycloak������֮ǰ����ÿ��վ��������һ����Infinispan�������� �����ǵ������У���������������Keycloak������֮ǰ������`jdg1`��`jdg2`�� �������Ȼ��Ҫ����Keycloak���������ұ���վ�㴦���ѻ�״̬����������վ���ϵ�Infinispan���������ֶ��л�����վ�㣬��[ʹվ���ѻ�������](https://www.keycloak.org/docs/latest/server_installation/index.html#onoffline)�������� ������ֶ���������վ���ѻ������һ���������ܻ�ʧ�ܣ������������ڼ���ܻ����һЩ�쳣��ֱ������վ�������õ�ʧ�ܲ����������Զ��ѻ���

#### 3.4.10. ʹ��վ�ѻ������� {#}

���磬�������������

1. վ��`site2`��`site1`�Ƕ���ȫ�ѻ��� ����ζ��`site2`�ϵ�����Infinispan���������ر�**����`site1`��`site2`֮������类�ƻ��ˡ�
2. ����վ��`site1`������Keycloak��������Infinispan������`jdg1`
3. ������`site1`�ϵ�Keycloak�������ϵ�¼��
4. ����`site1`��Keycloak�����������Խ��Ựд��`jdg1`�������ϵ�Զ�̻��棬�÷�����Ӧ�ý����ݱ��ݵ�`site2`�е�`jdg2`�������� �й���ϸ��Ϣ�������[ͨ����ϸ��Ϣ](https://www.keycloak.org/docs/latest/server_installation/index.html#communication)��
5. ������`jdg2`���߻��޷�����`jdg1`�� ���Դ�`jdg1`��`jdg2`�ı��ݽ�ʧ�ܡ�
6. ��`jdg1`��־���׳��쳣������Ҳ����`jdg1`������������Keycloak����������Ϊ������Ĭ�ϵ�`FAIL`����ʧ�ܲ��ԡ� �йر��ݲ��Ե���ϸ��Ϣ�������[����ʧ�ܲ���](https://www.keycloak.org/docs/latest/server_installation/index.html#backupfailure)��
7. ����Ҳ����Keycloak���淢�����û������޷���ɵ�¼��

�������Ļ�����վ��֮���������ܻ����ٿ��ܲ����û���ʱ�жϣ����ԣ������������������������`site1`�ϵ�Infinispan������֪��`site2`�ϵ�Infinispan�����������ã�������ǽ�ֹͣ���Է���`jdg2`վ���ϵķ����������Ҳ��ᷢ�����ݹ��ϡ��������ν�ġ�����վ�ѻ�����

ʹ��վ�ѻ�

�����ַ�������ʹ��վ�ѻ���

**�ɹ���Ա�ֶ�** - ����Ա����ʹ��`jconsole`��������������һЩJMX�������ֶ�ʹ�ض�վ���ѻ��� ��ǳ����ã��������ڼƻ��ж�ʱ��ʹ��`jconsole`��CLI�����������ӵ�`jdg1`��������ʹ`site2`�ѻ��� �й��ⷽ��ĸ�����ϸ��Ϣ����μ�[JDG�ĵ�](https://access.redhat.com/documentation/en-us/red_hat_data_grid/7.3/html/red_hat_data_grid_user_guide/x_site_replication#taking_a_site_offline)��

> ͨ����Ҫ��[SYNC��ASYNC����](https://www.keycloak.org/docs/latest/server_installation/index.html#backups)���ᵽ������Keycloak����ִ����Щ���衣 

**�Զ�** - ����һ��������ʧ�ܱ��ݺ�`site2`ͨ�����Զ��ѻ��� ����ͨ����[Infinispan����������](https://www.keycloak.org/docs/latest/server_installation/index.html#jdgsetup)�����õĻ��������е�`take-offline`Ԫ�ص���������ɵġ�

```xml
<take-offline min-wait="60000" after-failures="3" />
```

���ʾ����ʾ�������60����������3����������ʧ�ܣ�����û���κγɹ����ݣ���ô�����ض��ĵ������棬վ�㽫�Զ��ѻ���

�Զ�ʹվ���ѻ��Ƿǳ����õģ��ر��ǵ�վ��֮��������ж��Ǽƻ���ġ� ȱ���ǣ��ڼ�⵽�����ж�֮ǰ������һЩʧ�ܵı��ݣ���Ҳ������ζ��Ӧ�ó���˳��ֹ��ϡ� ���磬ĳЩ�û��ĵ�¼ʧ�ܻ��¼��ʱ�ܳ��� �ر������ʹ��ֵΪ `FAIL` �� `failure-policy`��

> ÿ�����涼�ᵥ������վ���Ƿ����ѻ�״̬�� 

����վ����

һ���������ָ��ˣ�`site1` �� `site2` ���Ի��̸ཻ���������Ҫ����վ���ߡ�����Ҫͨ��JMX��CLI�ֶ���ɣ�����������ʹվ���ѻ���ͬ������������Ҫ������л��沢������������

һ����վ���ߣ�ͨ�����:

- ��[״̬ת��](https://www.keycloak.org/docs/latest/server_installation/index.html#statetransfer)��
- �ֶ�[�������](https://www.keycloak.org/docs/latest/server_installation/index.html#clearcache)��

#### 3.4.11. ״̬ת�� {#}

����ת���Ǳ�����ֶ����衣 Infinispan�����������Զ�ִ�д˲����������������ڼ䣬ֻ�й���Ա���Ծ����ĸ�վ�������ѡ�����Ƿ���Ҫ������վ��֮��˫�����״̬ת�ƣ�����ֻ�ǵ�����У���ͬ������`site1 `��`site2`�������Ǵ�`site2`��`site1`��

˫��״̬ת�ƽ�ȷ��`site1`�ϵ�����**��**������ʵ�屻ת�Ƶ�`site2`�ϡ� �ⲻ�����⣬��Ϊ������`site2`�ϻ������ڡ� ���Ƶأ���`site2`������**��**������ʵ�彫��ת�Ƶ�`site1`�ϡ� ����������Ĳ�������Щ������վ���ϵ�����**֮ǰ**���ڲ���������վ���ϵ������ڼ���µ�ʵ�塣 �������������ʱ������һ��վ�㽫**ʤ��**�������ǵڶ���վ���������ڼ���ɵĸ��¡�

���ҵ��ǣ�û���κ�ͨ�õĽ�������� ���Ѻ������ж�ֻ��״̬��ͨ��������100%��ȷ�ش���վ��֮��100%һ�µ����ݡ� ��Keycloak���ԣ���ͨ������һ���ؼ����⡣ ���������£��û���Ҫ���µ�¼�����ǵĿͻ��ˣ������в���ȷ��loginFailures��������ǿ�������� �й���δ������Եĸ�����ʾ�������Infinispan/JGroups�ĵ���

״̬ת��Ҳ����ͨ��JMX��Infinispan����������ɡ� ����������`pushState`�� ����û����������������״̬��ȡ������״̬�ȡ� �й�״̬ת�Ƶĸ�����Ϣ�������[Infinispan docs](https://access.redhat.com/documentation/en-us/red_hat_data_grid/7.3/html/red_hat_data_grid_user_guide/x_site_replication#pushing_state_transfer_to_sites)��

#### 3.4.12. ������� {#}

������֮�󣬿��԰�ȫ����Keycloak�������̨���ֶ�������档 ������Ϊ��`site1`�ϵ����ݿ��п��ܴ���һЩ���ݷ����˱仯���������ڸ��¼�������Ӧ�ñ���Ч�������������ڼ�û�б�ת�Ƶ�`site2`�� ��ˣ�`site2`�ϵ�Keycloak�ڵ������Ȼ���仺������һЩ�¾ɵ����ݡ�

Ҫ������棬�����[�������������](https://www.keycloak.org/docs/6.0/server_admin/#_clear-cache)��

������ָ�ʱ�������κ����վ���ϵ�һ��Keycloak�ڵ������������㹻�ˡ� ����ʧЧ�¼������͵�����վ���е���������Keycloak�ڵ㡣 ���ǣ���Ҫ�����л��棨�����û�����Կ��ִ�д˲����� �й���ϸ��Ϣ�������[�������������](https://www.keycloak.org/docs/6.0/server_admin/#_clear-cache)��

#### 3.4.13. ����JDG�������� {#}

���ڰ�������JDG����ļ��ɺ�ѡ�

����ʧ�ܲ���

Ĭ������£�JDG��`clustered.xml`�ļ���Infinispan���������еı���`failure-policy`���ü���Ϊ`FAIL`�� �����Ը�����Ҫ�������Ϊ`WARN`��`IGNORE`��

`FAIL`��`WARN`֮����������ڣ���ʹ��`FAIL`����Infinispan���������Խ����ݱ��ݵ���һ��վ�㲢�ұ���ʧ��ʱ��ʧ�ܽ������ص����ߣ�Keycloak���������� ���ݿ��ܻ�ʧ�ܣ���Ϊ�ڶ���վ����ʱ�޷����ʣ����ߴ��ڳ��Ը���ͬһʵ��Ĳ������� ����������£�Keycloak�����������Ըò������Ρ� ���ǣ��������ʧ�ܣ����û����ܻ��ڸ����ĳ�ʱ�󿴵�����

ʹ��`WARN`ʱ��ʧ�ܵı��ݲ����Infinispan������������Keycloak�������� �û������������󣬽�����ʧ�ܵı��ݡ� ����һ���϶̵ĳ�ʱ��ͨ��Ϊ10�룬��Ϊ���Ǳ��ݵ�Ĭ�ϳ�ʱ�� ������ͨ��`backup`Ԫ�ص�����`timeout`���ı䡣 �������ԡ� Infinispan��������־��ֻ�����һ��WARNING��Ϣ��

Ǳ�ڵ������ǣ���ĳЩ����£�վ��֮�����ֻ��һЩ���ݵ������жϣ��������ԣ�ʹ��`FAIL`���ԣ������������������ʹ��`WARN`�������ԣ��������� վ����һЩ���ݲ�һ�¡� �������������վ����ͬʱ����ͬһʵ�壬Ҳ�ᷢ�����������

��Щ��һ���ж���⣿ ͨ��ֻ��ʾ�û���Ҫ���½��������֤��

��ʹ��`WARN`����ʱ�����ܻᷢ����`actionTokens`�����ṩ��������ض���Կ��һ���Ի���ʵ�����ǵ���ʹ�ã������ܡ��ɹ�������д����ͬ����Կ�� ���ǣ����磬OAuth2�淶[�ἰ](https://tools.ietf.org/html/rfc6749#section-10.5)�ô�������ǵ�һʹ�õġ� ʹ��`WARN`���ԣ������޷��ϸ�֤���������������վ����ͬʱд����ͬ�Ĵ��룬�����д������ͬ�Ĵ��롣

����нϳ��������жϻ����ԣ���ôͬʱʹ��`FAIL`��`WARN`������վ�㽫��һ��ʱ���ʧЧ����[ʹվ�����ߺ�����](https://www.keycloak.org/docs/latest/server_installation/index.html#onoffline)�������� ʹ��Ĭ�ϵ�1���ӳ�ʱ��ͨ����Ҫ1-3���Ӳ���ʹ������صĻ����ѻ��� ֮�󣬴������û��ĽǶ����������в������������������� ��[��վ���ߺ�����](https://www.keycloak.org/docs/latest/server_installation/index.html#onoffline)����������ֻ������վ��������ʱ�ֶ��ָ�����վ��

��֮�������ϣ��վ��֮��Ƶ��������ʱ����жϣ����������Խ���һЩ���ݲ�һ���Ҳ���100��׼ȷ��һ���Ի��棬��������ϣ�������û���������ͳ�ʱ�䳬ʱ����ô �л���`WARN`��

`WARN`��`IGNORE`֮����������ڣ�`IGNORE`���治��д��JDG��־�С� �����Infinispan�ĵ��еĸ�����ϸ��Ϣ��

Lock acquisition timeout (������ȡ��ʱ)

Ĭ����������NON_DURABLE_XAģʽ��ʹ�����񣬻�ȡ��ʱΪ0.����ζ�����ͬһ����Կ���ڽ�����һ�����������񽫿���ʧ�ܡ�

�����л�Ϊ0������Ĭ��10���ԭ����Ϊ�˱�����ܵ��������⡣ ʹ��Keycloak�����ܻᷢ��ͬһʵ�壨ͨ���ǻỰʵ���loginFailure��������վ��ͬʱ���¡� ����ܻ���ĳЩ����µ����������⽫����������ֹ10�롣 �й���ϸ��Ϣ�������[��JIRA����](https://issues.jboss.org/browse/JDG-1318)��

�����ʱΪ0������������ʧ�ܣ���������˾���ֵ`FAIL`�ı���`failure-policy`���򽫴�Keycloak���Ը����� ֻҪ�ڶ�������������ɣ�����ͨ���ͻ�ɹ�������ʵ�彫����������������Ӧ�ø��¡�

���ǿ���ʹ�ô����ý��в��������һ���Ժͽ���ǳ��ã����鱣������

Ψһ���ǹ��ܣ�������Infinispan��������־�е��쳣��ÿ������������ʱ���ᷢ����

#### 3.4.14. ͬ�����첽���� {#}

`backup`Ԫ�ص�һ����Ҫ������`strategy`���ԡ� ����������Ƿ���Ҫ`SYNC`��`ASYNC`�� ������7������֧�ֿ��������ĸ��ƵĻ��棬��Щ�����������Ϊ3�ֲ�ͬ�Ľ���ֱ��ģʽ��

1. ͬ�� ����
2. �첽 ����
3. ������

���ʹ��`SYNC`���ݣ��򱸷���ͬ���ģ������ڵڶ���վ���ϴ����ݺ󣬵����ߣ�Keycloak���������˵Ĳ���������Ϊ����ɡ� ���`ASYNC`�����ܸ������һ���棬��ȷ����`site2`�϶��ض�ʵ�壨���û��Ự���ĺ�����ȡ����`site1`�п������¡� ���⣬�������Ҫ����һ���ԣ�����Ҫ���� ��`ASYNC`һ����������ݵ�����վ��ʧ�ܣ��򲻻�֪ͨ�����ߡ�

����ĳЩ���棬�������ܸ��������б��ݲ���ȫ����������д��Infinispan�������� Ҫ���д����ã��벻Ҫ��`remote-store`Ԫ������Keycloak�˵��ض����� (�ļ� `KEYCLOAK_HOME/standalone/configuration/standalone-ha.xml`) ��Ȼ��ʹ���ض���`replicated-cache`Ԫ�ء� ��Infinispan��������Ҳ����Ҫ��

Ĭ������£�����7�����涼������`SYNC`���ݣ������ȫ��ѡ� ������һЩ��Ҫ���ǵ����

- �����ʹ�õ�������/����ģʽ������Keycloak���������ڵ�վ��`site1`�У���`site2`�е�Infinispan���������������ݡ������[ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#modes)�Ի�ȡ������ϸ��Ϣ����Ȼ��ͨ������ʹ�����л����`ASYNC`�������������ܡ�
- `work`������Ҫ����������վ�㷢��һЩ��Ϣ�����绺��ʧЧ�¼��� ��������ȷ��ĳЩ�����¼�,����userStorageͬ��;���ڵ���վ���Ϸ����� ���齫�����ñ���Ϊ`SYNC��
- `actionTokens`��������һ���Ի��棬���ڸ���ĳЩ����/Ʊ֤��ʹ��һ�Ρ� ���磬�������ƻ�OAuth2���롣 ���Խ�������Ϊ`ASYNC`����΢������ܣ����ǲ��ܱ�֤�ض�Ʊ֤����ǵ���ʹ�á� ���磬�������վ����ͬʱ����ͬһƱ֤������ô�������󶼿��ܳɹ�ʹ��`ASYNC`���ԡ� ���������������õĽ�ȡ�������Ƿ��ϲ�����õİ�ȫ�ԣ�`SYNC`���ԣ�����õ����ܣ�`ASYNC`���ԣ���
- `loginFailures`���������3��ģʽ�е��κ�һ����ʹ�á� �������û�б��ݣ�����ζ��ÿ��վ�㽫���������û��ĵ�¼ʧ�ܴ����������[Infinispan����](https://www.keycloak.org/docs/latest/server_installation/index.html#cache)�˽����飩�� �����һЩ��ȫ��������������һЩ�������ơ� ���⣬�������Խ��;ܾ�����DoS�������ķ��ա� ���磬���������ʹ������վ���ϵ��û����û���������ģ��1000��������������ζ����վ��֮�䴫�ݴ�����Ϣ������ܵ�������ӵ���� `ASYNC`���Կ��ܸ���⣬��Ϊ�ȴ����ݵ�����վ�㲻����ֹ���������󣬴Ӷ����¿��ܸ���ӵ�������������� ʹ��`ASYNC`���ԣ���¼ʧ�ܵĴ���Ҳ��׼ȷ��

������������֮�������ٶȽ�����DoS���ʽϵ͵Ļ��������鲻Ҫ����`loginFailures`���档

- ������`SYNC`�б���`sessions`��`clientSessions`���档 ֻ�е���ȷ���û�����ͷ���ͨ�����󣨴�[������](https://www.keycloak.org/docs/latest/server_installation/index.html#requestprocessing)�������Ŀͻ���Ӧ�ó���Keycloak������ʱ���ſ��Խ������л�Ϊ`ASYNC`����ʼ����ͬһվ���ϴ��� ���磬�����

  - ��ʹ������/����ģʽ����[ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#modes)������

  - �������пͻ���Ӧ�ó���ʹ��Keycloak [JavaScript Adapter](https://www.keycloak.org/docs/latest/securing_apps/index.html#_javascript_adapter)�� JavaScript��������������з��ͷ���ͨ������������ǲ��������ճ�ԻỰ������������û������������������ͬ��Ⱥ���ڵ㣨�����ͬһվ���ϣ�������

  - ���ĸ��ؾ������ܹ����ݿͻ���IP��ַ��λ�ã��ṩ���󣬲�������վ���ϲ���ͻ���Ӧ�ó���

    ���磬����2��վ��LON��NYC�� ֻҪ����Ӧ�ó���Ҳ������LON��NYCվ���У����Ϳ���ȷ�������׶��û��������û����󽫱��ض���LONվ���е�Ӧ�ó����Լ�LONվ���е�Keycloak�������� ����LONվ��ͻ��˲����Backchannel����Ҳ����LONվ���е�Keycloak�������Ͻ����� ��һ���棬���������û�������Keycloak����Ӧ�ó�������ͷ���ͨ��������NYCվ���ϴ���

- ����`offlineSessions`��`offlineClientSessions`���������Ƶģ���֮ͬ�����ڣ��������δ�ƻ�Ϊ�κοͻ���Ӧ�ó���ʹ���ѻ����ƣ����������Ҫ�������ǡ�

һ����˵������������ʲ������ܲ��ʺ�������ô�����汣����`SYNC`�����л����ȫ��

> �����л���SYNC/ASYNC���ݣ���ȷ���༭`backup`Ԫ�ص�`strategy`���ԡ� ���������� 

```xml
<backup site="site2" failure-policy="FAIL" strategy="ASYNC" enabled="true">
```

ע��cache-configurationԪ�ص�`mode`���ԡ�

#### 3.4.15. �����ų� {#}

������ʾּ�ڰ�����������⣺

- ����ͨ��[��������](https://www.keycloak.org/docs/latest/server_installation/index.html#setup)������ʹ�ô˹��ߣ��Ա��������������˽� ������ �Ķ���ƪ�ĵ����˽�����Ҳ������֮�١�

- ����[Infinispan����������](https://www.keycloak.org/docs/latest/server_installation/index.html#jdgsetup)�е�˵������Infinispan��jconsole��Ⱥ״̬��GMS����JGroups״̬��RELAY���� ������鿴��������Ԥ�ڣ���ô����ܿ��ܳ���Infinispan�������������ϡ�

- ����Keycloak����������Ӧ���ڷ����������ڼ俴����������Ϣ��

  ```
  18:09:30,156 INFO  [org.keycloak.connections.infinispan.DefaultInfinispanConnectionProviderFactory] (ServerService Thread Pool -- 54)
  Node name: node11, Site name: site1
  ```

  ��Keycloak�����������ڼ���վ�����ƺͽڵ������Ƿ���Ԥ��һ�¡�

- ���Keycloak�������Ƿ�Ԥ��λ�ڼ�Ⱥ�У�����ֻ������ͬһ�������ĵ�Keycloak�������˴��ڼ�Ⱥ�С� ��Ҳ����ͨ��GMS��ͼ��JConsole�н��м�顣 �й�������ϸ��Ϣ�������[��Ⱥ���ѽ��](https://www.keycloak.org/docs/6.0/server_installation/#troubleshooting)��

- ���������Keycloak�������ڼ����쳣��������ʾ��

  ```
  17:33:58,605 ERROR [org.infinispan.client.hotrod.impl.operations.RetryOnFailureOperation] (ServerService Thread Pool -- 59) ISPN004007: Exception encountered. Retry 10 out of 10: org.infinispan.client.hotrod.exceptions.TransportException:: Could not fetch transport
  ...
  Caused by: org.infinispan.client.hotrod.exceptions.TransportException:: Could not connect to server: 127.0.0.1:12232
  	at org.infinispan.client.hotrod.impl.transport.tcp.TcpTransport.<init>(TcpTransport.java:82)
  ```

  ��ͨ����ζ��Keycloak�������޷������Լ����������ĵ�Infinispan�������� ȷ����Ԥ�����÷���ǽ�����ҿ�������Infinispan��������

- ���������Keycloak�������ڼ����쳣��������ʾ��

  ```
  16:44:18,321 WARN  [org.infinispan.client.hotrod.impl.protocol.Codec21] (ServerService Thread Pool -- 57) ISPN004005: Error received from the server: javax.transaction.RollbackException: ARJUNA016053: Could not commit transaction.
   ...
  ```

  Ȼ������վ�����ӦInfinispan����������־��������Ƿ�δ�ܱ��ݵ�����վ�㡣 �������վ�㲻���ã����齫���л�Ϊ�ѻ����Ա�Infinispan���������᳢�Ա��ݵ��ѻ�վ�㣬�Ӷ����²���Ҳ��Keycloak�������˳ɹ�ͨ���� �й���ϸ��Ϣ�������[����DC�������](https://www.keycloak.org/docs/latest/server_installation/index.html#administration)��

- ����ͨ��JMX��õ�Infinispanͳ����Ϣ�� ���磬���Ե�¼��Ȼ��鿴�»Ự�Ƿ��ѳɹ�д������Infinispan�����������������`sessions`�����п��á� �����ͨ�����MBean��`sessions`�����е�Ԫ������������`jboss.datagrid-infinispan:type=Cache,name="sessions(repl_sync)",manager="clustered",component=Statistics`������`numberOfEntries`�� ��¼������վ���ϵ�����Infinispan�������϶�Ӧ����һ��`numberOfEntries`��Ŀ��

- ����[Keycloak����������](https://www.keycloak.org/docs/latest/server_installation/index.html#serversetup)��������DEBUG��־��¼�� ���磬�������¼������Ϊ�»Ự�ڵڶ���վ���ϲ����ã�����ü��Keycloak��������־������Ƿ���[Keycloak����������](https://www.keycloak.org/docs/latest/server_installation/index.html#serversetup)�е�˵���������������� �������֪������Ҫ��keycloak-user�ʼ��б���ѯ�ʣ���ô�ӵ����ʼ��е������������ĵ�Keycloak������������־�ļ�����а����� ����־Ƭ����ӵ��ʼ�����־����ĳ�����ڵ����ʼ����������ǡ�

- �������`site1`�ϵ�Keycloak�������ϸ�����ʵ�壬����`user`��������û����`site2`�ϵ�Keycloak�������Ͽ�����ʵ����£���ô����������ڸ���ͬ�����ݿⱾ�� ��Keycloak����δ��ȷ��Ч�� �����Գ�����ʱ����Keycloak���棬��[here](https://www.keycloak.org/docs/6.0/server_installation/#disabling-caching)��������ȷ�������Ƿ������ݿ⸴�Ƽ��� ���⣬�ֶ����ӵ����ݿⲢ��������Ƿ�Ԥ�ڸ��¿��ܻ����������� �����ض���ÿ�����ݿ�ģ��������Ҫ�������ݿ���ĵ���

- ��ʱ�����ܻ���Infinispan��������־�п������������ص��쳣��

  ```
  (HotRodServerHandler-6-35) ISPN000136: Error executing command ReplaceCommand,
  writing keys [[B0x033E243034396234..[39]]: org.infinispan.util.concurrent.TimeoutException: ISPN000299: Unable to acquire lock after
  0 milliseconds for key [B0x033E243034396234..[39] and requestor GlobalTx:jdg1:4353. Lock is held by GlobalTx:jdg1:4352
  ```

  ��Щ���ⲻһ���Ǹ����⡣ ���ǿ������κ�ʱ��������DC�ϴ���ͬһʵ��Ĳ����༭ʱ������ ���ڲ����кܳ����� ͨ����Keycloak���������յ��й�ʧ�ܲ�����֪ͨ���������ԣ���˴��û��ĽǶ�������ͨ��û���κ����⡣

- ���Keycloak�����������ڼ����쳣��������ʾ��

  ```
  16:44:18,321 WARN  [org.infinispan.client.hotrod.impl.protocol.Codec21] (ServerService Thread Pool -- 55) ISPN004005: Error received from the server: java.lang.SecurityException: ISPN000287: Unauthorized access: subject 'Subject with principal(s): []' lacks 'READ' permission
   ...
  ```

  ��Щ��־��Ŀ��Keycloak�Զ����Infinispan�Ƿ���Ҫ�����֤�Ľ����������ζ����Ҫ���������֤�� ��ʱ����ע�⵽�������ɹ��������������԰�ȫ�غ�����Щ��������޷������� ����������޷���������ȷ���Ѱ���[Infinispan����������](https://www.keycloak.org/docs/latest/server_installation/index.html#jdgsetup)�е�˵����ȷ����Infinispan���������֤�� Ҫ��ֹ��������־��Ŀ������ͨ����`spi=connectionsInfinispan/provider=default`�����н�`remoteStoreSecurityEnabled`��������Ϊ`true`��ǿ�ƽ��������֤��

  ```xml
  <subsystem xmlns="urn:jboss:domain:keycloak-server:1.1">
      ...
      <spi name="connectionsInfinispan">
          ...
          <provider name="default" enabled="true">
              <properties>
                  ...
                  <property name="remoteStoreSecurityEnabled" value="true"/>
              </properties>
          </provider>
      </spi>
  ```

- ���������ʹ��Keycloak������Ӧ�ó�����������֤���������֤ʧ�ܲ���������д������޴��ض��򣬲�������Keycloak��������־�п������´���

  ```
  2017-11-27 14:50:31,587 WARN  [org.keycloak.events] (default task-17) type=LOGIN_ERROR, realmId=master, clientId=null, userId=null, ipAddress=aa.bb.cc.dd, error=expired_code, restart_after_timeout=true
  ```

  �������ζ�����ĸ��ؾ�������Ҫ����Ϊ֧��ճ�ԻỰ�� ȷ��������Keycloak��������Property`jboss.node.name`���ڼ�ʹ�õ��ṩ��·�����ư������ؾ��������������ڱ�ʶ��ǰ����������ȷ���ơ�

- ���Infinispan`work`�������������������ܻ�����[��Infinispan����](https://issues.jboss.org/browse/JDG-987)�������ɻ�����δ��ȷ��������ġ� ����������£�ʹ�ÿյ�`<expiration />`��Ǹ��»���������������ʾ��

  ```xml
      <replicated-cache name="work" configuration="sessions-cfg">
          <expiration />
      </replicated-cache>
  ```

- �������Infinispan��������־�п������棬���磺

  ```
  18:06:19,687 WARN  [org.infinispan.server.hotrod.Decoder2x] (HotRod-ServerWorker-7-12) ISPN006011: Operation 'PUT_IF_ABSENT' forced to
    return previous value should be used on transactional caches, otherwise data inconsistency issues could arise under failure situations
  18:06:19,700 WARN  [org.infinispan.server.hotrod.Decoder2x] (HotRod-ServerWorker-7-10) ISPN006010: Conditional operation 'REPLACE_IF_UNMODIFIED' should
    be used with transactional caches, otherwise data inconsistency issues could arise under failure situations
  ```

  ����Ժ������ǡ� Ϊ�˱��⾯�棬Infinispan�������˵Ļ�����Ը���Ϊ���񻺴棬�����Ƽ�����������Ϊ�����ܵ�����bug���������һЩ����<https://issues.jboss.org/browse/ISPN-9323>�� �������ڣ�����ֻ��Ҫ�����ԡ�

- �������Infinispan��������־�п����������磺

  ```
  12:08:32,921 ERROR [org.infinispan.server.hotrod.CacheDecodeContext] (HotRod-ServerWorker-7-11) ISPN005003: Exception reported: org.infinispan.server.hotrod.InvalidMagicIdException: Error reading magic byte or message id: 7
  	at org.infinispan.server.hotrod.HotRodDecoder.readHeader(HotRodDecoder.java:184)
  	at org.infinispan.server.hotrod.HotRodDecoder.decodeHeader(HotRodDecoder.java:133)
  	at org.infinispan.server.hotrod.HotRodDecoder.decode(HotRodDecoder.java:92)
  	at io.netty.handler.codec.ByteToMessageDecoder.callDecode(ByteToMessageDecoder.java:411)
  	at io.netty.handler.codec.ByteToMessageDecoder.channelRead(ByteToMessageDecoder.java:248)
  ```

  ��������Keycloak��־�п���һЩ���ƵĴ��������Ա�������ʹ�õ�HotRodЭ��İ汾�����ݡ� �������Խ�Keycloak��JDG 7.2��������ɰ汾��Infinispan������һ��ʹ��ʱ�����ܻᷢ����������� �����`protocolVersion`������Ϊ����������ӵ�Keycloak�����ļ��е�`remote-store`Ԫ�أ��������������� ���磺

  ```
  <property name="protocolVersion">2.6</property>
  ```

## 4. ������ϵͳ���� {#}

Keycloak�ĵͼ�������ͨ���༭���а��е�`standalone.xml`��`standalone-ha.xml`��`domain.xml`�ļ�����ɵġ� ���ļ���λ��ȡ��������[����ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_operating-mode)��

��Ȼ�������ڴ������������ã������ڽ��ص���� *keycloak-server* ��ϵͳ�����á� ������ʹ���ĸ������ļ���*keycloak-server* ��ϵͳ�����ö�����ͬ�ġ�

keycloak-server��ϵͳͨ�����ļ�ĩβ������������ʾ��

```xml
<subsystem xmlns="urn:jboss:domain:keycloak-server:1.1">
   <web-context>auth</web-context>
   ...
</subsystem>
```

��ע�⣬����������������֮ǰ������ϵͳ�е��κθ��Ķ�������Ч��

### 4.1. ����SPI�ṩ���� {#}

ÿ���������õ�ϸ���ڸ����õ��������е������ط����ۡ� ���ǣ��˽�������SPI�ṩ�������������õĸ�ʽ�����á�

Keycloak��һ���߶�ģ�黯��ϵͳ�����кܴ������ԡ� �г���50�������ṩ����ӿڣ�SPI���������Խ���ÿ��SPI��ʵ�֡� SPI��ʵ�ֳ�Ϊ*�ṩ��*��

SPI�����е�����Ԫ�ض��ǿ�ѡ�ģ���������SPI����������ʾ��

```xml
<spi name="myspi">
    <default-provider>myprovider</default-provider>
    <provider name="myprovider" enabled="true">
        <properties>
            <property name="foo" value="bar"/>
        </properties>
    </provider>
    <provider name="mysecondprovider" enabled="true">
        <properties>
            <property name="foo" value="foo"/>
        </properties>
    </provider>
</spi>
```

��������ΪSPI`myspi`�����������ṩ���� `default-provider`����Ϊ`myprovider`�� ������SPI��������δ���������á� ��ЩSPI�������ṩ�̣���Щ������ ����`default-provider`���԰���SPIѡ��

����ע�⣬ÿ���ṩ���򶼶������Լ���һ���������ԡ� ���������ṩ�̶���һ����Ϊ`foo`��������һ��ʵֻ���ɺϡ�

ÿ������ֵ���������ṩ������͡� ���ǣ���һ�����⡣ ����`eventsStore`  SPI �� `jpa` �ṩ����

```xml
<spi name="eventsStore">
    <provider name="jpa" enabled="true">
        <properties>
            <property name="exclude-events" value="[&quot;EVENT1&quot;,
                                                    &quot;EVENT2&quot;]"/>
        </properties>
    </provider>
</spi>
```

���ǿ���ֵ�Է����ſ�ͷ�ͽ�β�� ����ζ�Ÿ�ֵ����Ϊ�б��ݸ��ṩ���� �ڴ�ʾ���У�ϵͳ�����ṩ���򴫵�һ����������Ԫ��ֵ *EVENT1* �� *EVENT2* ���б� Ҫ���б�����Ӹ���ֵ��ֻ��ʹ�ö��ŷָ�ÿ���б�Ԫ�ؼ��ɡ� ���ҵ��ǣ�����Ҫʹ�� `��quot;` ��ת��ÿ���б�Ԫ����Χ�����š�

### 4.2. ����WildFly CLI {#}

�����ֶ��༭�����⣬��������ͨ�� *jboss-cli* ���߷����������������á� CLI�������ڱ��ػ�Զ�����÷������� ����ű����ʹ��ʱ�����������á�

Ҫ����WildFly CLI������Ҫ����`jboss-cli`��

Linux/Unix

```bash
$ .../bin/jboss-cli.sh
```

Windows

```bat
> ...\bin\jboss-cli.bat
```

�⽫��������������ʾ��

��ʾ

```
[disconnected /]
```

�����ϣ�����������еķ�������ִ�����������ִ��`connect`���

����

```
[disconnected /] connect
connect
[standalone@localhost:9990 /]
```

����ܻ��룬����û�������κ��û��������룡���� ����������ж��������������������ͬһ̨�����������`jboss-cli`�����������ʻ������ʵ����ļ�Ȩ�ޣ����������û��������Ա�û��������롣 �����[* WildFly 16�ĵ�*](http://docs.wildfly.org/16/Admin_Guide.html)���˽�������Ը����øе������ʱ���ʹ�������ȫ�ĸ�����ϸ��Ϣ��

### 4.3. CLIǶ��ʽģʽ {#}

��������������������λ��ͬһ̨������ϣ�������ϣ���ڷ�����δ���ڻ״̬ʱ�����������Խ�������Ƕ��CLI���ڲ����������������ģʽ�½��и��ġ� Ϊ�ˣ�����ʹ����Ҫ���ĵ������ļ�ִ��`embed-server`���

embed-server (Ƕ�������)

```
[disconnected /] embed-server --server-config=standalone.xml
[standalone@embedded /]
```

### 4.4. CLI GUIģʽ {#}

CLIҲ������GUIģʽ�����С� GUIģʽ����SwingӦ�ó�����������ͼ�η�ʽ�鿴�ͱ༭ *running* ����������������ģ�͡� ������Ҫ������ʽ��CLI����˽����ѡ��ʱ��GUIģʽ�ر����á� GUI�����Դӱ��ػ�Զ�̷�����������������־��

��GUIģʽ��ʼ

```bash
$ .../bin/jboss-cli.sh --gui
```

*ע��: Ҫ���ӵ�Զ�̷���������Ҫ����--connectѡ� ʹ��--helpѡ��ɻ�ȡ������ϸ��Ϣ��*

����GUIģʽ����������Ҫ���¹��������ҵ��ڵ� `subsystem=keycloak-server` �� ����Ҽ������ýڵ㲢����  `Explore subsystem=keycloak-server` ���������һ������ʾkeycloak-server��ϵͳ����ѡ���

![cli gui](assets/cli-gui.png)

### 4.5. CLI�ű� {#}

CLI���й㷺�Ľű����ܡ� �ű�ֻ��һ������CLI������ı��ļ��� ����һ���ر������ģ�建��ļ򵥽ű���

turn-off-caching.cli

```
/subsystem=keycloak-server/theme=defaults/:write-attribute(name=cacheThemes,value=false)
/subsystem=keycloak-server/theme=defaults/:write-attribute(name=cacheTemplates,value=false)
```

Ҫִ�нű����ҿ��԰���CLI GUI�е�`Scripts`�˵������ߴ�������ִ�нű���������ʾ��

```bash
$ .../bin/jboss-cli.sh --file=turn-off-caching.cli
```

### 4.6. CLIʳ�� {#}

������һЩ���������Լ����ʹ��CLI����ִ�����ǡ� ��ע�⣬�ڵ�һ��ʾ���е�����ʾ���У�����ʹ��ͨ���·�� `**` ��ʾ��Ӧ���滻keycloak-server��ϵͳ��·����

���ڶ���ģʽ������ζ��:

```
**` = `/subsystem=keycloak-server
```

������ģʽ������ζ�ţ�

```
**` = `/profile=auth-server-clustered/subsystem=keycloak-server
```

#### 4.6.1. ���ķ�������Web������ {#}

```
/subsystem=keycloak-server/:write-attribute(name=web-context,value=myContext)
```

#### 4.6.2. ����ȫ��Ĭ������ {#}

```
**/theme=defaults/:write-attribute(name=default,value=myTheme)
```

#### 4.6.3. ����µ�SPI���ṩ���� {#}

```
**/spi=mySPI/:add
**/spi=mySPI/provider=myProvider/:add(enabled=true)
```

#### 4.6.4. �����ṩ�� {#}

```
**/spi=mySPI/provider=myProvider/:write-attribute(name=enabled,value=false)
```

#### 4.6.5. ����SPI��Ĭ���ṩ���� {#}

```
**/spi=mySPI/:write-attribute(name=default-provider,value=myProvider)
```

#### 4.6.6. ����dblock SPI {#}

```
**/spi=dblock/:add(default-provider=jpa)
**/spi=dblock/provider=jpa/:add(properties={lockWaitTimeout => "900"},enabled=true)
```

#### 4.6.7. Ϊ�ṩ����ӻ���ĵ�������ֵ {#}

```
**/spi=dblock/provider=jpa/:map-put(name=properties,key=lockWaitTimeout,value=3)
```

#### 4.6.8. ���ṩ������ɾ���������� {#}

```
**/spi=dblock/provider=jpa/:map-remove(name=properties,key=lockRecheckTime)
```

#### 4.6.9. ������Ϊ`List`���ṩ��������������ֵ {#}

```
**/spi=eventsStore/provider=jpa/:map-put(name=properties,key=exclude-events,value=[EVENT1,EVENT2])
```

## 5. Profiles (�����ļ�) {#}

Keycloak�е�ĳЩ����Ĭ�������δ���ã���Щ���ܰ�������ȫ֧�ֵĹ��ܡ� ���⣬Ĭ������»�����һЩ���ܣ������Խ�����Щ���ܡ�

�������úͽ��õĹ��ܰ�����

| ����                     | ����                                  | Ĭ������ | ֧�ּ��� |
| :----------------------- | :------------------------------------------- | :----------------- | :------------ |
| account2                 | New Account Management Console               | No                 | Experimental  |
| account_api              | Account Management REST API                  | No                 | Preview       |
| admin_fine_grained_authz | Fine-Grained Admin Permissions               | No                 | Preview       |
| authz_drools_policy      | Drools Policy for Authorization Services     | No                 | Preview       |
| docker                   | Docker Registry protocol                     | No                 | Supported     |
| impersonation            | Ability for admins to impersonate users      | Yes                | Supported     |
| openshift_integration    | Extension to enable securing OpenShift       | No                 | Preview       |
| script                   | Write custom authenticators using JavaScript | Yes                | Preview       |
| token_exchange           | Token Exchange Service                       | No                 | Preview       |

Ҫ��������Ԥ�����ܣ���������������

```bash
bin/standalone.sh|bat -Dkeycloak.profile=preview
```

������ͨ������ģʽ��Ϊ`server-one`�����ļ�`standalone/configuration/profile.properties`����`domain/servers/server-one/configuration/profile.properties`���������������� ������������ӵ��ļ��У�

```properties
profile=preview
```

Ҫ�����ض����ܣ���������������

```bash
bin/standalone.sh|bat -Dkeycloak.profile.feature.<feature name>=enabled
```

���磬Ҫ����Docker����ʹ��`-Dkeycloak.profile.feature.docker=enabled`��

������ͨ���������������`profile.properties`�ļ���������������

```properties
feature.docker=enabled
```

Ҫ�����ض����ܣ���������������

```bash
bin/standalone.sh|bat -Dkeycloak.profile.feature.<feature name>=disabled
```

���磬Ҫ����ģ�⣬��ʹ��`-Dkeycloak.profile.feature.impersonation=disabled`��

������ͨ���������������`profile.properties`�ļ���������������

```properties
feature.impersonation=disabled
```

## 6. ��ϵ���ݿ����� {#}

Keycloak�������Լ��Ļ���Java��Ƕ��ʽ��ϵ���ݿ�H2�� ����Keycloak���ڱ������ݵ�Ĭ�����ݿ⣬�Ա������Կ��伴�õ����������֤�������� ����ǿ�ҽ�����ʹ�ø��������������ⲿ���ݿ��滻���� H2���ݿ��ڸ߲�������²��Ǻܿ��У�Ҳ��Ӧ���ڼ�Ⱥ��ʹ�á� ���µ�Ŀ��������չʾ��ν�Keycloak���ӵ�����������ݿ⡣

Keycloakʹ�����ֲַ㼼�����־ñ������ϵ���ݡ� �ײ㼼����JDBC�� JDBC��һ���������ӵ�RDBMS��Java API�� ÿ�����ݿ����Ͷ��в�ͬ��JDBC�������������ݿ⹩Ӧ���ṩ�� ���������������Keycloak��ʹ����Щ�ض��ڹ�Ӧ�̵���������֮һ��

���ڳ־��ԵĶ��㼼����Hibernate JPA�� ���ǽ�Java����ӳ�䵽��ϵ���ݵĹ�ϵӳ��API�Ķ��� Keycloak�Ĵ󲿷ֲ�����Զ���ᴥ��Hibernate�����÷��棬�����ǽ���������������ֺ�������������������һ�㡣

> �� *WildFly 16�ĵ�* ��[����Դ�����½�](http://docs.wildfly.org/16/Admin_Guide.html#DataSource)�и�ȫ��ؽ���������Դ���á�

### 6.1. RDBMS�����嵥 {#}

������ΪKeycloak����RDBMS����ִ�еĲ��衣

1. �ҵ����������ݿ��JDBC��������
2. ����������JAR�����ģ���в�����ģ�鰲װ����������
3. �ڷ������������ļ�������JDBC��������
4. �޸�����Դ������ʹ�����ݿ��JDBC��������
5. �޸�����Դ�����Զ������ݿ�����Ӳ���

���½�ʹ��PostgresQL��Ϊ������ʾ���� �������ݿ���ѭ��ͬ�İ�װ���衣

### 6.2. ���JDBC�������� {#}

���Ҳ�����RDBMS��JDBC��������JAR�� ��ʹ�ô���������֮ǰ�����뽫������ģ���в����䰲װ���������С� ģ�鶨����ص�Keycloak��·���е�JAR�Լ���ЩJAR������ģ���������ϵ�� �������������ǳ��򵥡�

��Keycloak���а�� *��/modules/* Ŀ¼�У�����Ҫ����һ��Ŀ¼�ṹ������ģ�鶨�塣 Լ����ʹ��JDBC���������Java��������ΪĿ¼�ṹ�����ơ� ����PostgreSQL������Ŀ¼ *org/postgresql/main* �� �����ݿ���������JAR���Ƶ���Ŀ¼�У��������д���һ���յ� *module.xml* �ļ���

ģ��Ŀ¼

![db module](assets/db-module.png)

��ɴ˲����󣬴� *module.xml* �ļ�����������XML��

ģ�� XML

```xml
<?xml version="1.0" ?>
<module xmlns="urn:jboss:module:1.3" name="org.postgresql">

    <resources>
        <resource-root path="postgresql-9.4.1212.jar"/>
    </resources>

    <dependencies>
        <module name="javax.api"/>
        <module name="javax.transaction.api"/>
    </dependencies>
</module>
```

ģ������Ӧ��ģ���Ŀ¼�ṹƥ�䡣 ���ԣ�*org/postgresql* ӳ�䵽`org.postgresql`�� `resource-root path`����Ӧָ�����������JAR�ļ����� �����ֻ���κ�JDBC��������JAR�����е�����������ϵ��

### 6.3. ����������JDBC�������� {#}

������Ҫ�����ǽ��´����JDBC�����������������������ļ��У��Ա��ڷ���������ʱ���ز���Ϊ���á� ִ�д˲�����λ��ȡ��������[����ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_operating-mode)�� ���Ҫ�ڱ�׼ģʽ�²�����༭*��/standalone/configuration/standalone.xml*�� ���Ҫ�Ա�׼Ⱥ��ģʽ���в�����༭*.../standalone/configuration/ standalone-ha.xml*�� ���Ҫ����ģʽ�²�����༭*.../domain/configuration/domain.xml*�� ����ģʽ�£�����Ҫȷ���༭����ʹ�õ������ļ���`auth-server-standalone`��`auth-server-clustered`

�������ļ��У�����`datasources`��ϵͳ�е�`drivers` XML�顣 ��Ӧ�ÿ���ΪH2 JDBC��������������Ԥ������������ ������Ϊ�ⲿ���ݿ�����JDBC��������ĵط���

JDBC ����

```xml
  <subsystem xmlns="urn:jboss:domain:datasources:5.0">
     <datasources>
       ...
       <drivers>
          <driver name="h2" module="com.h2database.h2">
              <xa-datasource-class>org.h2.jdbcx.JdbcDataSource</xa-datasource-class>
          </driver>
       </drivers>
     </datasources>
  </subsystem>
```

��`drivers` XML���У�����Ҫ����һ�������JDBC�������� ����Ҫһ��`name`�������ѡ���κ�����Ҫ�ġ� ��ָ��`module`���ԣ�������ָ����֮ǰΪ��������JAR������`module`���� ���������ָ�����������Java�ࡣ �����ǰ�װPostgreSQL���������ʾ��������������λ�ڱ���ǰ�涨���ģ��ʾ���С�

��������JDBC��������

```
  <subsystem xmlns="urn:jboss:domain:datasources:5.0">
     <datasources>
       ...
       <drivers>
          <driver name="postgresql" module="org.postgresql">
              <xa-datasource-class>org.postgresql.xa.PGXADataSource</xa-datasource-class>
          </driver>
          <driver name="h2" module="com.h2database.h2">
              <xa-datasource-class>org.h2.jdbcx.JdbcDataSource</xa-datasource-class>
          </driver>
       </drivers>
     </datasources>
  </subsystem>
```

### 6.4. �޸�Keycloak����Դ {#}

����JDBC��������󣬱����޸�Keycloak���ڽ������ӵ����ⲿ���ݿ����������Դ���á� ������ע��JDBC�����������ͬ�����ļ���XML����ִ�д˲����������������������ݿ�����ӵ�ʾ����

��������JDBC��������

```xml
  <subsystem xmlns="urn:jboss:domain:datasources:5.0">
     <datasources>
       ...
       <datasource jndi-name="java:jboss/datasources/KeycloakDS" pool-name="KeycloakDS" enabled="true" use-java-context="true">
           <connection-url>jdbc:postgresql://localhost/keycloak</connection-url>
           <driver>postgresql</driver>
           <pool>
               <max-pool-size>20</max-pool-size>
           </pool>
           <security>
               <user-name>William</user-name>
               <password>password</password>
           </security>
       </datasource>
        ...
     </datasources>
  </subsystem>
```

����`KeycloakDS`��`datasource`���塣 ��������Ҫ�޸�`connection-url`�� ��Ӧ�̵�JDBCʵ�ֵ��ĵ�Ӧָ��������URLֵ�ĸ�ʽ��

�����������㽫ʹ�õ�`driver`�� �������ڱ�����һ����������JDBC����������߼����ơ�

ÿ��Ҫִ������ʱ���������ݿ�������Ӷ��ܰ��� Ϊ�˲���������Դʵ��ά����һ���򿪵����ӳء� `max-pool-size`ָ���������������������� ������ϣ������ϵͳ���ظ��Ĵ�ֵ��

�������ʹ��PostgreSQL������Ҫ�������ӵ����ݿ���������ݿ��û��������롣 �����ܻᵣ��ʾ���е����������ġ� ��һЩ�������ԶԴ˽���ģ���������ⳬ���˱�ָ�ϵķ�Χ��

> �й�����Դ���ܵĸ�����Ϣ�������* WildFly 16�ĵ�*�е�[����Դ�����½�](http://docs.wildfly.org/16/Admin_Guide.html#DataSource)�� 

### 6.5. ���ݿ����� {#}

�����������λ�ڷ��а��е�`standalone.xml`��`standalone-ha.xml`��`domain.xml`�ļ��С� ���ļ���λ��ȡ��������[����ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_operating-mode)��

���ݿ�����

```xml
<subsystem xmlns="urn:jboss:domain:keycloak-server:1.1">
    ...
    <spi name="connectionsJpa">
     <provider name="default" enabled="true">
         <properties>
             <property name="dataSource" value="java:jboss/datasources/KeycloakDS"/>
             <property name="initializeEmpty" value="false"/>
             <property name="migrationStrategy" value="manual"/>
             <property name="migrationExport" value="${jboss.home.dir}/keycloak-database-update.sql"/>
         </properties>
     </provider>
    </spi>
    ...
</subsystem>
```

���ܵ�����ѡ���ǣ�

- dataSource

  DataSource��JNDI����

- jta

  boolean���ԣ�����ָ��datasource�Ƿ�֧��JTA

- driverDialect

  ���ݿⷽ�Ե�ֵ���ڴ��������£�������Ҫָ�������ԣ���ΪHibernate���Զ���ⷽ�ԡ�

- initializeEmpty

  ���Ϊ�����ʼ�����ݿ⡣ �������Ϊfalse��������ֶ���ʼ�����ݿ⡣ ���Ҫ�ֶ������ݿ⼯migrationStrategy��ʼ��Ϊ`manual`����������һ������SQL������ļ�����ʼ�����ݿ⡣ Ĭ��Ϊtrue��

- migrationStrategy

  ����Ǩ�����ݿ�Ĳ��ԡ� ��ЧֵΪ`update`��`manual`��`validate`�� Update���Զ�Ǩ�����ݿ�ܹ��� �ֶ���ʹ�ÿ������ݿ����ֶ�ִ�е�SQL���������ĵ������ļ��� ��֤��ֻ������ݿ��Ƿ������µġ�

- migrationExport

  ��д�ֶ����ݿ��ʼ��/Ǩ���ļ���λ�õ�·����

- showSql

  ָ��Hibernate�Ƿ�Ӧ�ڿ���̨����ʾ����SQL���Ĭ��Ϊfalse���� ��ǳ��߳���

- formatSql

  ָ��Hibernate�Ƿ�Ӧ��ʽ��SQL���Ĭ��Ϊtrue��

- globalStatsInterval

  ����Hibernate��¼����ִ�е����ݿ��ѯ�����������ȫ��ͳ����Ϣ�� ͳ����Ϣʼ����ָ����ʱ����������Ϊ��λ���������������־������ÿ�α���������

- schema

  ָ��Ҫʹ�õ����ݿ��schema

> ��Щ���ÿ��ص���[* WildFly 16����ָ��*](http://docs.wildfly.org/16/Developer_Guide.html#hibernate-properties)������������ 

### 6.6. ���ݿ��Unicodeע������ {#}

Keycloak�е����ݿ�ģʽ���������������ֶ��е�Unicode�ַ�����

- Realms: ��ʾ���ƣ�HTML��ʾ����
- Federation Providers: ��ʾ����
- Users: �û������������ƣ����ϣ��������ƺ�ֵ
- Groups: ���ƣ��������ƺ�ֵ
- Roles: ����
- Descriptions of objects: ���������

�����ַ����������ݿ�����а������ַ���ͨ��Ϊ8λ�� ���ǣ�����ĳЩ���ݿ�ϵͳ����������Unicode�ַ���UTF-8���룬���������ı��ֶ���ʹ��������Unicode�ַ����� ͨ������8λ����������ȣ���ͨ���϶̵��ַ�����󳤶���������

ĳЩ���ݿ���Ҫ�����ݿ��/��JDBC������������������ò��ܴ���Unicode�ַ��� ���������ҵ��������ݿ�����á� ��ע�⣬����˴��г������ݿ⣬ֻҪ�������ݿ⼶���JDBC������������ȷ����UTF-8���룬����Ȼ��������������

�Ӽ����Ͻ���Unicode֧�������ֶεĹؼ���׼�����ݿ��Ƿ�����Ϊ`VARCHAR`��`CHAR`�ֶ�����Unicode�ַ����� ����ǣ���ôUnicode�ܿ����Ǻ���ģ�ͨ�����ֶγ���Ϊ���ۡ� �����ֻ֧��`NVARCHAR`��`NCHAR`�ֶ��е�Unicode����̫����֧�������ı��ֶΣ���ΪKeycloakģʽ�㷺ʹ��`VARCHAR`��`CHAR`�ֶΡ�

#### 6.6.1. Oracle ���ݿ� {#}

������ݿ�����`VARCHAR`��`CHAR`�ֶ���ʹ��Unicode֧�ִ����ģ����磬ʹ��`AL32UTF8`�ַ�����Ϊ���ݿ��ַ��������������ȷ����Unicode�ַ��� JDBC�������������������á�

������ݿ��ַ�������Unicode����ôҪ�������ֶ���ʹ��Unicode�ַ�����Ҫʹ����������`oracle.jdbc.defaultNChar`����Ϊ`true`������JDBC�������� ��`oracle.jdbc.convertNcharLiterals`������������Ϊ`true`���������ǵģ����ܲ��Ǿ��Ա�Ҫ�ġ� ���Խ���Щ��������Ϊϵͳ���Ի��������ԡ� ��ע�⣬����`oracle.jdbc.defaultNChar`���ܻ�����ܲ�������Ӱ�졣 �й���ϸ��Ϣ�������Oracle JDBC�������������ĵ���

#### 6.6.2. Microsoft SQL Server ���ݿ� {#}

ֻΪ�����ֶ���ȷ����Unicode�ַ��� ����ҪJDBC������������ݿ���������á�

#### 6.6.3. MySQL ���ݿ� {#}

�����`CREATE DATABASE`�����е�`VARCHAR`��`CHAR`fields��ʹ��Unicode֧�ִ������ݿ⣬�������ȷ����Unicode�ַ������磬ʹ��`utf8`�ַ�����ΪMySQL 5.5�е�Ĭ�����ݿ��ַ�������ע�� ���ڶ�`utf8`�ַ���[[1](https://www.keycloak.org/docs/latest/server_installation/index.html#_footnote_1)]�Ĵ洢Ҫ��ͬ��`utf8mb4`�ַ����������á� ��ע�⣬����������£��Է������ֶεĳ������Ʋ����ã���Ϊ�����������ɸ����������ַ����������ֽڡ� ������ݿ�ȱʡ�ַ���������洢Unicode����ֻ�������ֶ�����洢Unicodeֵ��

��JDBC�����������÷��棬��Ҫ��JDBC���������������������`characterEncoding = UTF-8`��

#### 6.6.4. PostgreSQL ���ݿ� {#}

�����ݿ��ַ���Ϊ`UTF8`ʱ��֧��Unicode�� ����������£�Unicode�ַ��������κ��ֶ���ʹ�ã��������ֶε��ֶγ��Ȳ�����١� ����ҪJDBC����������������á�

## 7. �������� {#}

keycover���ܻ���ΪһЩ�������ƶ��޷�ʹ�á����ȣ���������˵㶼�󶨵�`localhost`�����auth������ʵ����ֻ����һ̨���ػ�����ʹ�á����ڻ���HTTP�����ӣ�����ʹ��80��443֮���Ĭ�϶˿ڡ�HTTPS/SSL���ǿ��伴�����õģ����û������keycover����లȫ©�������keyshield���ܾ�����Ҫ���ⲿ������������ȫ��SSL��HTTPS���ӣ������Ҫ�������δ洢���Ա���ȷ��֤�˵㡣���½�����������Щ���ݡ�

### 7.1. �󶨵�ַ {#}

Ĭ������£�keycover�󶨵������������ص�ַ`127.0.0.1`�������ϣ�������ϵ������֤���������ã���ô�ⲻ��һ���ǳ����õ�ȱʡֵ��ͨ�������ǽ����ڹ��������ϲ�����������ƽ��������������·�ɵ�˽�������ϵĸ���Keycloak������ʵ���������������������Ȼ��Ҫ��������ӿ����󶨵�`localhost`֮�������������

���ð󶨵�ַ�ǳ��򵥣���������������ʹ��[ѡ�����ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_operating-mode)�½� �����۵� *standalone.sh* �� *domain.sh* �����ű�����ɡ�

```bash
$ standalone.sh -b 192.168.0.5
```

`-b`����Ϊ�κι����ӿ�����IP�󶨵�ַ��

���ߣ���������������������ð󶨵�ַ������Ա༭����������ļ����á� �������ļ������ļ���*standalone.xml* �� *domain.xml*������ȡ��������[����ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_operating-mode) ����Ѱ��`interfaces` XML�顣

```xml
    <interfaces>
        <interface name="management">
            <inet-address value="${jboss.bind.address.management:127.0.0.1}"/>
        </interface>
        <interface name="public">
            <inet-address value="${jboss.bind.address:127.0.0.1}"/>
        </interface>
    </interfaces>
```

`public`�ӿڶ�Ӧ�ڴ����ɹ���ʹ�õ��׽��ֵ���ϵͳ�� ����һ����ϵͳ��ʾ����Web�㣬���ṩKeycloak�������֤�˵㡣 `management`�ӿڶ�Ӧ��WildFly�����򿪵��׽��֡� �ر���������ʹ��`jboss-cli.sh`�����н����WildFly Web����̨���׽��֡�

�ڲ鿴`public`�ӿ�ʱ�����ῴ������һ�������ַ���`${jboss.bind.address:127.0.0.1}`�� ���ַ�����ʾֵ`127.0.0.1`������ͨ������Javaϵͳ�������������ϸ��ǣ�����

```bash
$ domain.sh -Djboss.bind.address=192.168.0.5
```

`-b`ֻ���������ļ�д���š� ��ˣ�������ֱ���������ļ������и��İ󶨵�ֵַ��Ҳ����������ʱ���������ϸ�������

> ����`interface`����ʱ�����и���ѡ����á� �йظ�����Ϣ������� *WildFly 16�ĵ�* �е�[����ӿ�](http://docs.wildfly.org/16/Admin_Guide.html#Interfaces_and_ports)��

### 7.2. �׽��ֶ˿ڰ� {#}

Ϊÿ���׽��ִ򿪵Ķ˿ھ���Ԥ�����Ĭ��ֵ�������������л������и��ǡ� Ϊ��˵���������ã������Ǽ�װ����[����ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_standalone-mode)�����в���*��/standalone/configuration/standalone.xml*�� ����`socket-binding-group`��

```xml
    <socket-binding-group name="standard-sockets" default-interface="public" port-offset="${jboss.socket.binding.port-offset:0}">
        <socket-binding name="management-http" interface="management" port="${jboss.management.http.port:9990}"/>
        <socket-binding name="management-https" interface="management" port="${jboss.management.https.port:9993}"/>
        <socket-binding name="ajp" port="${jboss.ajp.port:8009}"/>
        <socket-binding name="http" port="${jboss.http.port:8080}"/>
        <socket-binding name="https" port="${jboss.https.port:8443}"/>
        <socket-binding name="txn-recovery-environment" port="4712"/>
        <socket-binding name="txn-status-manager" port="4713"/>
        <outbound-socket-binding name="mail-smtp">
            <remote-destination host="localhost" port="25"/>
        </outbound-socket-binding>
    </socket-binding-group>
```

`socket-bindings`���彫�ɷ������򿪵��׽������ӡ� ��Щ��ָ��������ʹ�õ�`interface`���󶨵�ַ���Լ����ǽ��򿪵Ķ˿ںš� �������Ȥ���ǣ�

- http

  ��������Keycloak HTTP���ӵĶ˿�

- https

  ��������Keycloak HTTPS���ӵĶ˿�

- ajp

  ���׽��ְ󶨶�������AJPЭ��Ķ˿ڡ� ����ʹ��Apache HTTPD��Ϊ���ؾ�����ʱ��Apache HTTPD����������Э����`mod-cluster`���ʹ�á�

- management-http

  ����WildFly CLI��Web����̨ʹ�õ�HTTP���ӡ�

��[��ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_domain-mode)������ʱ�������׽��������е㼬�֣���Ϊʾ�� *domain.xml*�ļ����� ���`socket-binding-groups`���塣 ������¹�����`server-group`���壬����Կ���`socket-binding-group`����ÿ��`server-group`��

���׽��ְ�

```xml
    <server-groups>
        <server-group name="load-balancer-group" profile="load-balancer">
            ...
            <socket-binding-group ref="load-balancer-sockets"/>
        </server-group>
        <server-group name="auth-server-group" profile="auth-server-clustered">
            ...
            <socket-binding-group ref="ha-sockets"/>
        </server-group>
    </server-groups>
```

> ����`socket-binding-group`����ʱ�����и���ѡ����á� �йظ�����Ϣ������� *WildFly 16�ĵ�* �е�[�׽��ְ���](http://docs.wildfly.org/16/Admin_Guide.html#Interfaces_and_ports)��

### 7.3. ���� HTTPS/SSL {#}

> Ĭ������£�Keycloakδ����Ϊ����SSL/HTTPS�� ǿ�ҽ�������Keycloak�����������Keycloak������ǰ��ķ������������SSL�� 

��Ĭ����Ϊ��ÿ��Keycloak�����SSL/HTTPSģʽ���塣 ����[����������ָ��](https://www.keycloak.org/docs/6.0/server_admin/)���и���ϸ�����ۣ��������Ǹ���һЩ�����ĺ���Щģʽ�ļ�Ҫ������

- �ⲿ����

  ֻҪ�����ʹ��`localhost`��`127.0.0.1`��`10.0.x.x`��`192.168.x.x`��`172.16.x.x`��˽��IP��ַ��Keycloak�Ϳ�����û��SSL����������С� �����û���ڷ�����������SSL/HTTPS������������ͨ��HTTP�ӷ�˽��IP��ַ����Keycloak������յ�������Ϣ��

- none (û��)

  Keycloak����ҪSSL��������Ū����ʱ,��Ӧ��ֻ���ڿ�����

- ��������

  KeycloakҪ������IP��ַ��ʹ��SSL��

������Keycloak�������̨������ÿ�������SSLģʽ��

#### 7.3.1. ΪKeycloak Server����SSL/HTTPS {#}

�����û��ʹ�÷���������ƽ����������HTTPS����������ҪΪKeycloak����������HTTPS�� ���漰��

1. ��ȡ�����ɰ���SSL/HTTP������˽Կ��֤�����Կ��
2. ����Keycloak��������ʹ�ô���Կ�Ժ�֤�顣

##### ����֤���Java��Կ�� {#}

Ϊ������HTTPS���ӣ�����Ҫ��ȡ��ǩ���������ǩ��֤�鲢���䵼��Java��Կ�⣬Ȼ�������Ҫ����Keycloak Server��Web����������HTTPS��

###### ��ǩ��֤�� {#}

�ڿ��������У�������û�е�����ǩ��֤������ڲ���Keycloak�����������Ҫʹ��Java JDK������`keytool`ʵ�ó���������ǩ��֤�顣

```bash
$ keytool -genkey -alias localhost -keyalg RSA -keystore keycloak.jks -validity 10950
    Enter keystore password: secret
    Re-enter new password: secret
    What is your first and last name?
    [Unknown]:  localhost
    What is the name of your organizational unit?
    [Unknown]:  Keycloak
    What is the name of your organization?
    [Unknown]:  Red Hat
    What is the name of your City or Locality?
    [Unknown]:  Westford
    What is the name of your State or Province?
    [Unknown]:  MA
    What is the two-letter country code for this unit?
    [Unknown]:  US
    Is CN=localhost, OU=Keycloak, O=Test, L=Westford, ST=MA, C=US correct?
    [no]:  yes
```

��Ӧ��ʹ�������ڰ�װ�������ļ������DNS�������ش�`�������ֺ�������ʲô��`���⡣ ���ڲ���Ŀ�ģ�Ӧʹ��`localhost`�� ִ�д������`keycloak.jks`�ļ�������ִ��`keytool`�����ͬһĿ¼�����ɡ�

�������Ҫ������ǩ��֤�飬��û�е�����ǩ��֤�飬������[cacert.org](http://www.cacert.org/)��ѻ�ȡ�� ����֮ǰ���������һ�����á�

����Ҫ����������֤�����룺

```bash
$ keytool -certreq -alias yourdomain -keystore keycloak.jks > keycloak.careq
```

����`yourdomain`��Ϊ�����ɴ�֤���DNS���ơ� Keytool��������

```
-----BEGIN NEW CERTIFICATE REQUEST-----
MIIC2jCCAcICAQAwZTELMAkGA1UEBhMCVVMxCzAJBgNVBAgTAk1BMREwDwYDVQQHEwhXZXN0Zm9y
ZDEQMA4GA1UEChMHUmVkIEhhdDEQMA4GA1UECxMHUmVkIEhhdDESMBAGA1UEAxMJbG9jYWxob3N0
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAr7kck2TaavlEOGbcpi9c0rncY4HhdzmY
Ax2nZfq1eZEaIPqI5aTxwQZzzLDK9qbeAd8Ji79HzSqnRDxNYaZu7mAYhFKHgixsolE3o5Yfzbw1
29RvyeUVe+WZxv5oo9wolVVpdSINIMEL2LaFhtX/c1dqiqYVpfnvFshZQaIg2nL8juzZcBjj4as
H98gIS7khql/dkZKsw9NLvyxgJvp7PaXurX29fNf3ihG+oFrL22oFyV54BWWxXCKU/GPn61EGZGw
Ft2qSIGLdctpMD1aJR2bcnlhEjZKDksjQZoQ5YMXaAGkcYkG6QkgrocDE2YXDbi7GIdf9MegVJ35
2DQMpwIDAQABoDAwLgYJKoZIhvcNAQkOMSEwHzAdBgNVHQ4EFgQUQwlZJBA+fjiDdiVzaO9vrE/i
n2swDQYJKoZIhvcNAQELBQADggEBAC5FRvMkhal3q86tHPBYWBuTtmcSjs4qUm6V6f63frhveWHf
PzRrI1xH272XUIeBk0gtzWo0nNZnf0mMCtUBbHhhDcG82xolikfqibZijoQZCiGiedVjHJFtniDQ
9bMDUOXEMQ7gHZg5q6mJfNG9MbMpQaUVEEFvfGEQQxbiFK7hRWU8S23/d80e8nExgQxdJWJ6vd0X
MzzFK6j4Dj55bJVuM7GFmfdNC52pNOD5vYe47Aqh8oajHX9XTycVtPXl45rrWAH33ftbrS8SrZ2S
vqIFQeuLL3BaHwpl3t7j2lMWcK1p80laAxEASib/fAwrRHpLHBXRcq6uALUOZl4Alt8=
-----END NEW CERTIFICATE REQUEST-----
```

����ca�����͸�����CA. CA������ǩ��ǩ��֤�鲢���䷢�͸����� �ڵ�����֤��֮ǰ�������ȡ������CA�ĸ�֤�顣 �����Դ�CA����֤�飨����root.crt�����������£�

```
$ keytool -import -keystore keycloak.jks -file root.crt -alias root
```

���һ���ǽ��µ�CA���ɵ�֤�鵼����Կ�⣺

```
$ keytool -import -alias yourdomain -keystore keycloak.jks -file your-certificate.cer
```

##### ����Keycloak��ʹ����Կ�� {#}

��������ӵ�о�����Ӧ֤���Java��Կ�⣬����Ҫ����Keycloak��װ��ʹ������ ���ȣ�������༭*standalone.xml*��*standalone-ha.xml* �� *host.xml*�ļ���ʹ����Կ�Ⲣ����HTTPS��Ȼ�������Խ���Կ���ļ��ƶ�������� *configuration/* Ŀ¼����ѡ���λ���е��ļ������ṩ���ľ���·���� ���ʹ�þ���·�������������ɾ����ѡ��`relative-to`�������μ�[����ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_operating-mode)����

ʹ��CLI����µ�`security-realm`Ԫ�أ�

```bash
$ /core-service=management/security-realm=UndertowRealm:add()

$ /core-service=management/security-realm=UndertowRealm/server-identity=ssl:add(keystore-path=keycloak.jks, keystore-relative-to=jboss.server.config.dir, keystore-password=secret)
```

���ʹ����ģʽ������Ӧ����ÿ��������ʹ��`/host=<host_name>/`ǰ׺ִ�У�Ϊ�������������д���`security-realm`������������������ظ� ÿ��������

```
$ /host=<host_name>/core-service=management/security-realm=UndertowRealm/server-identity=ssl:add(keystore-path=keycloak.jks, keystore-relative-to=jboss.server.config.dir, keystore-password=secret)
```

�ڶ��������������ļ��У�`security-realms`Ԫ��Ӧ������ʾ��

```xml
<security-realm name="UndertowRealm">
    <server-identities>
        <ssl>
            <keystore path="keycloak.jks" relative-to="jboss.server.config.dir" keystore-password="secret" />
        </ssl>
    </server-identities>
</security-realm>
```

���������ڶ�����ÿ���������ļ��У�����`security-realm`���κ�ʵ���� �޸�`https-listener`��ʹ�ô���������

```
$ /subsystem=undertow/server=default-server/https-listener=https:write-attribute(name=security-realm, value=UndertowRealm)
```

���ʹ����ģʽ����������ǰ��������ʹ�õ������ļ���`/profile=<profile_name>/`��

���Ԫ��`server name="default-server"`��`subsystem xmlns="urn:jboss:domain:undertow:8.0"`����Ԫ�أ�Ӧ�ð������½ڣ�

```xml
<subsystem xmlns="urn:jboss:domain:undertow:8.0">
   <buffer-cache name="default"/>
   <server name="default-server">
      <https-listener name="https" socket-binding="https" security-realm="UndertowRealm"/>
   ...
</subsystem>
```

### 7.4. ����HTTP���� {#}

Keycloak������ͨ����Ҫ���䱣����Ӧ�ó���ͷ��񷢳��������HTTP���� auth������ͨ��ά��HTTP�ͻ������ӳ���������Щ�������ӡ� ����Ҫ��`standalone.xml`��`standalone-ha.xml`��`domain.xml`������һЩ���ݡ� ���ļ���λ��ȡ��������[����ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_operating-mode)��

HTTP�ͻ�������ʾ��

```xml
<spi name="connectionsHttpClient">
    <provider name="default" enabled="true">
        <properties>
            <property name="connection-pool-size" value="256"/>
        </properties>
    </provider>
</spi>
```

���ܵ�����ѡ���ǣ�

- establish-connection-timeout-millis

  �����׽������ӵĳ�ʱʱ�䡣

- socket-timeout-millis

  �����������δ�ڴ�ʱ�����յ����ݣ���ʱ���ӡ�

- connection-pool-size

  ���п����ж��ٸ����ӣ�Ĭ��Ϊ128����

- max-pooled-per-route

  ÿ���������Ժϲ����ٸ����ӣ�Ĭ��Ϊ64������

- connection-ttl-millis

  �����ʱ�䣨�Ժ���Ϊ��λ���� Ĭ�������δ���á�

- max-connection-idle-time-millis

  ���ӿ��������ӳ��б��ֿ��е��ʱ�䣨Ĭ��Ϊ900�룩�� ������Apache HTTP�ͻ��˵ĺ�̨�����̡߳� ����Ϊ-`1`�Խ��ô˼��ͺ�̨�̡߳�

- disable-cookies

  Ĭ��Ϊ`true`�� ����Ϊtrueʱ���⽫�����κ�cookie���档

- client-keystore

  ����Java��Կ���ļ����ļ�·���� ����Կ�����˫��SSL�Ŀͻ���֤�顣

- client-keystore-password

  �ͻ�����Կ������롣 ���������`client-keystore`������ *REQUIRED* ��

- client-key-password

  �ͻ���Կ�����롣 ���������`client-keystore`������ *REQUIRED* ��

- proxy-mappings

  ע�⴫��HTTP����Ĵ������á� �йظ�����ϸ��Ϣ�������[����HTTP����Ĵ���ӳ��](https://www.keycloak.org/docs/latest/server_installation/index.html#_proxymappings)���֡�

#### 7.4.1. ����HTTP����Ĵ���ӳ�� {#}

Keycloak���͵Ĵ���HTTP�������ѡ��ʹ�û��ڶ��ŷָ��Ĵ���ӳ���б�Ĵ���������� ����ӳ���ʾ����������ʽ��������ģʽ��`hostnamePattern;proxyUri`��ʽ��proxy-uri����ϣ����磺

```
.*\.(google|googleapis)\.com;http://www-proxy.acme.com:8080
```

Ҫȷ������HTTP����Ĵ�����Ҫ�������õ�������ģʽƥ��Ŀ������������һ��ƥ��ģʽȷ��Ҫʹ�õĴ���uri��������õ�ģʽ����ƥ�����������������ʹ�ô���

����uri������ֵ `NO_PROXY` ������ָʾ��Ӧ���κδ�������ƥ�����������ģʽ�������������ڴ���ӳ���ĩβָ��һ��catch-allģʽ��Ϊ���з�����������һ��Ĭ�ϴ���

����ʾ����ʾ�˴���ӳ�����á�

```
#All requests to Google APIs should use http://www-proxy.acme.com:8080 as proxy
.*\.(google|googleapis)\.com;http://www-proxy.acme.com:8080

#All requests to internal systems should use no proxy
.*\.acme\.com;NO_PROXY

#All other requests should use http://fallback:8080 as proxy
.*;http://fallback:8080
```

�����ͨ������`jboss-cli`�������á� ��ע�⣬����Ҫ��ȷ��ת��������ʽģʽ��������ʾ��

```
echo SETUP: Configure proxy routes for HttpClient SPI

# In case there is no connectionsHttpClient definition yet {#}
/subsystem=keycloak-server/spi=connectionsHttpClient/provider=default:add(enabled=true)

# Configure the proxy-mappings {#}
/subsystem=keycloak-server/spi=connectionsHttpClient/provider=default:write-attribute(name=properties.proxy-mappings,value=[".*\\.(google|googleapis)\\.com;http://www-proxy.acme.com:8080",".*\\.acme\\.com;NO_PROXY",".*;http://fallback:8080"])
```

`jboss-cli` �������������ϵͳ���á�ע�⣬��Ҫ�� `"` ������ `"` �ַ���

```xml
<spi name="connectionsHttpClient">
    <provider name="default" enabled="true">
        <properties>
            <property
            name="proxy-mappings"
            value="[&quot;.*\\.(google|googleapis)\\.com;http://www-proxy.acme.com:8080&quot;,&quot;.*\\.acme\\.com;NO_PROXY&quot;,&quot;.*;http://fallback:8080&quot;]"/>
        </properties>
    </provider>
</spi>
```

#### 7.4.2. ����HTTPS�������ο� {#}

��Keycloak��Զ��HTTPS�˵��ϵ���ʱ����������֤Զ�̷�������֤�飬��ȷ�������ӵ������εķ������� ����ڷ�ֹ�м��˹����Ǳ�Ҫ�ġ� ���뽫��ЩԶ�̷�������֤���ǩ����Щ֤���CA�������ο��С� �����ο���Keycloak����������

�ڰ�ȫ�����ӵ���ݴ���LDAP����ṩ���򣬷��͵����ʼ��Լ���ͻ���Ӧ�ó�����з���ͨ��ͨ��ʱ����ʹ�����ο⡣

> Ĭ������£�δ�������ο��ṩ���򣬲����κ�https���Ӷ����˵���׼java���ο����ã���[Java��JSSE�ο�ָ��](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/JSSERefGuide.html)�������� ���û�н������Σ�����Щ������HTTPS����ʧ�ܡ� 

������ʹ�� *keytool* �����µ����ο��ļ��򽫿�������֤����ӵ������ļ���

```bash
$ keytool -import -alias HOSTDOMAIN -keystore truststore.jks -file host-certificate.cer
```

���ο������ķ��а��е�`standalone.xml`��`standalone-ha.xml`��`domain.xml`�ļ������á� ���ļ���λ��ȡ��������[����ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_operating-mode)�� ������ʹ������ģ��������ο����ã�

```xml
<spi name="truststore">
    <provider name="file" enabled="true">
        <properties>
            <property name="file" value="path to your .jks file containing public certificates"/>
            <property name="password" value="password"/>
            <property name="hostname-verification-policy" value="WILDCARD"/>
            <property name="disabled" value="false"/>
        </properties>
    </provider>
</spi>
```

�����õĿ�������ѡ�������

- file

  Java��Կ���ļ���·���� HTTPS������Ҫһ�ַ�������֤����������֮ͨ�ŵķ������������� �����ί���������ġ� ��Կ�����һ��������������֤���֤��䷢������ �����ο��ļ�Ӧ��������ȫ�����Ĺ���֤�顣 ���`disabled`������������ *REQUIRED* ��

- password

  ���ο�����롣 ���`disabled`������������ *REQUIRED* ��

- hostname-verification-policy

  `WILDCARD`Ĭ������¡� ����HTTPS�����⽫��֤������֤����������� `ANY`��ʾδ��֤�������� `WILDCARD` �����������е�ͨ�������*.foo.com�� `STRICT` CN��������������ȫƥ�䡣

- disabled

  ���Ϊtrue��Ĭ��ֵ�����򽫺������ο����ã�����֤���齫���˵�JSSE���ã����������� �������Ϊfalse�������Ϊtruststore����`file`��`password`��

## 8. ��Ⱥ {#}


  ���ڽ����������Ҫ�ڼ�Ⱥ�����е�Keycloak�� ���ü�Ⱥʱ������Ҫ���ܶ����飬������˵��

- [ѡ��һ�ֲ���ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_operating-mode)
- [���ù����ⲿ���ݿ�](https://www.keycloak.org/docs/latest/server_installation/index.html#_database)
- ���ø��ؾ�����
- �ṩ֧��IP�ಥ��ר������

��ָ��ǰ�������۹�ѡ�����ģʽ�����ù������ݿ⡣ �ڱ����У����ǽ��������ø��ؾ��������ṩר�����硣 ���ǻ��������ڼ�Ⱥ����������ʱ��Ҫע���һЩ���⡣

> ������û��IP�ಥ������¶�Keycloak����Ⱥ�����������ⳬ���˱�ָ�ϵķ�Χ�� �йظ�����Ϣ������� *WildFly 16 �ĵ�* ��[JGroups](http://docs.wildfly.org/16/High_Availability_Guide.html#JGroups_Subsystem) �½ڡ� 

### 8.1. �Ƽ�������ܹ� {#}

���ڲ���Keycloak���Ƽ�������ϵ�ṹ���ڹ���IP��ַ������HTTP/HTTPS���ؾ��������Խ�����·�ɵ�λ��ר�������ϵ�Keycloak�������� ����������м�Ⱥ���ӣ����ṩ�˱����������ĺ÷�����

> Ĭ������£�û��ʲô������ֹδ����Ȩ�Ľڵ���뼯Ⱥ�͹㲥�ಥ��Ϣ�� ����Ǽ�Ⱥ�ڵ�Ӧ����ר�������е�ԭ�򣬷���ǽ���Ա������������ⲿ������ 

### 8.2. ��Ⱥʾ�� {#}

Keycloakȷʵ������һ��������ģʽ�Ŀ��伴�ü�Ⱥ��ʾ�� �й���ϸ��Ϣ����鿴[Ⱥ����ʾ��](https://www.keycloak.org/docs/latest/server_installation/index.html#_clustered-domain-example)һ�¡�

### 8.3. ���ø��ؾ���������� {#}

���������ڽ����������ؾ���������Ⱥ��Keycloak����֮ǰ��Ҫ���õ�һЩ��� ���������������ø��ؾ�����[Clustered Domain Example](https://www.keycloak.org/docs/latest/server_installation/index.html#_clustered-domain-example)��

#### 8.3.1. ʶ��ͻ���IP��ַ {#}

Keycloak�е�һЩ�������������ӵ������֤��������HTTP�ͻ��˵�Զ�̵�ַ�ǿͻ��˼��������ʵIP��ַ�� ���Ӱ�����

- �¼���־ - ��ʹ�ô����ԴIP��ַ��¼ʧ�ܵĵ�¼����
- ��ҪSSL - ��������SSL����Ϊ�ⲿ��Ĭ��ֵ�����������ⲿ������ҪSSL
- ��֤���� - ʹ��IP��ַ���Զ��������֤�������������ⲿ������ʾOTP
- ��̬�ͻ���ע��

������Keycloak�����֤������ǰ���з��������ؾ�����ʱ������ܻ������⡣ ͨ���������ǣ�����һ��λ�ڹ��������ϵ�ǰ�˴�������ƽ�Ⲣ������ת����λ��ר�������еĺ��Keycloak������ʵ���� �ڴ˷���������Ҫִ��һЩ�������ã��Ա㽫ʵ�ʵĿͻ���IP��ַת����Keycloak������ʵ�������䴦�� �ر�

- ���÷��������ؾ���������ȷ���� `X-Forwarded-For` �� `X-Forwarded-Proto` HTTPͷ��
- ���÷��������ؾ������Ա���ԭʼ `Host`HTTPͷ��
- ���������֤�������Դ� `X-Forwarded-For` ͷ��ȡ�ͻ��˵�IP��ַ��

���ô���������`X-Forwarded-For`��`X-Forwarded-Proto`HTTPͷ������ԭʼ��`Host`HTTPͷ�����˱�ָ�ϵķ�Χ�� ��ȡ�����Ԥ����ʩ����ȷ�����Ĵ�������`X-Forwared-For`ͷ�� ������Ĵ������ò���ȷ����ô *rogue* �ͻ��˿����Լ����ô˱�ͷ������ʹKeycloak��Ϊ�ͻ��˴Ӳ�ͬ��IP��ַ���Ӷ�����ʵ�����ӡ� ��������ڽ����κκ��������������IP��ַ���⽫��÷ǳ���Ҫ��

���˴�����֮�⣬����Ҫ��Keycloak��������һЩ������ ������Ĵ���ͨ��HTTPЭ��ת��������ô����Ҫ����Keycloak�Դ� `X-Forwarded-For` ͷ�����Ǵ��������ݰ�����ȡ�ͻ��˵�IP��ַ�� Ҫִ�д˲�������������ļ������ļ���*standalone.xml*��*standalone-ha.xml* �� *domain.xml*������ȡ��������[����ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_operating-mode)�������� `urn:jboss:domain:undertow:8.0` XML�顣

`X-Forwarded-For` HTTP ����

```xml
<subsystem xmlns="urn:jboss:domain:undertow:8.0">
   <buffer-cache name="default"/>
   <server name="default-server">
      <ajp-listener name="ajp" socket-binding="ajp"/>
      <http-listener name="default" socket-binding="http" redirect-socket="https"
          proxy-address-forwarding="true"/>
      ...
   </server>
   ...
</subsystem>
```

��`proxy-address-forwarding`������ӵ�`http-listener`Ԫ�ء� ��ֵ����Ϊ`true`��

������Ĵ���ʹ��AJPЭ�������HTTP��ת�����󣨼�Apache HTTPD + mod-cluster������ô�������Բ�ͬ�ķ�ʽ���á� ����Ҫ���һ������������AJP���ݰ�����ȡ����Ϣ���������޸�`http-listener`��

`X-Forwarded-For` AJP ����

```xml
<subsystem xmlns="urn:jboss:domain:undertow:8.0">
     <buffer-cache name="default"/>
     <server name="default-server">
         <ajp-listener name="ajp" socket-binding="ajp"/>
         <http-listener name="default" socket-binding="http" redirect-socket="https"/>
         <host name="default-host" alias="localhost">
             ...
             <filter-ref name="proxy-peer"/>
         </host>
     </server>
        ...
     <filters>
         ...
         <filter name="proxy-peer"
                 class-name="io.undertow.server.handlers.ProxyPeerAddressHandler"
                 module="io.undertow.core" />
     </filters>
 </subsystem>
```

#### 8.3.2. ʹ�����������HTTPS/SSL {#}

�������ķ������ʹ�ö˿�8443����SSL��������Ҫ�����ض���HTTPS�����Ķ˿ڡ�

```xml
<subsystem xmlns="urn:jboss:domain:undertow:8.0">
    ...
    <http-listener name="default" socket-binding="http"
        proxy-address-forwarding="true" redirect-socket="proxy-https"/>
    ...
</subsystem>
```

��`redirect-socket`������ӵ�`http-listener`Ԫ�ء� ֵӦΪ`proxy-https`����ָ��������Ҫ������׽��ְ󶨡�

Ȼ����`socket-binding-group`Ԫ�������һ���µ�`socket-binding`Ԫ�أ�

```xml
<socket-binding-group name="standard-sockets" default-interface="public"
    port-offset="${jboss.socket.binding.port-offset:0}">
    ...
    <socket-binding name="proxy-https" port="443"/>
    ...
</socket-binding-group>
```

#### 8.3.3. ��֤���� {#}

������ͨ����������·�� `/auth/realms/master/.well-known/openid-configuration` ����֤���������ؾ��������á� ���磬�����������ַ�� `https://acme.com/`�����URL `https://acme.com/auth/realms/master/.well-known/openid-configuration`�� �⽫��ʾһ��JSON�ĵ��������г���Keycloak�����˵㡣 ȷ���˵��Է��������ؾ������ĵ�ַ��scheme, domain and port����ͷ�� ͨ����������������ȷ��Keycloak����ʹ����ȷ�Ķ˵㡣

����Ӧ��֤Keycloak�Ƿ񿴵����������ȷԴIP��ַ�� �����������Գ���ʹ����Ч���û�����/�������¼�������̨�� ��Ӧ���ڷ�������־����ʾ���¾��棺

```
08:14:21,287 WARN  XNIO-1 task-45 [org.keycloak.events] type=LOGIN_ERROR, realmId=master, clientId=security-admin-console, userId=8f20d7ba-4974-4811-a695-242c8fbd1bf8, ipAddress=X.X.X.X, error=invalid_user_credentials, auth_method=openid-connect, auth_type=code, redirect_uri=http://localhost:8080/auth/admin/master/console/?redirect_fragment=%2Frealms%2Fmaster%2Fevents-settings, code_id=a3d48b67-a439-4546-b992-e93311d6493e, username=admin
```

���`ipAddress`��ֵ�������Ե�¼�ļ������IP��ַ�������Ƿ���������ƽ������IP��ַ��

#### 8.3.4. ʹ�����ø��ؾ����� {#}

���ڽ����������[Clustered Domain Example](https://www.keycloak.org/docs/latest/server_installation/index.html#_clustered-domain-example)�����۵����ø��ؾ�����.

[Clustered Domain Example](https://www.keycloak.org/docs/latest/server_installation/index.html#_clustered-domain-example)�����Ϊ��һ̨����������С� Ҫ����һ̨����������һ��slave������Ҫ

1. �༭ *domain.xml* �ļ���ָ���µ�����slave
2. ���Ʒ������ַ��档 ������Ҫ*domain.xml*��*host.xml* �� *host-master.xml*�ļ��� ��Ҳ����Ҫ *standalone/* Ŀ¼��
3. �༭ *host-slave.xml* �ļ��Ը���ʹ�õİ󶨵�ַ�����������ϸ�������

##### ʹ��Load Balancerע�������� {#}

���������ȿ�һ��ʹ�� *domain.xml* �еĸ��ؾ���������ע���µ�����slave�� �򿪴��ļ���ת��`load-balancer`�����ļ��е�undertow���á� ��`reverse-proxy` XML�������һ����Ϊ`remote-host3`����`host`���塣

domain.xml�����������

```xml
<subsystem xmlns="urn:jboss:domain:undertow:8.0">
  ...
  <handlers>
      <reverse-proxy name="lb-handler">
         <host name="host1" outbound-socket-binding="remote-host1" scheme="ajp" path="/" instance-id="myroute1"/>
         <host name="host2" outbound-socket-binding="remote-host2" scheme="ajp" path="/" instance-id="myroute2"/>
         <host name="remote-host3" outbound-socket-binding="remote-host3" scheme="ajp" path="/" instance-id="myroute3"/>
      </reverse-proxy>
  </handlers>
  ...
</subsystem>
```

`output-socket-binding`��һ���߼�����ָ���Ժ��� *domain.xml* �ļ������õ�`socket-binding`�� `instance-id`���Զ���������Ҳ������Ψһ�ģ���Ϊcookieʹ�ô�ֵ���ڸ���ƽ��ʱ����ճ�ԻỰ��

������ת��`load-balancer-socket` `socket-binding-group` ��Ϊ `remote-host3` ��� `outbound-socket-binding`�� ���°���Ҫָ���������������Ͷ˿ڡ�

domain.xml outbound-socket-binding

```xml
<socket-binding-group name="load-balancer-sockets" default-interface="public">
    ...
    <outbound-socket-binding name="remote-host1">
        <remote-destination host="localhost" port="8159"/>
    </outbound-socket-binding>
    <outbound-socket-binding name="remote-host2">
        <remote-destination host="localhost" port="8259"/>
    </outbound-socket-binding>
    <outbound-socket-binding name="remote-host3">
        <remote-destination host="192.168.0.5" port="8259"/>
    </outbound-socket-binding>
</socket-binding-group>
```

##### Master Bind Addresses (���󶨵�ַ) {#}

��������Ҫ���ľ��Ǹ�������������`public`��`management`�󶨵�ַ�� ����[�󶨵�ַ](https://www.keycloak.org/docs/latest/server_installation/index.html#_bind-address)һ���е�˵���༭ *domain.xml* �ļ�����������������ָ����Щ�󶨵�ַ ���������£�

```bash
$ domain.sh --host-config=host-master.xml -Djboss.bind.address=192.168.0.2 -Djboss.bind.address.management=192.168.0.2
```

##### Host Slave Bind Addresses (���������󶨵�ַ) {#}

���������������ò�����`public`��`management`����������󶨵�ַ��`jboss.domain.master-address`���� �༭*host-slave.xml*�ļ�������������ָ�����ǣ�������ʾ��

```bash
$ domain.sh --host-config=host-slave.xml
     -Djboss.bind.address=192.168.0.5
      -Djboss.bind.address.management=192.168.0.5
       -Djboss.domain.master.address=192.168.0.2
```

`jboss.bind.address`��`jboss.bind.addres.management`��ֵ��������slave��IP��ַ�� `jboss.domain.master.address`��ֵ���������������IP��ַ�����������master�����Ĺ����ַ��

#### 8.3.5. �����������ؾ����� {#}

�й����ʹ��������������ĸ���ƽ��������Ϣ������� *WildFly 16�ĵ�* �е�[���ؾ���](http://docs.wildfly.org/16/High_Availability_Guide.html)���֡�

### 8.4. ճ�ԻỰ {#}

���͵ļ�Ⱥ����������ؾ����������������ר�������ϵ�2�������Keycloak�������� ��������Ŀ�ģ�������ؾ����������ض�������Ự��ص���������ת����ͬһKeycloak��˽ڵ㣬����ܻ�����á�

ԭ���ǣ�Keycloak����ʹ��Infinispan�ֲ�ʽ�����������뵱ǰ�����֤�Ự���û��Ự��ص����ݡ� Ĭ������£�Infinispan�ֲ�ʽ����������һ�������ߡ� ����ζ���ض��Ự��������һ��Ⱥ���ڵ��ϣ��������ڵ���ҪԶ�̲��һỰ���ܷ�������

���磬���IDΪ`123`����֤�Ự������`node1`�ϵ�Infinispan�����У�Ȼ��`node2`��Ҫ���ҸûỰ������Ҫͨ�����罫�����͵�`node1`�Է����ض��Ự ʵ�塣

����ض��Ựʵ��ʼ���ڱ��ؿ��ã���������ģ��������ճ�ԻỰ�İ�������ɡ� ���й���ǰ�˸��ؾ��������������Keycloak�ڵ�ļ�Ⱥ�����еĹ����������������ģ�

- �û����ͳ�ʼ�����Բ鿴Keycloak��¼��Ļ
- ��������ǰ�˸��ؾ������ṩ�����߽���ת����ĳ������ڵ㣨���磬node1���� �ϸ��˵���ڵ㲻��Ҫ������ģ������Ը�������һЩ��׼���ͻ���IP��ַ�ȣ�����ѡ�� ��һ�ж�ȡ���ڵײ㸺�ؾ����������������ʵ�ֺ����á�
- Keycloakʹ�����ID������123��������֤�Ự�����䱣�浽Infinispan���档
- Infinispan�ֲ�ʽ������ݻỰID�Ĺ�ϣֵ����Ự����Ҫ�����ߡ� �йش����ݵ���ϸ��Ϣ�������[Infinispan�ĵ�](http://infinispan.org/docs/8.2.x/user_guide/user_guide.html#distribution_mode)�� �����Ǽ���Infinispan��`node2`ָ��Ϊ�˻Ự�������ߡ�
- Keycloakʹ��`<session-id>.<owner-node-id>`�ȸ�ʽ����cookie `AUTH_SESSION_ID`�� �����ǵ�ʾ���У�������`123.node2`��
- ʹ��Keycloak��¼��Ļ��������е�AUTH_SESSION_ID cookie����Ӧ���ظ��û�

����һ��������������ؾ�������������һ������ת����`node2`������ģ���Ϊ���ǽڵ㣬����IDΪ123����֤�Ự�������ߣ����Infinispan�����ڱ��ز��ҸûỰ�� �����֤��ɺ������֤�Ự��ת��Ϊ�û��Ự���ûỰҲ��������`node2`�ϣ���Ϊ��������ͬ��ID`123`��

ճ�ԻỰ����Ⱥ�����ò���ǿ���Եģ�����������ԭ���������������� ����Ҫ��loadbalancer����Ϊճ����`AUTH_SESSION_ID` cookie�ϡ� �⾿��ȡ�������ĸ��ؾ�������

������Keycloak��ʹ�������ڼ��ϵͳ����`jboss.node.name`����ֵ��·���������Ӧ�� ���磬`-Djboss.node.name=node1`��ʹ��`node1`����ʶ·�ɡ� ��·�ɽ���Infinispan����ʹ�ã����ڽڵ����ض���Կ��������ʱ���ӵ�AUTH_SESSION_ID cookie�� ������ʹ�ô�ϵͳ���Ե����������ʾ����

```bash
cd $RHSSO_NODE1
./standalone.sh -c standalone-ha.xml -Djboss.socket.binding.port-offset=100 -Djboss.node.name=node1
```

ͨ�������������У�·������Ӧʹ������������ͬ�����ƣ������Ǳ���ġ� ������ʹ������·�����ơ� ���磬���Ҫ��ר������������Keycloak����������������

#### 8.4.1. �������·�� {#}

ĳЩ���ؾ�������������Ϊ�������·����Ϣ�������������ں��Keycloak�ڵ㡣 ���ǣ���������������ͨ��Keycloak���·�ߡ� ������Ϊ��������ʱ���ܵõ����ƣ���ΪKeycloak֪����Ϊ�ض��Ự�������ߵ�ʵ�岢�ҿ���·�ɵ��ýڵ㣬�ýڵ㲻һ���Ǳ��ؽڵ㡣

�����Ը�⣬����ͨ��������������ӵ�Keycloak��ϵͳ�����е�`RHSSO_HOME/standalone/configuration/standalone-ha.xml`�ļ���������Keycloak��·����Ϣ��ӵ�AUTH_SESSION_ID cookie�У�

```xml
<subsystem xmlns="urn:jboss:domain:keycloak-server:1.1">
  ...
    <spi name="stickySessionEncoder">
        <provider name="infinispan" enabled="true">
            <properties>
                <property name="shouldAttachRoute" value="false"/>
            </properties>
        </provider>
    </spi>

</subsystem>
```

### 8.5. �ಥ�������� {#}

���伴�õļ�Ⱥ֧����ҪIP�ಥ�� �鲥��һ������㲥Э�顣 ��Э��������ʱ���ڷ��ֺͼ��뼯Ⱥ�� �������ڹ㲥��Ϣ���Ա㸴�ƺ�ʹKeycloakʹ�õķֲ�ʽ����ʧЧ��

Keycloak�ļ�Ⱥ��ϵͳ��JGroups��ջ�����С� ���伴�ã���Ⱥ�İ󶨵�ַ�󶨵�ר������ӿڣ�Ĭ��IP��ַΪ127.0.0.1�� ������༭[Bind Address](https://www.keycloak.org/docs/latest/server_installation/index.html#_bind-address) �����۵�*standalone-ha.xml* �� *domain.xml*�����½ڡ�

ר����������

```xml
    <interfaces>
        ...
        <interface name="private">
            <inet-address value="${jboss.bind.address.private:127.0.0.1}"/>
        </interface>
    </interfaces>
    <socket-binding-group name="standard-sockets" default-interface="public" port-offset="${jboss.socket.binding.port-offset:0}">
        ...
        <socket-binding name="jgroups-mping" interface="private" port="0" multicast-address="${jboss.default.multicast.address:230.0.0.4}" multicast-port="45700"/>
        <socket-binding name="jgroups-tcp" interface="private" port="7600"/>
        <socket-binding name="jgroups-tcp-fd" interface="private" port="57600"/>
        <socket-binding name="jgroups-udp" interface="private" port="55200" multicast-address="${jboss.default.multicast.address:230.0.0.4}" multicast-port="45688"/>
        <socket-binding name="jgroups-udp-fd" interface="private" port="54200"/>
        <socket-binding name="modcluster" port="0" multicast-address="224.0.1.105" multicast-port="23364"/>
        ...
    </socket-binding-group>
```

����Ҫ���õĶ�����`jboss.bind.address.private`��`jboss.default.multicast.address`�Լ���Ⱥ��ջ�Ϸ���Ķ˿ڡ�

> ������û��IP�ಥ������¶�Keycloak���м�Ⱥ���������ⳬ���˱�ָ�ϵķ�Χ�� �йظ�����Ϣ������� *WildFly 16�ĵ�* �е�[JGroups](http://docs.wildfly.org/16/High_Availability_Guide.html#JGroups_Subsystem)��

### 8.6. ȷ����Ⱥͨ�Ű�ȫ {#}

����Ⱥ�ڵ���ר�������ϸ���ʱ������Ҫ����ר��������ܼ��뼯Ⱥ��鿴��Ⱥ�е�ͨ�š� ���⣬��������Ϊ��Ⱥͨ�����������֤�ͼ��ܡ� ֻҪ����ר�������ǰ�ȫ�ģ��Ͳ������������֤�ͼ��ܡ� ���κ�һ������£�Keycloak�������ڼ�Ⱥ�Ϸ��ͷǳ����е���Ϣ��

���ҪΪ��Ⱥͨ�����������֤�ͼ��ܣ������ *JBoss EAP����ָ��*�е�[����Ⱥ��](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.0/html/configuration_guide/configuring_high_availability#securing_cluster)��

### 8.7. ���л���Ⱥ���� {#}

����Keycloak��Ⱥ�ڵ�ͬʱ������ ��Keycloak������ʵ������ʱ��������ִ��һЩ���ݿ�Ǩ�ƣ�������״γ�ʼ���� ���ݿ��������ڼ�Ⱥ�ڵ�ͬʱ����ʱ��ֹ���������໥��ͻ��

Ĭ������£������������ʱΪ900�롣 ���ĳ���ڵ����ڵȴ�����������ʱ�����޷������� ͨ����������Ҫ����/����Ĭ��ֵ�����Է���һ���������ķ��а��е�`standalone.xml`��`standalone-ha.xml`��`domain.xml`�ļ��н������á� ���ļ���λ��ȡ��������[����ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_operating-mode)��

```xml
<spi name="dblock">
    <provider name="jpa" enabled="true">
        <properties>
            <property name="lockWaitTimeout" value="900"/>
        </properties>
    </provider>
</spi>
```

### 8.8. ����Ⱥ�� {#}

��Ⱥ��������Keycloakȡ��������[����ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_operating-mode)

Standalone Mode (����ģʽ)

```bash
$ bin/standalone.sh --server-config=standalone-ha.xml
```

Domain Mode (��ģʽ)

```bash
$ bin/domain.sh --host-config=host-master.xml
$ bin/domain.sh --host-config=host-slave.xml
```

��������Ҫʹ������������ϵͳ���ԡ� ���磬�������Ĳ���`-b`��ϵͳ����`jboss.node.name`����ָ��·�ɵ����ƣ���[Sticky Sessions](https://www.keycloak.org/docs/latest/server_installation/index.html#sticky-sessions)������ ���֡�

### 8.9. �����ų� {#}

- ��ע�⣬�����м�Ⱥʱ����Ӧ����������Ⱥ�ڵ����־�п���������Ƶ���Ϣ��

  ```
  INFO  [org.infinispan.remoting.transport.jgroups.JGroupsTransport] (Incoming-10,shared=udp)
  ISPN000094: Received new cluster view: [node1/keycloak|1] (2) [node1/keycloak, node2/keycloak]
  ```

  �����ֻ�����ᵽ��һ���ڵ㣬�����ļ�Ⱥ��������δ������һ��

  ͨ������������ǽ����ļ�Ⱥ�ڵ����ר�������ϣ�����ʹ�÷���ǽ����ͨ�š� ���Խ��ڹ������ʵ������÷���ǽ�����������硣 �������ĳ��ԭ��������Ҫ�ڼ�Ⱥ�ڵ������÷���ǽ������Ҫ��һЩ�˿ڡ� Ĭ��ֵΪUDP�˿�55200���鲥��ַΪ230.0.0.4���鲥�˿�45688�� ��ע�⣬���ҪΪJGroups��ջ������ϵ��������ܣ��������Ҫ�򿪸���˿ڡ� Keycloak���󲿷ּ�Ⱥ����ί�и�Infinispan/JGroups�� �йظ�����Ϣ������� *WildFly 16�ĵ�* �е�[JGroups](http://docs.wildfly.org/16/High_Availability_Guide.html#JGroups_Subsystem)��

- ������Թ���ת��֧�֣��߿����ԣ������𣬵��ںͻ����������Ȥ�������[��������������](https://www.keycloak.org/docs/latest/server_installation/index.html#cache-configuration)��

## 9. �������������� {#}

Keycloak���������͵Ļ��档 һ�����͵Ļ���λ�����ݿ�ǰ�棬�Լ������ݿ�ĸ��أ���ͨ�������ݱ������ڴ���������������Ӧʱ�䡣 ���򣬿ͻ��ˣ���ɫ���û�Ԫ���ݱ����ڴ��໺���С� �˻����Ǳ��ػ��档 ��ʹ���ھ��и���Keycloak�������ļ�Ⱥ�У����ػ���Ҳ��ʹ�ø��ơ� �෴�����ǽ��ڱ��ر��������������������Ŀ�������Ⱥ�����ಿ�ַ�����Ч��Ϣ�����������Ŀ�� ���ڵ����ĸ��ƻ���`work`���������ǽ�ʧЧ��Ϣ���͵�������Ⱥ������Ӧ�ӱ��ػ����������Щ��Ŀ�� �⼫��ؼ��������������������Ч�ʣ���������ͨ�����紫������Ԫ���ݡ�

�ڶ������͵Ļ��洦���û��Ự���ѻ����ƺ͸��ٵ�¼ʧ�ܣ��Ա���������Լ������������������������ ��Щ�����б������������ʱ�ģ������ڴ��У��������ڼ�Ⱥ�и��ơ�

����������Щ���ٻ���ļ�Ⱥ�Ǽ�Ⱥ�����һЩ����ѡ�

> ��Щ���ٻ���ĸ��߼����ÿ����� *WildFly 16�ĵ�* ��[Infinispan](http://docs.wildfly.org/16/High_Availability_Guide.html#Infinispan_Subsystem)�����ҵ��� 

### 9.1. Eviction and Expiration(����͵���) {#}

ΪKeycloak�����˶����ͬ�Ļ��档 ��һ�����򻺴���Ա����йذ�ȫӦ�ó��򣬳��氲ȫ���ݺ�����ѡ�����Ϣ�� ����һ�������û�Ԫ���ݵ��û����档 ��������Ĭ�����Ϊ10000����Ŀ����ʹ���������ʹ�õ�������ԡ� �����е�ÿһ�����󶨵������޶����棬�û������Ⱥ�������е������ �˻�������ʽ�����ģ����Ҿ������ô�С�������� ��ͬ�������ڱ�����Ȩ���ݵ�`authorization`���档 `keys`���汣���й��ⲿ��Կ�����ݣ�����Ҫ����ר�õ��޶����档 �෴������������ȷ������`expiration`�������Կ�ᶨ�ڹ��ڲ�ǿ�ƶ��ڴ��ⲿ�ͻ��˻�����ṩ�����ء�

������*standalone.xml*��*standalone-ha.xml*��*domain.xml*��������Щ�����������Ժ������Ŀ������ȡ��������[����ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_operating-mode)�� �������ļ��У���infinispan��ϵͳ�Ĳ��֣������������ڣ�

```xml
<subsystem xmlns="urn:jboss:domain:infinispan:8.0">
    <cache-container name="keycloak">
        <local-cache name="realms">
            <object-memory size="10000"/>
        </local-cache>
        <local-cache name="users">
            <object-memory size="10000"/>
        </local-cache>
        ...
        <local-cache name="keys">
            <object-memory size="1000"/>
            <expiration max-idle="3600000"/>
        </local-cache>
        ...
    </cache-container>
```

Ҫ���ƻ���չ�������Ŀ����ֻ����ӻ�༭�ض��������õ�`object`Ԫ�ػ�`expiration`Ԫ�ء�

���⣬���е����Ļ���`sessions`��`clientSessions`��`offlineSessions`��`offlineClientSessions`��`loginFailures`��`actionTokens`�� ��Щ�����ڼ�Ⱥ�����зֲ���Ĭ����������ǵĴ�С�����ơ� ����������н�ģ�����ܻᶪʧһЩ�Ự�� ���ڵĻỰ��Keycloak�������ڲ�������Ա��������Ƶ�������Щ����Ĵ�С�� ������ڴ����Ự�������ڴ����⣬�����Գ��ԣ�

- ���Ӽ�Ⱥ�Ĵ�С����Ⱥ�еĸ���ڵ���ζ�ŻỰ�ڽڵ�֮������ȵطֲ���
- ����Keycloak���������̵��ڴ�
- ���������ߵ�������ȷ�������汣����һ��λ�á� �й���ϸ��Ϣ�������[���ƺ͹���ת��](https://www.keycloak.org/docs/latest/server_installation/index.html#_replication) 
- ���÷ֲ�ʽ�����l1-lifespan�� �йظ�����ϸ��Ϣ�������Infinispan�ĵ�
- ���ٻỰ��ʱ��������Keycloak�������̨��Ϊÿ�����򵥶���ɡ� ������ܻ�Ӱ�������û��Ŀ����ԡ� �й���ϸ��Ϣ�������[��ʱ](https://www.keycloak.org/docs/6.0/server_admin/#_timeouts)��

����һ������ĸ��ƻ��棬`work`����Ҫ�����ڼ�Ⱥ�ڵ�֮�䷢����Ϣ; Ĭ���������Ҳ���޽��޵ġ� ���ǣ��˻��治Ӧ�����κ��ڴ����⣬��Ϊ�˻����е���Ŀ�ǳ����ݡ�

### 9.2. ���ƺ͹���ת�� {#}

��һЩ���棬��`sessions`��`authenticationSessions`��`offlineSessions`��`loginFailures`�ȵȣ��μ�[Eviction and Expiration](https://www.keycloak.org/docs/latest/server_installation/index.html#_eviction)�˽����ϸ�ڣ��� ��ʹ�ü�Ⱥ����ʱ����Ϊ�ֲ�ʽ���档 ��Ŀ���Ḵ�Ƶ�ÿ���ڵ㣬����ѡ��һ�������ڵ���Ϊ�����ݵ������ߡ� ����ڵ㲻���ض����ٻ�����Ŀ�������ߣ����ѯ��Ⱥ�Ի�ȡ���� ����ڹ���ת����ζ�����ӵ��һ�����ݵ����нڵ㶼�رգ���ô�����ݽ���Զ��ʧ�� Ĭ������£�Keycloak��ָ��һ�����������ߡ� ��ˣ�����Ǹ��ڵ㷢�����ϣ���ô���ݾͻᶪʧ�� ��ͨ����ζ���û�����ע�������ұ����ٴε�¼��

������ͨ������`distributed-cache`�����е�`owners`���������ĸ���һ�����ݵĽڵ�����

owners (ӵ����)

```xml
<subsystem xmlns="urn:jboss:domain:infinispan:8.0">
   <cache-container name="keycloak">
       <distributed-cache name="sessions" owners="2"/>
...
```

���������Ѿ�������������������������ڵ㽫����һ���ض����û���¼�Ự��

> ���������������ʵ����ȡ�������Ĳ��� ������������û��Ƿ��ڽڵ�ر�ʱע������ôһ�������߾��㹻�ˣ��������⸴�ơ� 

> ͨ�����ǵ������ǽ���������Ϊʹ�ô���ճ�ԻỰ�ĸ��ؾ��⡣ ���������������ģ���Ϊ�ṩ�ض������Keycloak������ͨ�������Էֲ�ʽ��������ݵ������ߣ�����ܹ��ڱ��ز������ݡ� �й���ϸ��Ϣ�������[ճ���Ự](https://www.keycloak.org/docs/latest/server_installation/index.html#sticky-sessions)�� 

### 9.3. ���û��� {#}

Ҫ����������û����ٻ��棬����༭���а��е�`standalone.xml`��`standalone-ha.xml`��`domain.xml`�ļ��� ���ļ���λ��ȡ��������[����ģʽ](https://www.keycloak.org/docs/latest/server_installation/index.html#_operating-mode)�� ����������������ӡ�

```xml
    <spi name="userCache">
        <provider name="default" enabled="true"/>
    </spi>

    <spi name="realmCache">
        <provider name="default" enabled="true"/>
    </spi>
```

Ҫ���û��棬�뽫Ҫ���õĻ����`enabled`��������Ϊfalse�� ������������������������ʹ�˸�����Ч��

### 9.4. ������ʱ������� {#}

Ҫ���������û����棬��ת��Keycloak�������̨�������á���������ҳ�档 �ڴ�ҳ���ϣ�������������򻺴棬�û�������ⲿ��Կ���档

> �������򻺴潫������� 

## 10. Keycloak��ȫ���� {#}

Keycloak��һ��HTTP(S)���������Է���WebӦ�ó���ͷ���֮ǰ���޷���װKeycloak�������� ����������URL���������Ա�ͨ���������¼��/��������������֤������ĳЩURL�� ����������Ӧ�ó����ж���URLģʽ�Ľ�ɫԼ����

### 10.1. ����װ������ {#}

��Keycloak����ҳ������Keycloak�������沢��ѹ����

```bash
$ unzip keycloak-proxy-dist.zip
```

Ҫ����������������һ�����������ļ������ǽ����Ժ����ۣ���

```bash
$ java -jar bin/launcher.jar [your-config.json]
```

���δָ�����������ļ���·���������������ڵ�ǰ����Ŀ¼�в�����Ϊ`proxy.json���ļ���

### 10.2. �������� {#}

����һ��ʾ�������ļ���

```
{
    "target-url": "http://localhost:8082",
    "target-request-timeout": "60000",
    "send-access-token": true,
    "bind-address": "localhost",
    "http-port": "8080",
    "https-port": "8443",
    "keystore": "classpath:ssl.jks",
    "keystore-password": "password",
    "key-password": "password",
    "applications": [
        {
            "base-path": "/customer-portal",
            "error-page": "/error.html",
            "adapter-config": {
                "realm": "demo",
                "resource": "customer-portal",
                "realm-public-key": "MIGfMA0GCSqGSIb",
                "auth-server-url": "http://localhost:8081/auth",
                "ssl-required" : "external",
                "principal-attribute": "name",
                "credentials": {
                    "secret": "password"
                }
            }
            ,
            "constraints": [
                {
                    "pattern": "/users/*",
                    "roles-allowed": [
                        "user"
                    ]
                },
                {
                    "pattern": "/admins/*",
                    "roles-allowed": [
                        "admin"
                    ]
                },
                {
                    "pattern": "/users/permit",
                    "permit": true
                },
                {
                    "pattern": "/users/deny",
                    "deny": true
                }
            ]
        }
    ]
}
```

#### 10.2.1. �������� {#}

�������Ļ�������ѡ�����£�

- target-url

  �˷����������URL�� *��Ҫ*��

- target-request-timeout

  ��������ĳ�ʱ���Ժ���Ϊ��λ���� *��ѡ��*�� Ĭ��ֵΪ30000��

- send-access-token

  ������־�� ���Ϊtrue�����ͨ��KEYCLOAK_ACCESS_TOKEN��ͷ���������Ʒ��͵������������ *��ѡ��*�� Ĭ��ֵΪfalse��

- bind-address

  ���ڽ�������������׽��ְ󶨵���DNS���ƻ�IP��ַ�� *��ѡ��*�� Ĭ��ֵΪ*localhost*

- http-port

  ��������HTTP����Ķ˿ڡ� ���δָ����ֵ�����������������HTTP���� *��ѡ��*��

- https-port

  ����HTTPS����Ķ˿ڡ� ���δָ����ֵ�������������HTTPS���� *��ѡ��*��

- keystore

  Java��Կ���ļ���·�������ļ������������ܹ�����HTTPS�����˽Կ��֤�顣 �������ļ�·�������ߣ������ǰ�����`classpath:`����������·���в��Ҵ��ļ��� *��ѡ��*�� �����������HTTPS����δ������Կ�⣬������Զ�������ǩ��֤�鲢ʹ�ø�֤�顣

- buffer-size

  HTTP�������׽��ֻ�������С ͨ��Ĭ��ֵ�㹻�á� *��ѡ��*��

- buffers-per-region

  ÿ��region(����)��HTTP�������׽��ֻ��� ͨ��Ĭ��ֵ�㹻�á� *��ѡ��*��

- io-threads

  ����IO���߳����� ͨ��Ĭ�����㹻�õġ� *��ѡ��*�� Ĭ��ֵ�ǿ��ô���������* 2��

- worker-threads

  ����������߳����� ͨ��Ĭ��ֵ�㹻�á� *��ѡ��*�� Ĭ��ֵ�ǿ��ô���������* 16��

### 10.3. Ӧ�ó������� {#}

��������`applications`���������£�������Ϊÿ��Ҫ�������������һ������Ӧ�ó���

- base-path

  Ӧ�ó���Ļ��������ĸ��� ������'/'��ͷ�� *��Ҫ*��

- error-page

  ��������д���������ʾĿ��Ӧ�ó���Ĵ���ҳ�����URL�� *��ѡ��*�� ���ǻ���·�������·���� ������������У�������`/customer-portal/error.html`��

- adapter-config

  *��Ҫ*�� ���κ�����Keycloak��������������ͬ��

- proxy-address-forwarding

  ���й�����һ������/���ؾ���������ʱ������ʹ��X-Forwarded-For��X-Forwarded-Host��X-Forwarded-Proto��

#### 10.3.1. Լ������ {#}

��ÿ��Ӧ�ó����£���������`constraints`���������ж���һ������Լ���� Լ����������ڻ���·����URLģʽ�� �����Ծܾ��������Ҫ����ض�URLģʽ���������֤�� ��Ҳ����ָ����·������Ľ�ɫ�� �������Լ���������ڸ�һ���Լ����

- pattern

  �����Ӧ�ó���Ļ���·��ƥ���URLģʽ�� ������'/'��ͷ�� *����*. �����ֻ��һ��ͨ�����������λ��ģʽ��ĩβ����Ч��`/foo/bar/*`��`/foo/*.txt` ��Ч��`/ */foo/*`��

- roles-allowed

  ������ʴ�urlģʽ�Ľ�ɫ�ַ������顣 *��ѡ��*��

- methods

  HTTP�������ַ������飬���ǽ���ռ��ƥ���ģʽ��HTTP���� *��ѡ��*��

- excluded-methods

  ƥ���ģʽʱ�����Ե�HTTP�����ַ������顣 *��ѡ��*��

- deny

  �ܾ����з��ʴ�URLģʽ��Ȩ�ޡ� *��ѡ��*��

- permit

  �������з��ʶ����������֤���ɫӳ�䡣 *��ѡ��*��

- permit-and-inject

  �������з��ʣ�������û��Ѿ��������֤����ע���ͷ�� *��ѡ��*��

- authenticate

  ��Ҫ�Դ�ģʽ���������֤��������Ҫ��ɫӳ�䡣 *��ѡ��*��

#### 10.3.2. Header Names Config (ͷ������) {#}

����������Ӧ�ó����б��£������Ը��Ǵ���ע���ͷ�ֶ����Ƶ�Ĭ��ֵ�������[Keycloak Identity Headers](https://www.keycloak.org/docs/latest/server_installation/index.html#_identity_headers)���� ��ӳ���ǿ�ѡ�ġ�

- keycloak-subject

  ����: MYAPP_USER_ID

- keycloak-username

  ����: MYAPP_USER_NAME

- keycloak-email

  ����: MYAPP_USER_EMAIL

- keycloak-name

  ����: MYAPP_USER_ID

- keycloak-access-token

  ����: MYAPP_ACCESS_TOKEN

### 10.4. Keycloak��ʶͷ {#}

������ת�������������ʱ��Keycloak Proxy��ʹ���յ���OIDC��������е�ֵ����һЩ������ͷ�Խ��������֤��

- KEYCLOAK_SUBJECT

  �û�ID�� ��Ӧ��JWT`sub`������Keycloak���ڴ洢���û����û�ID��

- KEYCLOAK_USERNAME

  �û����� ��Ӧ��JWT`preferred_username`��

- KEYCLOAK_EMAIL

  ���õ��û��ĵ����ʼ���ַ��

- KEYCLOAK_NAME

  �������, �û�ȫ���� 

- KEYCLOAK_ACCESS_TOKEN

  �����������Ϊ���ͣ����ڴ˱�ͷ�з��ͷ������ơ� �����ƿ����ڷ��������������� ����ʹ�������ļ��е�`header-names`ӳ�����ñ����ֶ����ƣ�`{     "header-names" {         "keycloak-subject": "MY_SUBJECT"     } }`

