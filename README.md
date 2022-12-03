# Sorting-Station

## Descrição do problema:

Neste projeto, é implementada uma aplicação em linguagem Ladder realizada com auxílio do Software [Siemens's TIA Portal V15](https://support.industry.siemens.com/cs/document/109745155/simatic-step-7-including-plcsim-v13-sp2-trial-download?dti=0&lc=en-WW). E em seguida, a simulação do funcionamento do código em um CLP junto do ambiente onde será tratada a problemática é feita utilizando uma das cenas predefinidas do Software [Factory IO](https://factoryio.com/). O problema em questão consiste sem separar objetos em função de suas cores. Uma visão geral da cena é mostrada abaixo.

<p align="center">
<img src=https://user-images.githubusercontent.com/44499744/205458709-0000163b-bcad-43c1-83a8-5ec7175f25d3.png>
</p>

<p align="center"> 
<b>Figura 1:</b> Sorting Station.
</p>

As cores possíveis para esse caso são: Azul, Verde e Cinza. As mesmas são identificadas por um sensor que vai acionar os separadores para garantir que cada objeto vá para a rampa devida de separação. Abaixo é mostrado o sensor.

<p align="center">
<img src=https://user-images.githubusercontent.com/44499744/205458948-db59bc4a-4913-4cf4-8f6d-970c48071299.png>
</p>

<p align="center"> 
<b>Figura 2:</b> Sensor.
</p>

O processo é iniciado e interrompido pressionando respectivamente os botões verde e vermelho presentes no painel do CLP. Baixo é mostrado o painel.

<p align="center">
<img src=https://user-images.githubusercontent.com/44499744/205459343-26c44644-0b43-4c8b-a7f9-e5be8edbf655.png>
</p>

<p align="center"> 
<b>Figura 3:</b> Painel do CLP.
</p>

## Descrição da implementação lógica Realizada:

A implementação realizada no [Siemens's TIA Portal V15](https://support.industry.siemens.com/cs/document/109745155/simatic-step-7-including-plcsim-v13-sp2-trial-download?dti=0&lc=en-WW) pode ser descrita em duas partes. A primeira consiste no acionamento e controle do sistema como um todo. Quando o usuário pressiona o botão de *start*, o sistema como um todo é energizado e não para até que o segundo botão chamado *stop* seja pressionado. 

A segunda parte, consiste em 3 blocos lógicos, de forma que cada um é responsável por acionar um dos três separadores para cada uma das cores de objetos que estão passando na esteira. Quando o sensor detecta a cor de objeto, que no problema em questão é traduzido como um *valor inteiro*, um timer é acionado para garantir a sincronia entre a posição da peça na esteira e a reação do separador, por fim, o mesmo retorna para sua posição inicial após um segundo. A tabela com a relação *Inteiro* --> *Cor* pode ser vizualida abaixo.

| Inteiro     | Cor |
| :--------:  | :-------:|
| 1           |  Azul    |
| 4           |  Verde   |
| 7           |  Cinza   |

A visão esquemática dos blocos lógicos podem ser vizualidas [aqui](https://github.com/Tayco110/Sorting-Station/files/10147304/Descricao.dos.blocos.logicos.pdf).

## Tabela de endereçamento: 

| Endereço    | Tag            | Tipo |
| :--------:  |:-------:       |:----:|
| %I0.1       | start          | Bool |
| %I0.3       | stop           | Bool |
| %ID30       | vision sensor  | DInt |
| %Q0.0       | entry conveyor | Bool |
| %Q0.2       | exit Conveyor  | Bool |
| %Q0.3       | sorter 1 turn  | Bool |
| %Q0.4       | sorter 1 belt  | Bool |
| %Q0.5       | sorter 2 turn  | Bool |
| %Q0.6       | sorter 2 belt  | Bool |
| %Q0.7       | sorter 3 turn  | Bool |
| %Q1.0       | sorter 3 belt  | Bool |
| %Q1.4       | timmer 1 valve | Bool |
| %Q1.5       | timmer 2 valve | Bool |
| %Q1.6       | timmer 3 valve | Bool |

## Resultado:

O ```.gif``` abaixo mostra o processo automatizado em execução.
