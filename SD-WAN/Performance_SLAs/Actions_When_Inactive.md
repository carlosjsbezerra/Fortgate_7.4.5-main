### Seção **Actions when Inactive** com a opção **Update static route** ativada. Vamos entender o que essa configuração faz:

---

### **Actions when Inactive (Ações quando Inativo):**
Esta seção define o que o FortiGate deve fazer quando o link monitorado for considerado inativo com base nas verificações do SLA.

---

### **Update static route (Atualizar rota estática):**
- **O que é:** Quando essa opção está ativada (como no caso da imagem), o FortiGate removerá automaticamente as rotas estáticas associadas a esse link quando ele for considerado inativo.

  - Isso significa que o FortiGate ajustará dinamicamente as rotas de rede para garantir que o tráfego não seja roteado por um link com problemas de qualidade.

---

### **Como funciona:**
- Se o link monitorado falhar as verificações de SLA (por exemplo, ultrapassando os limites de latência, jitter ou perda de pacotes), o FortiGate vai marcar o link como **inativo** e removerá as rotas estáticas associadas a ele.
- Quando o link voltar a estar ativo (após passar nas verificações bem-sucedidas), as rotas estáticas serão restauradas automaticamente, permitindo que o tráfego volte a passar por esse link.

---

### **Por que é útil:**
- Essa configuração evita que o tráfego da rede seja encaminhado por um link com baixa qualidade ou que esteja inativo, redirecionando-o para outros links mais confiáveis.
- Melhora a **resiliência da rede**, evitando falhas de conectividade que poderiam ocorrer se o tráfego continuasse passando por um link problemático.

---

### **Quando usar essa configuração:**
- Recomendado para redes **SD-WAN** que têm múltiplos links de internet e dependem de roteamento dinâmico. 
- Se um link falhar ou tiver problemas de desempenho, essa configuração garante que o tráfego seja desviado automaticamente para outros links mais estáveis, sem intervenção manual.

---

### **Conclusão:**
Com a opção **Update static route** ativada, o FortiGate removerá as rotas estáticas de um link problemático quando ele for considerado **inativo**, evitando o roteamento de tráfego por esse link. Quando o link voltar a ficar ativo, a rota será restaurada automaticamente.

Se você tiver mais dúvidas ou precisar de ajuda para ajustar essa configuração, é só avisar!
