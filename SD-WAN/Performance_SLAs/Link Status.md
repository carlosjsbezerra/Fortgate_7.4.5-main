### Link Status

A seção **Link Status** define como o FortiGate monitora a conectividade de um link SD-WAN e quando ele será considerado inativo ou restaurado. Abaixo estão as explicações para cada campo:

---

#### 1. **Check Interval (Intervalo de Verificação)**
- **O que é:** Define o intervalo de tempo entre cada verificação do link, medido em milissegundos (ms).
- **Valor na imagem:** 500 ms.
- **Como funciona:**
  - A cada **500 ms** (meio segundo), o FortiGate enviará pacotes de monitoramento (como ping ou consultas DNS) para verificar a qualidade do link.
  - Com esse valor, o FortiGate realiza duas verificações por segundo, permitindo monitoramento quase em tempo real.
- **Recomendação:**
  - Um intervalo de **500 ms** é apropriado para uma detecção rápida de problemas.
  - Se sua rede não exige resposta rápida, você pode aumentar o intervalo para reduzir o tráfego gerado pelas verificações.

---

#### 2. **Failures before inactive (Falhas antes de ser marcado como inativo)**
- **O que é:** Define o número de falhas consecutivas necessárias para o FortiGate marcar um link como inativo.
- **Valor na imagem:** 5.
- **Como funciona:**
  - Se o link falhar por **5 verificações consecutivas**, ele será marcado como **inativo**.
  - Com o intervalo de 500 ms, o FortiGate levaria **2,5 segundos** (5 x 500 ms) para marcar o link como inativo.
- **Recomendação:**
  - **5 falhas** é um valor equilibrado para evitar a desativação por pequenas falhas temporárias.
  - Se você precisa de uma resposta mais rápida, pode reduzir o número de falhas para **3**, o que reduziria o tempo de resposta para **1,5 segundo**.

---

#### 3. **Restore link after (Restaurar link após)**
- **O que é:** Define o número de verificações consecutivas bem-sucedidas necessárias para o FortiGate restaurar um link após ele ter sido marcado como inativo.
- **Valor na imagem:** 5.
- **Como funciona:**
  - Após um link ser marcado como inativo, ele precisará de **5 verificações consecutivas bem-sucedidas** para ser restaurado.
  - Com o intervalo de 500 ms, isso levaria **2,5 segundos** (5 x 500 ms) para o link ser reativado.
- **Recomendação:**
  - **5 verificações** garantem que o link realmente se estabilizou antes de ser restaurado.
  - Se você quiser uma recuperação mais rápida, pode diminuir esse valor para **3**.

---

### Resumo das Recomendações:

| Tipo de Aplicação                        | Check Interval | Failures before inactive | Restore link after |
|------------------------------------------|----------------|--------------------------|--------------------|
| **Aplicações Críticas (VoIP, Videoconferência)** | 250 ms         | 3                        | 3                  |
| **Uso Comum (Navegação, Streaming)**            | 500 ms         | 5                        | 5                  |
| **Redes com Baixa Qualidade (Tolerância Maior)**| 1000 ms        | 7                        | 7                  |

