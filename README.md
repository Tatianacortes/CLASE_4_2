# CLASE 4 II CORTE
# Diseño de Sistemas de Transmisión en Control de Movimiento

## Objetivos del diseño ##  
  - Selección de motor y transmisión para cumplir perfiles de movimiento.  
  - Asegurar torque e inercia adecuados, para asegurar una buena relación de transmisión.

## Problemas de diseño ##
| Tipo | Información cocnocida                            | Encontrar / Dimensionar         |
|------|--------------------------------------------------|---------------------------------|
| 1    | Movimiento deseado de la carga                   | Transmisión y motor             |
| 2    | Motor y transmisión existentes                   | Movimiento resultante de la carga |
| 3    | Motor existente, movimiento deseado de la carga  | Transmisión                     |
| 4    | Movimiento deseado de la carga, transmisión      | Motor                           |

## Inercia y Torque Reflejado
- La inercia es la resistencia de un objeto al cambio en su velocidad angular:  
  $$\sum T = J \alpha$$
- Se utiliza en sistemas rotacionales y de traslación.
- Afectados por la relación de trasnmisión. 
  
## Tipos de Transmisiones Mecánicas
### Engranajes  
![Figura de prueba](IMAGES/engranajes.png)
##
- **Relación de transmisión**:
  Se puede encontrar revisando la velocidad tangencial de las dos ruedas, o la potencia mecánica, y a partir de estas dos caracteristicas se pueden obtener las siguientes ecuaciones equivalentes. 
#### Ecuaciones de Transmisión

#### Definición de la Relación de Transmisión

La relación de transmisión está definida por:

$N_{GB}=\frac{\text{motor speed}}{\text{load speed}}$

---

- Velocidad tangencial:

$V_{\text{tangential}}=\omega_m r_m=\omega_l r_l$

- Relación de velocidades angulares:

$\frac{\omega_m}{\omega_l}=\frac{r_l}{r_m}$

- Relación de transmisión:

$N_{GB}=\frac{\omega_m}{\omega_l}=\frac{r_l}{r_m}$

---
- En función del número de dientes:

$\frac{n_l}{n_m}=\frac{r_l}{r_m}$

$N_{GB}=\frac{\omega_m}{\omega_l}=\frac{r_l}{r_m}=\frac{n_l}{n_m}$

---

#### Torque

- Potencia transmitida:

$\mathbb{P}=T_m \omega_m=T_l \omega_l$

- Relación de velocidades y torque:

$\frac{\omega_m}{\omega_l}=\frac{T_l}{T_m}$

---

#### Resultado

$N_{GB}=\frac{\omega_m}{\omega_l}=\frac{r_l}{r_m}=\frac{n_l}{n_m}=\frac{T_l}{T_m}$

**NOTA:** EL TORQUE QUE ESTA GENERANDO LA RUEDA MOTRIZ ES DIFERENTE AL TORQUE QUE EXPERIMENTA LA CARGA

### Simulaciones 

Simulink  

![Figura de prueba](IMAGES/simulink.png)

Simscape Multibody

![Figura de prueba](IMAGES/multibody.png) 

### Inercia reflejada
---

Acople directo: Motor, eje y carga:  

$T_m = J_{load} \, \ddot{\theta}_m$

---

Sistema de engranajes: Motor, sistema de engranajes y carga:  

$T_l = J_{load} \, \ddot{\theta}_l$  

$\dfrac{r_l}{r_m} T_m = J_{load} \, \ddot{\theta}_l$  

Si se usa la relación de desplazamiento tangencial:   
$r_l \theta_l = r_m \theta_m$  

Obteniendo:  
$r_l \ddot{\theta}_l = r_m \ddot{\theta}_m$

$r_l \theta_l = r_m \theta_m$

Reemplazando:

$\dfrac{r_l}{r_m} T_m = J_{load} \, \dfrac{r_m}{r_l} \ddot{\theta}_m$  

Despejando:

$T_m = J_{load} \left( \dfrac{r_m}{r_l} \right)^2 \ddot{\theta}_m$

**Inercia reflejada**
$= J_{load} \, \dfrac{1}{N_{GB}^2} \ddot{\theta}_m$
---
### Torque reflejado 

De la relación dada por la potencia:    

$\frac{\omega_m}{\omega_l} = \frac{T_l}{T_m}$

$T_m = \frac{\omega_l}{\omega_m} T_l$

**Torque reflejado= $\quad = \frac{T_l}{N_{GB}}$**

### Eficiencia

Relación de salida y entrada  

$\quad P = T \cdot \omega$

$\eta = \frac{P_{output}}{P_{input}}$

$T_l \, \omega_l = \eta \, T_m \, \omega_m$

$T_m = \frac{T_l}{\eta \, N_{GB}}$

$J_{ref} = \frac{J_{load}}{\eta \, N_{GB}^2}$

