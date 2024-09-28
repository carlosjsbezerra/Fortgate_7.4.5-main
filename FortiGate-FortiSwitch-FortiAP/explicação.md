# Tutorial: Configurando uma Rede Básica com FortiGate, FortiSwitch e FortiAP

Neste tutorial, vamos configurar uma rede usando **FortiGate**, **FortiSwitch** e **FortiAP**. Vou explicar cada passo e por que ele é importante para você entender o processo.

---

## 1. O que é FortiGate, FortiSwitch e FortiAP?

- **FortiGate**: É o **firewall** que protege a sua rede contra ameaças, controla o que entra e sai, e gerencia o tráfego de rede.
- **FortiSwitch**: É o **switch** que distribui a conexão de rede para dispositivos via cabo, como computadores e impressoras.
- **FortiAP**: O **FortiAP** é o **ponto de acesso wireless**, responsável por fornecer Wi-Fi para os dispositivos conectados sem fio.

---

## 2. Por que precisamos configurar tudo isso?

O **FortiGate**, **FortiSwitch** e **FortiAP** desempenham funções diferentes, mas precisam ser configurados para trabalharem juntos. A configuração garante que o **FortiGate** gerencie o **FortiSwitch** e o **FortiAP**, mantendo a rede organizada, segura e funcionando corretamente.

---

## 3. Habilitar o Controlador de Wireless e Switch no FortiGate

### O que estamos fazendo?
Vamos habilitar os controladores **Switch Controller** e **Wireless Controller** no **FortiGate**.

### Por que estamos fazendo isso?
Esses controladores permitem que o **FortiGate** gerencie o **FortiSwitch** e o **FortiAP**, facilitando a configuração e o monitoramento.

### Como fazer?
1. No **FortiGate**, acesse **System > Feature Visibility**.
2. Ative **Switch Controller** e **Wireless Controller**.
3. Clique em **Apply**.

---

## 4. Configurar a Interface FortiLink

### O que estamos fazendo?
Vamos configurar a interface **FortiLink**, que permitirá ao **FortiGate** gerenciar o **FortiSwitch**.

### Por que estamos fazendo isso?
A **FortiLink** é o canal de comunicação entre o **FortiGate** e o **FortiSwitch**. Sem isso, o **FortiSwitch** não pode ser configurado nem gerenciado pelo **FortiGate**.

### Como fazer?
1. No **FortiGate**, vá até **WiFi & Switch Controller**.
2. Localize a interface **FortiLink** (IP padrão `10.255.1.1/24`).
3. Verifique que o **FortiSwitch** está como **unauthorized**.
4. Clique no **FortiSwitch** e selecione **Authorize**.

---

## 5. Configurar VLAN para o FortiAP

### O que estamos fazendo?
Vamos criar uma **VLAN** para o tráfego do **FortiAP**.

### Por que estamos fazendo isso?
A **VLAN** organiza o tráfego da rede, separando o tráfego do **FortiAP** do tráfego de outros dispositivos. Isso aumenta a segurança e facilita o gerenciamento.

### Como fazer?
1. No **FortiGate**, vá até **Network > Interfaces**.
2. Clique em **Create New** e selecione **VLAN**.
3. Configure:
   - **Name**: `FortiAP_VLAN`
   - **VLAN ID**: `60`
   - **IP Address**: `192.168.60.99/24`
4. Ative **Ping** e **Administrative Access**.
5. Ative o **DHCP Server** para que os dispositivos conectados ao Wi-Fi recebam IPs automaticamente.

---

## 6. Autorizar o FortiAP

### O que estamos fazendo?
Vamos **autorizar** o **FortiAP** para que o **FortiGate** possa gerenciá-lo.

### Por que estamos fazendo isso?
Assim como o **FortiSwitch**, o **FortiAP** precisa ser autorizado para que o **FortiGate** possa configurá-lo e monitorá-lo.

### Como fazer?
1. No **FortiGate**, vá para **WiFi & Switch Controller > Managed FortiAPs**.
2. Localize o **FortiAP** listado como **unauthorized**.
3. Clique com o botão direito nele e selecione **Authorize**.

---

## 7. Criar um SSID

### O que estamos fazendo?
Vamos criar um **SSID**, que é o nome da rede Wi-Fi transmitida pelo **FortiAP**.

### Por que estamos fazendo isso?
Sem um **SSID**, o **FortiAP** não transmitirá uma rede Wi-Fi, e os dispositivos não poderão se conectar.

### Como fazer?
1. No **FortiGate**, vá até **WiFi & Switch Controller > SSIDs**.
2. Clique em **Create New**.
3. Configure:
   - **SSID Name**: `Example SSID`
   - **IP Address**: `192.168.61.1/24`
   - Ative o **DHCP Server**.
4. Defina o **Broadcast SSID** como `EXAMPLE` e uma senha, como `Fortinet1!`.

---

## 8. Criar uma Política de Firewall para o Tráfego Wireless

### O que estamos fazendo?
Vamos criar uma política de **firewall** para permitir que o tráfego da rede wireless tenha acesso à internet.

### Por que estamos fazendo isso?
A **política de firewall** é uma regra que permite ou bloqueia o tráfego na rede. Sem essa regra, os dispositivos conectados ao Wi-Fi não terão acesso à internet.

### Como fazer?
1. No **FortiGate**, vá até **Policy & Objects > Firewall Policy**.
2. Clique em **Create New**.
3. Configure:
   - **Name**: `Wireless`
   - **Incoming Interface**: `Example SSID`
   - **Outgoing Interface**: `Any`
   - **Source**: `Any`
   - **Destination**: `Any`
   - Ative o **NAT**.

---

## 9. Configurar VLAN para Clientes Conectados via Cabo

### O que estamos fazendo?
Vamos criar uma **VLAN** para os dispositivos conectados ao **FortiSwitch** via cabo.

### Por que estamos fazendo isso?
Criar uma **VLAN** separada para dispositivos cabeados ajuda a organizar e controlar o tráfego de rede, mantendo-o separado e seguro.

### Como fazer?
1. No **FortiGate**, vá até **Network > Interfaces**.
2. Clique em **Create New** e selecione **VLAN**.
3. Configure:
   - **Name**: `Wired_VLAN`
   - **VLAN ID**: `70`
   - **IP Address**: `192.168.70.1/24`
4. Ative o **DHCP Server** para essa VLAN.

---

## 10. Criar Política de Firewall para Clientes Conectados por Cabo

### O que estamos fazendo?
Vamos criar uma política de **firewall** para permitir que o tráfego dos dispositivos conectados por cabo tenha acesso à internet.

### Por que estamos fazendo isso?
Assim como fizemos para o tráfego wireless, precisamos criar uma regra para que o tráfego dos dispositivos conectados ao **FortiSwitch** tenha acesso à internet.

### Como fazer?
1. No **FortiGate**, vá até **Policy & Objects > Firewall Policy**.
2. Clique em **Create New** e configure:
   - **Incoming Interface**: `Wired_VLAN`
   - **Source**: `Any`
   - **Destination**: `Any`
   - Ative o **NAT**.

---

## Conclusão

Agora que tudo está configurado, o **FortiGate**, **FortiSwitch** e **FortiAP** estão trabalhando juntos. Sua rede está configurada tanto para dispositivos conectados via cabo quanto para os conectados via Wi-Fi, e todos podem acessar a internet de maneira segura.
