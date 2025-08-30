# Síntese de um Supervisor para o Problema do Gato e do Rato Usando Supremica


* Imagine uma torre com 5 salas conectadas em um ciclo (Sala 1 → Sala 2 → Sala 3 → Sala 4 → Sala 5 → Sala 1). Há um gato e um rato que se movem livremente entre as salas. Sem controle:

<p align="center">
  <img src="https://github.com/Danilo0liveira/CatRat/blob/main/images/plant_automaton_spec.jpg?raw=true" alt="Logo" width="400"/>
</p>

<p align="center">Figura 01: Representação Das Salas</p>


* O gato pode entrar em qualquer sala adjacente, nos qual os **Eventos: move_gato_esquerda, move_gato_direita**

* O rato faz o mesmo com os **Eventos: move_rato_esquerda, move_rato_direita**.

* O gato não deve entrar na sala onde o rato está. Se isso acontecer o gato irá comer o rato (ou haverá uma "colisão" ou estado perigoso). Além disso, o sistema deve ser não bloqueante (não deve travar) e permitir o máximo de liberdade ao gato e ao rato.


<p align="center">
  <img src="https://github.com/Danilo0liveira/CatRat/blob/main/images/plant_automaton.jpg?raw=true" alt="Logo" width="400"/>
</p>

<p align="center">Figura 02: Representação Da Planta Com Gato e Rato</p>

* Com a Planta original o problema torna-se incontrolável, devido a presença dos eventos de movimento do rato, é impossível evitar com que o rato chegue na sala em que o gato está presente. Portanto, para tornar o problema controlável, é preciso a adição de elementos novos a planta. Nesse caso, foi adicionado uma barreira física controlada: portas. Com elas, é possível controlar indiretamente o movimento do rato evitando, assim, a presença dos dos animais na mesma sala.

<p align="center">
  <img src="https://github.com/Danilo0liveira/CatRat/blob/main/images/new_plant_automaton.jpg?raw=true" alt="Logo" width="400"/>
</p>

<p align="center">Figura 03: Nova Representação Da Planta Com Gato e Rato</p>

* Na Figura 04 é apresentada o novo autômato do gato. Nesse modelo, foi adicionado um estado transicional entre as salas: **Door23, Door34, Door45, Doo50**. Portanto, antes mesmo do gato ou rato mover de sala, é preciso que ele passe pela porta. Esta pode estar aberta ou fechada. Nessa representação, entre as salas 1 e 2 não há portas.

* Para que o gato mova-se de uma sala para uma porta dele deve acionar um dos eventos: **GatoR, GatoL**.

* Para que o gato mova-se de uma porta para uma sala adiante, ele deve acionar um dos eventos: **DoorIsClosedLGato, DoorIsOpenRGato**

* Para que o rato mova-se de uma sala para uma porta dele deve acionar um dos eventos: **RatoR, RatoL**.

* Para que o gato mova-se de uma porta para uma sala adiante, ele deve acionar um dos eventos: **DoorIsClosedL, DoorIsOpenR**

* Nessa composição, os eventos controláveis são: **DoorIsClosedLGato, DoorIsOpenRGato**, **DoorIsClosedL, DoorIsOpenR**, **GatoR, GatoL**

* Nessa composição, os eventos não controláveis são: **RatoR, RatoL**.

<p align="center">
  <img src="https://github.com/Danilo0liveira/CatRat/blob/main/images/new_gato_automaton.jpg?raw=true" alt="Logo" width="400"/>
</p>

<p align="center">Figura 04: Nova Representação do Gato</p>

<p align="center">
  <img src="https://github.com/Danilo0liveira/CatRat/blob/main/images/new_rat_automaton.jpg?raw=true" alt="Logo" width="400"/>
</p>

<p align="center">Figura 05: Nova Representação do Rato</p>

* Para realização da planta, foi feita a composição em paralelo dos autômatos do Gato e do Rato. Na Figura 06 é apresentado todos os estados desta composição, nela foi marcado os estados indesejáveis: Gato e Rato na mesma sala e Gato e Rato na mesma porta.

<p align="center">
  <img src="https://github.com/Danilo0liveira/CatRat/blob/main/images/supremica_new_plant_automaton.jpg?raw=true" alt="Logo" width="400"/>
</p>

<p align="center">Figura 06: Nova Representação do Rato</p>

* Com a planta e as restrições dos estados proibidos, foi feita a sintese do supervisório da planta excluindo os estados indesejáveis.

<p align="center">
  <img src="https://github.com/Danilo0liveira/CatRat/blob/main/images/analyzer.jpg?raw=true" alt="Logo" width="400"/>
</p>

<p align="center">Figura 07: Nova Representação do Rato</p>

# Funcionamento do Supervisor

* Na Figura 08 é apresentada a simulação no estado em que o gato está presenta na Sala 2 e o rato está presente na Porta 23. Nota-se que, os eventos que permitiram a passagem do rato estão desativados. Assim, indicando que a porta está fechada.

<p align="center">
  <img src="https://github.com/Danilo0liveira/CatRat/blob/main/images/gatosala2_ratoporta23.jpg?raw=true" alt="Logo" width="800"height="200"/>
</p>

<p align="center">Figura 08: Simulação Estado 0</p>

* Na Figura 09 é apresentada a simulação no estado em que o gato está presenta na Sala 1 e o rato está presente na Porta 23. Nota-se que, os eventos que permitiram a passagem do rato estão desativados. Assim, indicando que a porta está fechada.

<p align="center">
  <img src="https://github.com/Danilo0liveira/CatRat/blob/main/images/gatosala1_ratoporta23.jpg?raw=true" alt="Logo" width="800"height="200"/>
</p>

<p align="center">Figura 09: Simulação Estado 1</p>

* Na Figura 10 é apresentada a simulação no estado em que o gato está presenta na Sala 5 e o rato está presente na Porta 23. Nota-se que, os eventos que permitiram a passagem do rato estão ativados. Assim, indicando que a porta está aberta.

<p align="center">
  <img src="https://github.com/Danilo0liveira/CatRat/blob/main/images/gatosala5_ratoporta23.jpg?raw=true" alt="Logo"  width="800"height="200"/>
</p>

<p align="center">Figura 10:  Simulação Estado 2</p>


* Na Figura 11 é apresentada a simulação no estado em que o gato está presenta na Sala 5 e o rato está presente na Porta 50. Nota-se que, os eventos que permitiram a passagem do rato estão desativados. Assim, indicando que a porta está fechada.

<p align="center">
  <img src="https://github.com/Danilo0liveira/CatRat/blob/main/images/gatosala5_ratoporta50.jpg?raw=true" alt="Logo"  width="800"height="200"/>
</p>


<p align="center">Figura 11:  Simulação Estado 3</p>

# Link para o vídeo do YouTube

https://youtu.be/y9Id18Df5ZI