Se debe tener en cuenta que los engranajes no son ideales, tienen una eficiencia puesto que se enfrentan a perdidas en cuanto a la fricción, el acople o demás, esta fricción la da en el fabricante, existen cajas desde 90 o hasta 95% de eficiencia. 

**PARA TODO EL DIMENSIONAMIENTO DEL MOTOR, SE CONOCE LA INERCIA TOTAL:**  

$J_{total} = J_m + J_{\text{on motor shaft}} + J_{ref}$    

$J_m$: Inercia ejer motor.  

$J_{\text{on motor shaft}}$: Inercia acople y transmisión.  

$J_{ref}$: Inercia reflejado.  

---
### Ejemplo

#### 1. 
![Figura de prueba](IMAGES/motor.png)   

$J_\text{total} = J_m + J_\text{on motor shaft} + J_\text{ref}$

$J_\text{on motor shaft} = J_\text{coupling} + J_\text{mg}$

$J_\text{ref} = \frac{1}{\eta N_\text{GB}^2} \left[ J_\text{lg} + J_\text{load} \right]$

$J_\text{total} = J_m + J_\text{coupling} + J_\text{mg} + \frac{1}{\eta N_\text{GB}^2} \left[ J_\text{lg} + J_\text{load} \right]$

![Figura de prueba](IMAGES/bloques.png)

#### 2.
El Sistema en la figura usa un engranaje PN023 de Apex Dynamics. Este tiene 5:1 de relación, 0,15 Kg − cm2 reflejado a la entrada y 97% de eficiencia. El motor es un Quantum QB02301 NEMA tamaño 23 de Allied Motion Technologies. Este tiene 1,5x10−5 Kg − m2 de inercia en el rotor. Si la inercia de la carga es 10x10−4 Kg − m2. Encuentre la relación de inercia.  

![Figura de prueba](IMAGES/ejemplo.png)  

$$
J_{\text{load} \rightarrow M} = \frac{J_{\text{load}}}{\eta N_{\text{GB}}^2}
= \frac{10 \times 10^{-4}}{0.97 \cdot 5^2}
= 4.124 \times 10^{-5} \ \text{kg·m}^2
$$

$$
J_R = \frac{J_{\text{on motor shaft}} + J_{\text{load} \rightarrow M} + J_{\text{GB} \rightarrow M}}{J_m}
= \frac{4.124 \times 10^{-5} + 0.15 \times 10^{-4}}{1.5 \times 10^{-5}}
= 3.75
$$


### Relación de inercia

Los relaciones de transmisión y de las caracteristicas de los mecanismos, estan dadas en terminos de relación d einercia, es decir el porcentaje de incercia total que tiene que mover el motor con respecto a la incercia del motor, y con estas se logra reconocer si se esta lejos o cerca de el valor que puede mover el motor. En la práctica, la relación de inercia permite definir el motor que cumpla con los requqerimientos necesarios, esto a traves de dos rangos que se presentan en la tabla a continuacióm.   

$$
J_R = \frac{J_{\text{on motor shaft}} + J_{\text{ref}}}{J_m}
$$

$$J_R = \frac{J_{\text{on motor shaft}} + J_{\text{load} \rightarrow M} + J_{\text{GB} \rightarrow M}}{J_m}$$  

| Relación inercia | Rango      | Casos                                               | Posibles problemas                        |
|------------------|------------|-----------------------------------------------------|-------------------------------------------|
| Baja             | 1 o 2      | Movimientos rápidos, frecuentes paradas y arranques | Motor sobredimensionado                   |
| Alta             | Mayor a 10 | No es importante dinámicas rápidas                 | Baja eficiencia o Torque insuficiente     |

Cuando se habla de movimiento rápidos, se refiere a que las ruedas tienen una diferencia pequeña, entre si, por lo que los movimientos van a responder más rápido. Y cuando se refiere a baja eficiencia, se puede interpretar que el motor se esta quedando corto respecto a sus necesidades. 

En conclusión lo recomendable es tener una relación de inercia menor o igual a 5 y claramente, mayor a 2. 
##
### Polea-Correa  

Este mecanismo convierte moviemiento ortacional en movimiento rotacional, sin embargo, dependiendo del tamaño de las poleas se tiene ventaja mecánica. Estas pueden ser lisas, dentadas o sistemas de cadena, y dependiendo del tamaño de la carga se obtiene el tipo de cadena a usar. 

- **Relación de transmisión**:  

$$V_{tangential} = \omega_{ip} \cdot r_{ip} = \omega_{lp} \cdot r_{lp}$$

$$
N_{BP} = \frac{\omega_{ip}}{\omega_{lp}} = \frac{r_{lp}}{r_{ip}}
$$

La prinicpal diferencia con un sistema de engranajes es que en este, las poleas giran hacia la misma dirección. 

