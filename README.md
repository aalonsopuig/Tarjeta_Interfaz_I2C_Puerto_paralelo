<html>

<head>
<meta http-equiv="Content-Language" content="es">
<meta name="GENERATOR" content="Microsoft FrontPage 4.0">
<meta name="ProgId" content="FrontPage.Editor.Document">
</head>




<font size="4"><b><i>Tarjeta interface KI<sup>2</sup>C para
      comunicaciones entre&nbsp;<br>
      Puerto Paralelo y Bus I<sup>2</sup>C.&nbsp;</i></b></font>
      <p>Por Alejandro Alonso Puig<br>
      Noviembre 2.003<br>
 
 
<hr>
<p align="justify"><br>
A continuación se muestra la tarjeta interface KI<sup>2</sup>C que permite
acceder al bus I<sup>2</sup>C desde el puerto paralelo de un PC. Dicha tarjeta
está desarrollada tomando como base la tarjeta K8000 de Velleman y es
compatible con su software de control.</p>
<p align="justify">El objetivo de esta económica tarjeta (9 €) es hacer más
accesible el bus I<sup>2</sup>C a todos los bolsillos. Permite además
implementar soluciones en las que los dispositivos del robot sean controlados
por bus I<sup>2</sup>C&nbsp; desde sistemas empotrados y PCs con puerto
paralelo.</p>
<p align="center"><img border="0" src="KI2C.gif" width="436" height="355"></p>
<p align="justify"><u><b><i>Componentes</i></b></u></p>
<p align="justify">Los componentes requeridos para la fabricación de dicha
tarjeta son los siguiente:</p>
<ul>
  <li>
    <p align="justify">1 Placa de circuito impreso&nbsp;</li>
  <li>
    <p align="justify">3 Optoacopladores de alta velocidad 6N136 (para
    protección del puerto paralelo del PC)</li>
  <li>
    <p align="justify">3 Zócalos de 8 pines (para los optoacopladores)</li>
  <li>
    <p align="justify">1 Circuito Integrado 74LS125 para adecuación de la señal</li>
  <li>
    <p align="justify">1 Zócalo de 14 pines para el 74LS125&nbsp;</li>
  <li>
    <p align="justify">1 Diodo led amarillo (para &quot;ver&quot; los pulsos de
    reloj)</li>
  <li>
    <p align="justify">1 Diodo led verde (para &quot;ver&quot; las
    transferencias de datos)</li>
  <li>
    <p align="justify">1 Diodo led de cualquier color (como indicador de módulo
    encendido)</li>
  <li>
    <p align="justify">1 Regulador de tensión 78L05 (Para asegurar el correcto
    voltaje)</li>
  <li>
    <p align="justify">Barrera de 3 pines con puente (para switchear entre
    utilizar la tensión entregada por el regulador o directamente la tensión
    proveniente del exterior)&nbsp;</li>
  <li>
    <p align="justify">7 resistencias de 4,7Kohm (1/4W)</li>
  <li>
    <p align="justify">3 resistencias de 150ohm (1/4W)</li>
  <li>
    <p align="justify">1 resistencia de 220ohm (1/4W)</li>
  <li>
    <p align="justify">1 resistencia de 330ohm (1/4W)</li>
  <li>
    <p align="justify">1 Conector DB25 macho codado</li>
  <li>
    <p align="justify">2 clemas para circuito impreso pequeñas</li>
</ul>
<p align="justify">El valor de todos los componentes en Espa�a a la fecha del
desarrollo de este informe ha sido de 9 €</p>
<p align="justify">&nbsp;</p>
<p align="justify"><i><u><b>El circuito</b></u></i></p>
<p align="justify">El circuito es muy básico. Consta fundamentalmente de 3
optoacopladores de alta velocidad que aíslan el puerto paralelo de los demás
circuitos para evitar que posibles fallos en los mismos puedan dañar el puerto
paralelo. Se utiliza un optoacoplador para el envío de la señal de reloj (SCL)
del PC al bus I<sup>2</sup>C&nbsp; y dos optoacopladores para los datos (uno
para el envío y otro para la recepción).</p>
<p align="justify">Para la adecuación de la señal se utiliza el circuito
74LS125, que es un cuádruple buffer triestado.</p>
<p align="justify">El software en el PC envía la señal de reloj I<sup>2</sup>C
a través del pin 17 del puerto paralelo (<span style="text-decoration: overline">Select
In</span>), envía los datos a través del pin 14 (<span style="text-decoration: overline">Auto
Feed</span>) y los recibe a través del pin 13 (Select). Ha de tenerse en cuenta
que con esta configuración no es posible detectar si un slave a detenido la
señal de reloj, cosa que ocurre en ocasiones si necesita tiempo adicional para
llevar a cabo alguna acción. Por ello se deberá tener esto en cuenta
utilizando temporizadores adecuados.</p>
<p align="justify">El led amarillo (CLK) mostrará la actividad de la señal de
reloj, mientras que el led verde (DATA) mostrará la actividad de transferencia
de datos, en un sentido o en otro.</p>
<p align="justify">El circuito dispone de un regulador de tensión a 5v. La
utilización o no de dicho regulador se puede llevar a cabo mediante el puente
de pines. Deberá seleccionarse el uso del regulador cuando el voltaje utilizado
sea superior a 5 v y deberá desactivarse si se utiliza un voltaje de 5 voltios.</p>
<p align="justify">El circuito ya dispone de las resistencias PullUp necesarias
en todo bus I<sup>2</sup>C.&nbsp;</p>
<p align="justify">Ha de tenerse en cuenta que la conexión de dispositivos I<sup>2</sup>C&nbsp;
se ha de hacer no solo con las líneas SCL y SDA, sino también con las masas
para que las referencias de nivel bajo sean las mismas.</p>
<p align="justify">&nbsp;</p>
<ul>
  <li>
    <p align="justify"><a href="KI2CSch.png">Imagen del Esquema electrónico</a>
    <font size="1">(.PNG 24 kb)</font></li>
  <li>
    <p align="justify"><a href="KI2Csch.zip">Esquema electrónico y PCB en formato
    Eagle</a><font size="2">  </font><font size="1">(.ZIP 40 kb)</font></li>
</ul>
<p align="justify">&nbsp;</p>
<p align="justify"><b><i><u>Software</u></i></b></p>
<p align="justify">Para la utilización del interface desde el PC se pueden
utilizar las librerías escritas para la tarjeta K8000 de Velleman para
diferentes lenguajes de programación y sistemas operativos.</p>
<p align="justify">Para más información sobre las librerías y su manejo, así
como para ver un ejemplo de utilización de este tipo de tarjeta, se puede
acceder al trabajo del autor: <a href="https://github.com/aalonsopuig/Servidor_eco_I2C.git">Servidos de eco I2C</a>


</body>

</html>
