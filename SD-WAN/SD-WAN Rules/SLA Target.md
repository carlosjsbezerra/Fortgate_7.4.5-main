### 1. **Latency threshold (Limite de latência):**
   - **O que é:** Latência mede o tempo (em milissegundos, ms) que um pacote leva para viajar de uma origem até o destino e voltar. Em outras palavras, é o atraso na transmissão de dados entre o seu FortiGate e o servidor.
   - **O valor na imagem:** 93 ms.
   - **Recomendação:** 
     - Um valor aceitável de latência varia conforme o tipo de serviço que você deseja oferecer.
     - Para serviços que exigem respostas rápidas, como chamadas VoIP ou jogos online, você deve buscar valores abaixo de **50 ms**.
     - Para uso comum da Internet, como navegação e streaming, valores de até **100 ms** podem ser aceitáveis. No entanto, é recomendável manter esse valor abaixo de **150 ms**.
     - Se seus links forem rápidos e estáveis, você pode definir um valor de **100 ms a 150 ms**.

### 2. **Jitter threshold (Limite de jitter):**
   - **O que é:** Jitter representa a variação na latência entre pacotes consecutivos. Jitter elevado pode causar problemas em aplicativos sensíveis a tempo real, como VoIP e videoconferências, porque os pacotes podem não chegar de forma regular.
   - **O valor na imagem:** 50 ms.
   - **Recomendação:**
     - Para aplicativos que dependem de baixa variação de latência, como VoIP, recomenda-se manter o jitter abaixo de **30 ms**.
     - Em cenários de uso geral, um valor de até **50 ms** pode ser aceitável, mas tente manter abaixo de **40 ms** se possível para garantir um desempenho suave.
     - Se a rede tiver mais tolerância a variações, como em navegação web comum, o jitter pode ser definido até **50 ms**.

### 3. **Packet Loss threshold (Limite de perda de pacotes):**
   - **O que é:** A perda de pacotes é a porcentagem de pacotes que são enviados, mas nunca chegam ao destino. A perda de pacotes pode causar interrupções, principalmente em chamadas de vídeo ou voz, downloads e transmissões ao vivo.
   - **O valor na imagem:** 2%.
   - **Recomendação:**
     - Idealmente, você quer que a perda de pacotes seja a mais baixa possível. Em redes estáveis, a perda de pacotes deve ser **0%** ou muito próxima disso.
     - Para garantir um serviço de boa qualidade, um limite aceitável de perda de pacotes seria até **1%**.
     - Para serviços mais tolerantes à perda de pacotes (como navegação na web), um valor de **2%** pode ser aceitável. No entanto, acima de **2%** a qualidade do serviço já pode começar a ser visivelmente afetada.

### Como escolher os valores ideais para sua rede:
- **Aplicações críticas (VoIP, Videoconferência):**
  - **Latência:** < 50 ms
  - **Jitter:** < 30 ms
  - **Perda de pacotes:** 0% a 1%

- **Uso comum (Navegação, Streaming, Downloads):**
  - **Latência:** < 100 ms
  - **Jitter:** < 50 ms
  - **Perda de pacotes:** Até 1% ou 2%

- **Redes com baixa qualidade (mais tolerância a variações):**
  - **Latência:** Até 150 ms
  - **Jitter:** Até 50 ms
  - **Perda de pacotes:** Até 2%
