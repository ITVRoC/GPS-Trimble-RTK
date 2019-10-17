# Applanix POS LV V5 125



Applanix POS LV V5 125 é um sistema que permite a localização em tempo real de um veículo até em locais com pouco ou nenhum sinal de GPS. 
O sistema possui 3 sensores principais: 

![image](https://user-images.githubusercontent.com/44469467/67007442-c79dbf00-f0bd-11e9-97e1-a38ad9a7f1f2.png)

### IMU

Sensor de 6 graus de liberdade (3 de posições 3 de orientação) que contém saidas velocidade e ângulos.



### DMI 

É basicamente um encoder que gera 4096 pulsos por rotação e pode ser encaixado em alguma roda do veículo. Com isto, é possível  calcular a distância total percorrida considerando 
o diâmetro da roda no qual foi instalado.


![image](https://user-images.githubusercontent.com/44469467/67007503-f025b900-f0bd-11e9-931f-a35daaeb0570.png)


### Receptores GPS

A CPU do Applanix possui entrada para dois receptores GNSS (Primário e secundário). A utilização dos dois receptores se torna necessária devido ao 
seistema GAMS (GNSS Azimuth Measurement Subsystem). Este sistema aumenta e mantém a precisão da rota no modo de navegação levando a um erro de 0.015 graus 


# Princípio de funcionamento

A CPU roda um algoritmo de navegação que resolve as equações de movimento de Newton através dos dados colhidos da IMU. Em seguida, é aplicado um 
filtro de Kalman com os sinais do GPS, GAMS e DMI. Caso algum sensor esteja em falha, a CPU consegue detectar e alterar o programa
para otimizar o algoritimo.

![image](https://user-images.githubusercontent.com/44469467/67005805-d84c3600-f0b9-11e9-9c70-74eb155a7380.png)

Com o sistema completo implementado, as seguintes saídas são providas:

* Posição
* Velocidade
* Altitude
* Aceleração
* Distância total
* Erro 
* Variação Angular

# Observações 

A implementação em robôs móveis pequenos é bastante dificultada pois os componentes do sistema são grandes e pesados. Além disso
O Applanix não possui correções RTK nativas, logo, visando o máximo desempenho na localização, é necessário que haja uma fonte de correções RTK externa e que o sistema GAMS esteja implementado
Sendo que para utilizar o sistema GAMS é necessário que haja um espaçamento de no mínimo 1,5 metros entre as antenas e alta velocidade para calibração do mesmo (60km/h).

Quando completamente implementado com GAMS e correções RTK, o sistema possuirá erros de posição, velocidade e altitude na casa de centímetros.