### Simulaciones

Simulink  

![Figura de prueba](IMAGES/poleas.png)

Simscape Multibody

![Figura de prueba](IMAGES/poleamultibody.png) 

### Inercia reflejada  

$$J_{trans_{ref}}=J_{IP}+J_{belt\rightarrow in}+J_{LP\rightarrow in}+J_{load\rightarrow in}+J_{C2\rightarrow in}$$

$$=J_{IP}+\left(\frac{W_{belt}}{g\cdot\eta}\right)\cdot r_{ip}^2+\frac{1}{\eta N_{BP}^2}(J_{LP}+J_{load}+J_{C2})$$  

Todos los elementos que componene esta ecuación responden a una relación de transmisión, excepto la correa, por lo tanto su inercia reflejada se expresa de la siguiente manera: 

$$J=mr^2$$

Sustituyendo $W_{belt}=mg$ y $r=r_{ip}$:

$$J_{belt\rightarrow in}=\frac{W_{belt}}{g\cdot\eta}\cdot r_{ip}^2$$

### Torque de carga   

$$T_{load\rightarrow in}=\frac{T_{ext}}{\eta N_{BP}}$$

## Ejercicios adicionales 
### 1. 
Un sistema utiliza un engranaje con una relación de 8:1, una inercia reflejada a la entrada de 0.25 kg·cm² y una eficiencia del 95%. El motor tiene una inercia del rotor de 2×10⁻⁵ kg·m², y la inercia de la carga es de 5×10⁻⁴ kg·m².
Encuentra la relación de inercia $J_R$.

 **Datos:**
- $N_{\text{GB}} = 8$
- $\eta = 0.95$
- $J_{\text{GB} \rightarrow M} = 0.25 \ \text{kg·cm}^2 = 0.25 \times 10^{-4} \ \text{kg·m}^2$
- $J_m = 2 \times 10^{-5} \ \text{kg·m}^2$
- $J_{\text{load}} = 5 \times 10^{-4} \ \text{kg·m}^2$

**1. Inercia reflejada de la carga al motor:**

$$
J_{\text{load} \rightarrow M} = \frac{J_{\text{load}}}{\eta N_{\text{GB}}^2}
= \frac{5 \times 10^{-4}}{0.95 \cdot 8^2}
= \frac{5 \times 10^{-4}}{60.8}
= 8.22 \times 10^{-6} \ \text{kg·m}^2
$$

**2. Relación de inercia total:**

$$
J_R = \frac{J_{\text{on motor shaft}} + J_{\text{load} \rightarrow M} + J_{\text{GB} \rightarrow M}}{J_m}
= \frac{0.25 \times 10^{-4} + 8.22 \times 10^{-6}}{2 \times 10^{-5}} 
= \frac{3.322 \times 10^{-5}}{2 \times 10^{-5}} 
= 1.66
$$

### 2.  

Se tiene un reductor con relación de 4:1, eficiencia del 90%, y una inercia reflejada a la entrada de 0.10 kg·cm². El motor tiene una inercia de 1×10⁻⁵ kg·m² y la inercia de la carga es 2×10⁻³ kg·m².
Calcula la inercia reflejada a la entrada del motor y la relación de inercia $J_R$.   

**Datos:**
- $N_{\text{GB}} = 4$
- $\eta = 0.90$
- $J_{\text{GB} \rightarrow M} = 0.10 \times 10^{-4} \ \text{kg·m}^2$
- $J_m = 1 \times 10^{-5} \ \text{kg·m}^2$
- $J_{\text{load}} = 2 \times 10^{-3} \ \text{kg·m}^2$

**1. Inercia reflejada:**

$$
J_{\text{load} \rightarrow M} = \frac{2 \times 10^{-3}}{0.90 \cdot 4^2}
= \frac{2 \times 10^{-3}}{14.4}
= 1.39 \times 10^{-4} \ \text{kg·m}^2
$$

**2. Relación de inercia:**

$$
J_R = \frac{0.18 \times 10^{-4} + 8.33 \times 10^{-6}}{2.5 \times 10^{-5}}
= \frac{2.633 \times 10^{-5}}{2.5 \times 10^{-5}}
= 1.05
$$




## Comparación de Transmisiones  
| Tipo          | Ventajas                     | Desventajas               |  
|---------------|-----------------------------|---------------------------|  
| Engranajes    | Alta precisión               | Costo elevado             |  
| Polea-Correa  | Silenciosa                   | Deslizamiento posible     |  



## Conclusiones
- El diseño de transmisiones requiere equilibrar torque, inercia y eficiencia.  
- La relación de transmisión es crítica para reflejar correctamente cargas al motor.  
- Simulaciones (e.g., Simscape) son herramientas esenciales para validar diseños.  



## Referencias
1. Universidad ECCI. *Control de Movimiento*. 

