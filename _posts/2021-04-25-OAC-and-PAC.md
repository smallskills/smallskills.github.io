---
layout: post
title: Oracle Analytics Cloud com Private Access Channel
subtitle: Conecte Oracle Analytics Cloud (OAC) com fontes de dados usando o Private Access Channel (PAC).
share-img: /assets/img/oci.jpg
thumbnail-img: /assets/img/oci.jpg
tags: [Cloud, Oracle, Analytics, PAC, Private Access Channel, DNS, Network]
comments: true
---

Recentemente a Oracle tornou disponível o Private Access Channel (PAC) uma solução que permite conectar o Oracle Analytics Cloud à fonte de dados privadas como Oracle Autonomous ADW, Oracle Autonomous ATP e DBSystem.

Private Access Channel (PAC) é uma alternativa nativa ao Remote Data Gateway (RDG) e deve substitui-lo no futuro, mas atualmente algumas fontes de dados suportam apenas RDG. Importante destacar que RDG e PAC podem ser utilizados simultaneamente em uma mesma instância do Oracle Analytics Cloud na OCI. 

## Criando e configurando Private Access Channel

Navegue até **Analytics Cloud** clique na Analytics Instance que deseja configurar o Private Access Channel. 

![oac-01](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/SbYQCekItBp_5ngn6uEP6ozz6ZCSPKGLrMyUqgVI_FAaa2Z5ATolu3uAEmTkJ-Dj/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/OAC-PAC/oac-1.png)

Vá até **Private Access Channel.**

![oac-02](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/T2oHyfbS6q0gCveXiCBtM-yQDXg0q0ExSyxNXdMAOOwKWkldT0N0EnY_V4fGWzQD/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/OAC-PAC/oac-2.png)

Clique em **Configure Private Access Channel.**

![oac-03](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/J0lky6nm4t23ZLL6yNu-efCEZRZbbj5_fIl2SthcMBVrBEYKbLe3EYCD6tQrrVjW/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/OAC-PAC/oac-3.png)

Insira os dados para conexão com a fonte de dados e clique em **Configure.**

- Nome
- Selecione o compartment da VCN e subnet.
- Selecione a VCN
- Selecione a subnet
- Add DNS Zone que deseja conectar ao Analytics Cloud, por exemplo adb.sa-saopaulo-1.oraclecloud.com para autonomous na região de São Paulo.

![oac-04](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/zcjayskMSkCdIGyBwFx3w0T7HIFAAQOYJ4xkunGXVZ1FJpcEmoDVUNFpru1_q-8d/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/OAC-PAC/oac-4.png)

**Importante:** O provisionamento do Private Access Channel dura entre 1h e 2h. A console do Analytics Cloud estará acessível, mas pode haver interrupção temporária do serviço durante o provisionamento.

![oac-05](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/4ZA_X2ZBczX6QE22gxdFmCFkdzhTxrdZ9FyAEkamcXG-jW5i2fybF8wLTtyRLiTz/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/OAC-PAC/oac-5.png)

Quando o provisionamento for concluído o Private Access Channel será apresentado dessa forma em **Analytics Cloud > Analytics Instance > Private Access Channel.**

![oac-06](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/4ZA_X2ZBczX6QE22gxdFmCFkdzhTxrdZ9FyAEkamcXG-jW5i2fybF8wLTtyRLiTz/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/OAC-PAC/oac-6.png)

Antes de prosseguir verifique NSG ou Security List da fonte de dados e adicione regras permitindo o acesso a partir dos endereços IPs do Private Access Channel (PAC).

![oac-11](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/4ZA_X2ZBczX6QE22gxdFmCFkdzhTxrdZ9FyAEkamcXG-jW5i2fybF8wLTtyRLiTz/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/OAC-PAC/oac-11.png)

## Conectando Analytics Cloud com fonte de dados via Private Access Channel

Navegue até **Analytics Cloud > Analytics Instance** e clique na URL do Analytics Cloud em **Access Information**. 

Na conlose do Analytics Cloud clique em **Criar** e depois em **Conexão.**

![oac-07](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/4ZA_X2ZBczX6QE22gxdFmCFkdzhTxrdZ9FyAEkamcXG-jW5i2fybF8wLTtyRLiTz/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/OAC-PAC/oac-7.png)

Escolha o tipo de fonte de dados desejado, neste caso é um Autonomous Transaction Processing.

![oac-08](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/4ZA_X2ZBczX6QE22gxdFmCFkdzhTxrdZ9FyAEkamcXG-jW5i2fybF8wLTtyRLiTz/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/OAC-PAC/oac-8.png)

Insira os dados da fonte de dados e clique em **Salvar.**

- Nome da conexão
- Descrição.
- Wallet do Autonomous no formato .zip.
- User e password do Autonomous
- Tipo de serviço

![oac-09](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/4ZA_X2ZBczX6QE22gxdFmCFkdzhTxrdZ9FyAEkamcXG-jW5i2fybF8wLTtyRLiTz/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/OAC-PAC/oac-9.png)

Feito isso a conexão com uma fonte de dados a partir do Private Access Channel é estabelecida.

![oac-10](https://objectstorage.sa-saopaulo-1.oraclecloud.com/p/mO3zrzrXRdXAEDG9iNQdV6i1If5B0Al3i4caL42JdStbsoOSRIA0WDll7h5z3e70/n/gr8gkzaf8nit/b/bucket-euoraf4-site/o/OAC-PAC/oac-10.png)

Dessa forma o Private Access Channel (PAC) está habilitado em uma instância do Analytics Cloud.
