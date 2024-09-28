# Tutorial: Configurando uma Rede Básica com FortiGate, FortiSwitch e FortiAP

Neste tutorial, vamos abordar como configurar uma rede básica utilizando um **FortiGate** firewall, **FortiSwitch** e **FortiAP**. A seguir, passo a passo, você verá como configurar esses dispositivos e integrá-los em sua rede.

---

## 1. Visão Geral da Configuração Inicial

**Equipamentos Utilizados:**
- **FortiGate 90G** - Firewall para gerenciar sua rede.
- **FortiSwitch 108F-FPOE** - Switch para expandir a conectividade da rede e fornecer Power over Ethernet (PoE).
- **FortiAP** - Ponto de acesso wireless.

**Conexões:**
- **FortiGate 90G Port A** conectado à **Porta 8 do FortiSwitch**
- **FortiGate Port 1** conectado ao **FortiAP** via PoE.

Vamos configurar o **FortiSwitch** e o **FortiAP** do zero, e garantir que ambos sejam gerenciados pelo **FortiGate**.

---

## 2. Habilitar os Controladores de Wireless e Switch

Para começar a configuração, é necessário habilitar os controladores no **FortiGate**.

1. Acesse a interface de administração do **FortiGate**.
2. Navegue até **System > Feature Visibility**.
3. Ative as seguintes opções:
   - **Switch Controller**
   - **Wireless Controller**
4. Clique em **Apply**.

Depois de aplicar, os menus para **WiFi & Switch Controller** estarão visíveis no painel à esquerda.

---

## 3. Configurar a Interface FortiLink

Agora vamos configurar a interface **FortiLink**, que será usada para gerenciar o **FortiSwitch** a partir do **FortiGate**.

1. Acesse **WiFi & Switch Controller** e localize a interface **FortiLink**.
2. Por padrão, o **FortiLink** pode estar configurado para utilizar o espaço de IP `10.255.1.1/24`.
3. Verifique que o **FortiSwitch** está conectado, mas não autorizado.
4. Autorize o **FortiSwitch** clicando sobre ele e selecionando a opção **Authorize**.

Isso permite que o **FortiGate** gerencie o **FortiSwitch**.

---

## 4. Configurar VLAN para o FortiAP

Agora, precisamos criar uma **VLAN** para o tráfego gerado pelo **FortiAP**.

1. Acesse **Network > Interfaces** e clique em **Create New**.
2. Escolha **VLAN** e configure da seguinte maneira:
   - **Name**: `FortiAP_VLAN`
   - **VLAN ID**: `60`
   - **IP Address**: `192.168.60.99/24`
   - Habilite **Ping** e **Administrative Access**.
   - Habilite o **DHCP Server** para essa **VLAN**.
3. Aplique as configurações.

Agora, atribua essa **VLAN** à porta onde o **FortiAP** está conectado:

1. Acesse **WiFi & Switch Controller > FortiSwitch Ports**.
2. Selecione a **Port 1** (onde o **FortiAP** está conectado) e altere a **Native VLAN** de **FortiLink** para **FortiAP_VLAN**.
3. Clique em **Apply**.

---

## 5. Autorizar o FortiAP

Agora que a **VLAN** está configurada, vamos autorizar o **FortiAP** para que ele seja gerenciado pelo **FortiGate**.

1. Vá até **WiFi & Switch Controller > Managed FortiAPs**.
2. Você verá o **FortiAP** listado como **unauthorized**.
3. Clique com o botão direito sobre ele e selecione **Authorize**.

O **FortiGate** começará a sincronizar as configurações com o **FortiAP**.

---

## 6. Criar um SSID

Para que o **FortiAP** transmita uma rede sem fio, é necessário criar um **SSID**.

1. Vá até **WiFi & Switch Controller > SSIDs** e clique em **Create New**.
2. Configure da seguinte forma:
   - **SSID Name**: `Example SSID`
   - **IP Address**: `192.168.61.1/24`
   - Habilite o **DHCP Server** para essa rede.
   - Defina o **Broadcast SSID** como `EXAMPLE`.
   - Defina uma **Password** como `Fortinet1!`.
3. Aplique as configurações.

---

## 7. Verificar o Status do FortiAP

Com o **SSID** criado, você pode verificar o status do **FortiAP**:

1. Acesse **WiFi & Switch Controller > Managed FortiAPs**.
2. Verifique se o **FortiAP** está **Online** e transmitindo.
3. Veja em quais **channels** (como 1 e 165) o **FortiAP** está transmitindo.

---

## 8. Criar Política de Firewall para Tráfego Wireless

Para permitir o tráfego da rede wireless para a internet, é necessário criar uma política de **firewall**.

1. Vá até **Policy & Objects > Firewall Policy** e clique em **Create New**.
2. Configure as opções:
   - **Name**: `Wireless`
   - **Incoming Interface**: `Example SSID`
   - **Outgoing Interface**: `Any`
   - **Source**: `Any`
   - **Destination**: `Any`
   - Habilite **NAT** e **Log All Sessions**.
3. Aplique as configurações e mova essa política para o topo da lista.

---

## 9. Testar a Conectividade Wireless

Agora você pode testar a rede wireless:

1. Conecte-se ao **SSID** `EXAMPLE` utilizando a senha `Fortinet1!`.
2. Verifique se a conexão está funcionando acessando um site, como `fortinet.com`.

Agora, sua rede wireless está configurada e conectada à internet.

---

## 10. Configurar VLAN para Clientes Cabeados

Para clientes conectados via cabo, vamos configurar uma nova **VLAN**.

1. Vá até **Network > Interfaces** e clique em **Create New**.
2. Configure as seguintes opções:
   - **Name**: `Wired_VLAN`
   - **VLAN ID**: `70`
   - **IP Address**: `192.168.70.1/24`
   - Habilite o **DHCP Server**.
3. Aplique as configurações.

Agora, atribua essa **VLAN** às portas do **FortiSwitch** onde os dispositivos com fio serão conectados:

1. Acesse **WiFi & Switch Controller > FortiSwitch Ports**.
2. Selecione as portas 2 a 7 e altere a **Native VLAN** para **Wired_VLAN**.
3. Clique em **Apply**.

---

## 11. Criar Política de Firewall para Tráfego Cabeado

Assim como fizemos para o tráfego wireless, vamos criar uma política de firewall para os clientes cabeados.

1. Vá até **Policy & Objects > Firewall Policy** e clique em **Create New**.
2. Defina a **Incoming Interface** como `Wired_VLAN`.
3. Configure **Source**, **Destination** e **Service** como `Any`.
4. Habilite **NAT** e aplique as configurações.

---

## 12. Conclusão

Agora, seu **FortiGate**, **FortiSwitch** e **FortiAP** estão completamente configurados, com suporte para clientes conectados tanto via cabo quanto wireless. Você pode acessar a internet e gerenciar sua rede de maneira centralizada por meio do **FortiGate**.
