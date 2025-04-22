### **1. Conceito Base**
Para converter 12V DC em 220V AC, precisas de:
1. **Oscilador/Inversor**: Para transformar os 12V DC da bateria em uma onda alternada de alta frequência ou 50Hz.
2. **Transformador**: Para elevar a tensão de saída até 220V AC.
3. **Modificação do Transformador**: Como vais dividir a bobina primária em 110V + 110V, isso é essencial para criar uma entrada em configuração push-pull.

---

### **2. Modificação do Transformador**
Um transformador típico de 220V para 12V AC tem:
- **Primário:** 220V
- **Secundário:** 12V

Tu queres usá-lo ao contrário, ou seja, transformar **12V DC em 220V AC**. Mas como o primário é apenas uma bobina de 220V, vais dividi-lo em duas bobinas **110V + 110V** para criar um enrolamento **center-tap** (tomada central). Assim, o transformador pode funcionar como push-pull, o que facilita a inversão da corrente.

#### **Como Fazer a Modificação**
1. **Abrir o transformador:** Retira o isolamento para expor as bobinas.
2. **Identificar o enrolamento primário (220V):** Conta o número de voltas.
3. **Dividir o enrolamento em dois de 110V:** 
   - Marca o meio do enrolamento de 220V.
   - Separa as espiras em dois conjuntos iguais (110V cada).
   - Liga o meio ao **ponto central (center-tap)**.
   - Os dois extremos vão receber os pulsos alternados do inversor.

---

### **3. Circuito Inversor (Push-Pull)**
Para alimentar esse transformador modificado a partir da bateria de 12V, precisas de um **circuito inversor** que converta DC para AC. Um dos métodos mais simples é usar um **circuito push-pull com transistores MOSFETs ou um driver IC como SG3525**.

#### **Funcionamento do Push-Pull**
- O **center-tap** do transformador vai ligado diretamente aos **12V da bateria**.
- Dois MOSFETs (ou transístores) alternam a condução, ligando-se à terra em momentos alternados.
- Isso cria uma corrente alternada no transformador, induzindo a saída de **220V AC**.

---

### **4. Resolução e Cálculo**
#### **Frequência e Forma de Onda**
- Para um funcionamento eficiente, a frequência da comutação deve ser **50Hz** (ou 60Hz, dependendo do país).
- Podes gerar a onda quadrada com um **CI como SG3525** ou um **microcontrolador como Arduino**.

#### **Cálculo da Potência**
- Bateria: **12V, 360A → 4320W**
- Supondo eficiência de **80%**, a potência útil é **~3456W**.
- Corrente no primário: \( I = P / V \) → \( I = 3456W / 12V = 288A \) (corrente alta!)
- MOSFETs precisam suportar **picos de corrente acima de 300A**, então transistores robustos como **IRF3205 ou IGBT** podem ser necessários.

---

### **5. Considerações Finais**
- **Transformador aquecerá**: Usa um modelo de alta potência com núcleo adequado.
- **MOSFETs necessitam de dissipação térmica**: Usa **coolers e dissipadores**.
- **Onda quadrada pode causar ruídos**: Se quiseres onda senoidal, precisas de um circuito **PWM + filtro LC**.
