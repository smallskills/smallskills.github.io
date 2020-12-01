---
layout: post
title: Configurando OCI-CLI e 1º deploy de Instance VM
subtitle: Após este tutorial você será capaz de acessar o OCI-CLI localmente e criar Instances VMs na Oracle Cloud
tags: [Cloud, Oracle, OCI, CLI, Instance, VM, Windows, Linux, MacOs]
comments: true
---

## Requisitos

| Uma conta Oracle Cloud | Obrigatório |
| Python v2.7 ou superior | Obrigatório |
| Tenancy OCID | Obrigatório |
| Compartment OCID | Obrigatório |
| User OCID | Obrigatório |

## Baixando e instalando o Oracle Cloud Infrastructure CLI

Aceite as configurações default ou personalize conforme a necessidade.

**MacOS/Linux**  
```javascript
bash -c "$(curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)"
```

**Windows**  
```javascript
powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.ps1'))"
```

Certifique-se que a instalação foi bem sucedida. 

```javascript
oci --help
```

Caso a instalação tenha sido bem sucedida receberá um output como esse.

![Oci-Help](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/E4YcwQoBdQsKXZm8fVrLci4xiInG0FiRaGWSQfNEXxVXJAmfiSXS-3-PPKoWV2Vr/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/2020-11-30-Configurando-OCI-CLI/oci-help.png)

## Configurando Oracle Cloud Infrastructure CLI

Com o CLI instalado, agora é preciso configura-lo. Nesta etapa será necessário compartment OCID, tenancy OCID e user OCID.

**Obtendo User OCID, Compartmet OCID e Tenancy OCID** 

User OCID: Navegue até Identity>Users>Seu User

![User-Ocid](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/np_zGbe9Zaz9UINKmPcGJhRIxsGrUHuVEEcDhLG6RQow1d6SMvspygRAq_UCpzff/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/2020-11-30-Configurando-OCI-CLI/user-ocid.png)

Compartment OCID: Navegue até Identity>Compartment>Compartment Details

![Compartment-Ocid](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/JKEwDkGRSm-IbJIVUlHz89Ozcw_pjs8kkl5SeoTkl_QzlyfId2wS1EiD_AaLwXXs/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/2020-11-30-Configurando-OCI-CLI/compartment-ocid.png)

Tenancy OCID: Navegue até Administration>Compartment>Tenancy Details

![Tenancy-Ocid](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/AgiXs372OaF4Jl9P2gdjVXpgceo-c_u7So_hh2oFnDolVOGFv3VwgCEniswKKxQB/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/2020-11-30-Configurando-OCI-CLI/tenancy-ocid.png)

Para iniciar o processo de configuração execute o comando abaixo, aceite as configurações default ou personalize conforme a necessidade.

```javascript
oci setup config
```
![Oci-Setup](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/Wu9yqvH68zmY2b7VbxXnbi1pwXZl54R7-YfNC8WVNpf-kz_xCczdbvMNjpwQagLy/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/2020-11-30-Configurando-OCI-CLI/oci-setup-config.png)

Nesta etapa será criada uma API Keys e será utilizado a public key recém criada nesse processo.

**MacOS/Linux**

Preencha com as suas infomações (caminho/nome da public key) apontadas no momento da confinguração.

```javascript
$ cd /home/ubuntu/.oci/
$ vim oci_api_key_public.pem 
```
Copie o conteúdo completo da Public Key.

![Public-Key](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/vOVDjB3xmwdJUYLaQRSVXluCGDaCtPUbN0gv6At8kYdtnrgLK5wJSptvLISA0nxT/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/2020-11-30-Configurando-OCI-CLI/public-key.png)

**Windows**

Abra a Public Key no notepad e copie todo o conteúdo.

![Public-Key-Windows](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/vOVDjB3xmwdJUYLaQRSVXluCGDaCtPUbN0gv6At8kYdtnrgLK5wJSptvLISA0nxT/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/2020-11-30-Configurando-OCI-CLI/public-key.png)

Acesse a console Oracle Cloud e vá atá o caminho Identity>Users>Seu User>API Keys>Add API Key.

Selecione "Paste Public Key", cole o conteúdo da Public Key e clique em Add.

![Api-Key](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/GFEO45ZEfNHoh4PEG-JULwJJ5h-sPIdLFyc8kRyIUiPalFoyrwEd4CdkCPVZhnT2/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/2020-11-30-Configurando-OCI-CLI/api-key.png)

Após adicionada a API Key é gerada um Fingerprint. 

![Finger-Print](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/J-fdWrzqA79ic4IYMXvSTJg0gslBP0R1KeGY4wfuY0jFus4Kx0ZTago6Uhi2QtJc/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/2020-11-30-Configurando-OCI-CLI/fingerprint.png)

Visualize o arquivo de configuração.

**MacOS/Linux**

```javascript
$ cd /home/ubuntu/.oci/
$ cat config
```

