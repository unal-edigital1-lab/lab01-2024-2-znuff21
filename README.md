# Laboratorio 01. Sumador de 1 bit Juan Esteban Otavo García

## Específicación

Durante este laboratorio se analizó el código de un sumador de un bit A y un bit B completo. Dicho sumador cuenta con carrier y se comporta acorde a la siguiente tabla de verdad propuesta por el docente.

A  | B  | Cin | Out | Cout 
-- | -- | --  | --  |  --
0| 0 | 0 |0 | 0
0| 0 | 1 | 1| 0
0| 1 | 0 | 1| 0
0| 1 | 1 | 0| 1
1| 0 | 0 | 1| 0
1| 0 | 1 | 0| 1
1| 1 | 0 | 0| 1
1| 1 | 1 | 1| 1


## Entregable 1

Para la primera entrega se realizó la implementación del módulo sum1bcc_primitive en Quartus, posteriormente se analizó el código con el fin de entender todas las líneas, el código estudiado fue el siguiente: 

```verilog

module sum1bcc_primitive (A, B, Ci,Cout,S);

  input  A;
  input  B;
  input  Ci;***
  output Cout;
  output S;

  wire a_ab;
  wire x_ab;
  wire cout_t;

  and(a_ab,A,B);
  xor(x_ab,A,B);

  xor(S,x_ab,Ci);
  and(cout_t,x_ab,Ci);

  or (Cout,cout_t,a_ab);

endmodule
```

Las líneas que empiezan con la palabra input seguido del nombre de una variable permiten declarar las entradas del circuito, asímismo las líneas que empiezan con la palabra output declaran las salidas del circuito. La palabra reservada wire permite declarar los cables que serán usados para conectar las entradas y salidas del sistema.

And, or y xor son funciones que permiten conectar variables mediante compuertas lógicas.

Primero, calcula la suma parcial (x_ab) x_ab = A XOR B: Suma los bits A y B sin considerar el acarreo. Luego, calcula el acarreo parcial (a_ab): a_ab = A AND B: Determina si se genera un acarreo entre A y B. Después, suma el acarreo de entrada (S): S = x_ab XOR Ci: Suma el acarreo de entrada (Ci) al resultado parcial (x_ab). Finalmente, calcula el acarreo total (Cout): cout_t = x_ab AND Ci: Determina si el acarreo de entrada afecta la suma parcial y Cout = cout_t OR a_ab: El acarreo final es la combinación de ambos acarreos.


## Entregable 2

Adicional al módulo sum1bcc_primitive, se analizó el siguiente código

```verilog
module sum1bcc (A, B, Ci,Cout,S);

  input  A;
  input  B;
  input  Ci;
  output Cout;
  output S;

  reg [1:0] st;

  assign S = st[0];
  assign Cout = st[1];

  always @ ( * ) begin
    st  <=   A+B+Ci;
  end
  
endmodule
```

Al igual que en el código anterior, primero se define el módulo sum1bcc y se asignan sus entradas A, B y Ci y sus salidas Cout y S. Luego, se declara un registro de 2 bits (st) para almacenar el resultado completo de la suma. st[0] almacena el bit menos significativo S y st[1] almacena el bit más significativo Cout.

En el bloque always se calcula la suma. Este bloque combinacional se activa siempre que cualquier señal (en este caso, A, B, o Ci) cambie de valor. Esto se indica con always @ (*). Dentro del bloque la suma A + B + Ci se calcula y se almacena en el registro st. Finalmente, como st tiene 2 bits, puede almacenar tanto el resultado (S) como el acarreo (Cout).

Comparando los módulos sum1bcc_primitive y sum1bcc se pueden encontrar diferencias significativas en la programación que llevan para llegar al mismo resultado. Mientras que en sum1bcc se usa una suma directa (A + B + Ci), en sum1bcc_primitive se usan puertas lógicas para realizar la suma, como se explicó en el entregable anterior.

## Entregable 3

Para el entregable 3, se creó el proyecto en Quartus y se usó el módulo sum1bcc como archivo principal. Luego, se compiló usando la opción Analysis and Synthesis como se ve en la siguiente imagen.

![image](https://github.com/unal-edigital1-lab/lab01-2024-2-znuff21/blob/master/src/docs/image.png)




Luego de comprobar que el código compilara correctamente, se procedió a realizar la simulación usando el software Questa. Para la simulación, las entradas A, B y Cin se forzaron a clock con el fin de revisar los diferentes resultados y que sean correctos, la captura de pantalla de la simulación se muestra a continuación.

![image](https://github.com/unal-edigital1-lab/lab01-2024-2-znuff21/blob/master/src/docs/image%202.png)

Donde se pudo comprobar que el código para el sumador de 1 bit funciona correctamente.

Finalmente, pese a que se realizaron los pasos indicados en la guía, no fue posible verificar el funcionamiento del código en la FPGA, a continuación se muestran capturas del proceso donde se seleccionan los pines y se carga el código a la tarjeta.

![image](https://github.com/unal-edigital1-lab/lab01-2024-2-znuff21/blob/master/src/docs/image%203..png)

![image](https://github.com/unal-edigital1-lab/lab01-2024-2-znuff21/blob/master/src/docs/image%204.png)







