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

### Sumador