![Config-Cat](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/QP1n5BBih4rC9YNK2DSH5bS3xtB5NJZSqtGeIsJr-xsNbuZqbf1ucSKhplx_QIm7/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/2020-11-30-Configurando-OCI-CLI/config.png)

**Windows**

Navegue até a pasta do arquivo config e abra com notepad.

![Config-Cat-Windows](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/uEdpaH0pQjgD4EQ04W7AqkVGFTqKIkaWt180qI7FpypikIpvb46_hukwPIV3qbT3/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/2020-11-30-Configurando-OCI-CLI/config-windows.png)

Certifique-se que a configuração foi bem sucedida listando os compartments do Tenancy.

```javascript
$ oci iam compartment list
```

![Compartment-List](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/FmAMKaP-SLgK1KhRNlVZGlXRsg0qTQD0PPydkh4BnKz7z7R3Usd8p64-Td6J0Jpc/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/2020-11-30-Configurando-OCI-CLI/compartment-list.png)

## Deploy de uma Instance VM com OCI-CLI

Após instalar, configurar e certificar-se que tudo funciona bem com OCI-CLI, siga os passos abaixo para criar uma Instance VM via CLI.

Para essa task será necessario as seguintes informações:

| Recurso | Onde Conserguir |
| :------ |:--- |
| Availability Domain | Console Oracle Cloud |
| Compartment OCID | Console Oracle Cloud |
| Subnet OCID | Console Oracle Cloud |
| Shape OCID | Console Oracle Cloud |
| Image OCID | Site Oracle |
| Display Name | Defina um Nome | 
| SSH Key | Gerar no Deploy |

Inicie criando um diretorio para armazenar a SSH Key.

```javascript
$ mkdir keys
```

Gere uma nova SSH Key.

```javascript
$ ssh-keygen -t rsa -N "" -b 2048 -C "CiCd-Compute-Instance" -f /home/ubuntu/keys/key-test
```

Faça o deploy da Instance VM na OCI.

```javascript
$ oci compute instance launch --availability-domain syxp:SA-SAOPAULO-1-AD-1 --compartment-id ocid1.compartment.oc1..aaaaaaaa2tjqxvk2oxw45php23trjixcrzwb3bhzhcw4qqjpjcpvozny6mza --shape VM.Standard.E2.1.Micro --subnet-id ocid1.subnet.oc1.sa-saopaulo-1.aaaaaaaa2j4d7too2lkyjtlzujdegwl3m37tpoqxilnsyunykc2nh3fy65kq --image-id ocid1.image.oc1.sa-saopaulo-1.aaaaaaaa7inha53kcyutiqdbz3w4gvms2ab5z3bc624loheugh7fbvg4wada --assign-public-ip true --display-name instance-vm-teste --ssh-authorized-keys-file /home/ubuntu/keys/key-test.pub
```

Aguarde até que o estado da Intance VM seja Running.

![VM-Provi](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/uFBtSSpKLs3ENerlca0jXrbENvMSLpLtW1BO4P8xH2K7-vTNg96n4E75He7du8Rn/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/2020-11-30-Configurando-OCI-CLI/vm-provi.png)

![VM-Run](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/OjOqNQ0NTBbAZyzEqp_LkbzdUI5YGrBrJFFZuzM7bIGfr-Q3HIh1sMS_v6vPytfB/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/2020-11-30-Configurando-OCI-CLI/vm-run.png)

Acesse a Instance VM recém criada.

```javascript
$ chmod 400 /home/ubuntu/keys/key-test
$ ssh -i /home/ubuntu/keys/key-test opc@168.138.148.108
```



**Here is some bold text**

## Here is a secondary heading

Here's a useless table:

| Number | Next number | Previous numbe |
| :------ |:--- | :--- |
| Five | Six | Four |
| Ten | Eleven | Nine |
| Seven | Eight | Six |
| Two | Three | One |


How about a yummy crepe?

![Oci-Help](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/F4ceppVSvIlaAfzCmhLvVjXEeykRzrH61nScYp9Ayn7_WBxtbfar7VaejUbW0-11/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/2020-11-30-Configurando-OCI-CLI/oci-helpoci-help.png)

It can also be centered!

![Crepe](https://s3-media3.fl.yelpcdn.com/bphoto/cQ1Yoa75m2yUFFbY2xwuqw/348s.jpg){: .mx-auto.d-block :}

Here's a code chunk:

~~~
var foo = function(x) {
  return(x + 5);
}
foo(3)
~~~

And here is the same code with syntax highlighting:

```javascript
var foo = function(x) {
  return(x + 5);
}
foo(3)
```

And here is the same code yet again but with line numbers:

{% highlight javascript linenos %}
var foo = function(x) {
  return(x + 5);
}
foo(3)
{% endhighlight %}

## Boxes
You can add notification, warning and error boxes like this:

### Notification

{: .box-note}
**Note:** This is a notification box.

### Warning

{: .box-warning}
**Warning:** This is a warning box.

### Error

{: .box-error}
**Error:** This is an error box.