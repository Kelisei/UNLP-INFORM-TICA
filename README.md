# Algoritmos Utiles:
Este es un repositorio donde pienso guardar todos los algoritmos realizados durante el la carrera, por ahora solo de taller en adelante.

Si ves algún error o tenes alguna duda o sabes como hacer una función que encuentre el máximo de un dato por el que el arbol no esta ordenado mensajeame a:
.【𝓚𝓮𝓵𝓲𝓼𝓮𝓲】#6143


**Indice:** 

1. Arboles (BST)
* [Declaración](#Declaración)
* [Inserción](#Inserción)
* [Informar Simple](#Informar-Simple)
* [Función Maximo/Minimo Ordenado](#Función-Máximo-Mínimo)
* [Procedure Máximo/Mínimo](#Procedure-Máximo-Mínimo)
* [Encontrar Ordenado](#Encontrar-Ordenado)
* [Encontrar](#Encontrar)
* [Informar Acumulando](#Informar-Acumulando)
* [Informar Uno](#Informar-Uno)
* [Informar Inferior](#Informar-Inferior)
* [Informar Rango](#Informar-Rango)

Declaración
===========
```pascal
type
	arbol = ^nodo;
	nodo = record
		dato:integer;
		hi:arbol;
		hd:arbol;
	end;
```
Inserción
===========
```pascal
procedure insertar {a}(var A:arbol; n:nodo);
Begin
  if (A = nil) then
   begin
      new(A);
      A^.dato:= n; A^.HI:= nil; A^.HD:= nil;
   end
   else
    if (n.numero < A^.dato.numero) then crear(A^.HI,n)
    else crear(A^.HD,n)   
End;
```
Informar Simple
===========
```pascal
Procedure x ( a : arbol );
begin
   if ( a<> nil ) then begin
    x (a^.hi);
	writeln ('Numero de socio:',a^.dato.numero);
    x (a^.hd);
   end;
end;
```
Función Máximo Mínimo
===========
```pascal
{Cuando el arbol esta ordenado en base a lo que queremos sacar}
	function conseguirMaximo(a:arbol):integer;
	begin
		if (a = nil) then 
			conseguirMaximo:=-1
		else if (a^.hd = nil) then 
			conseguirMaximo:=a^.dato.numero
		else conseguirMaximo:=conseguirMaximo(a^.hd);
	end;
```
Procedure Máximo Mínimo
===========
```pascal
{Cuando buscamos elementos no ordenados en el arbol}
	procedure buscarMasEdad(a:arbol; var maxE:integer; var maxN:integer);
	begin
	   if ( a <> nil ) then begin
		writeln(a^.dato.numero);
		if (a^.dato.edad > maxE) then begin
			maxE:=a^.dato.edad;
			maxN:=a^.dato.numero;
		end;
		buscarMasEdad (a^.hi, maxE, maxN);
		buscarMasEdad (a^.hd, maxE, maxN);
   end;
```
Encontrar Ordenado
===========
```pascal
procedure bv (a:arbol);
var
	valor:Integer;
	function encontrar (a:arbol; v:integer):boolean;
	begin
		if (a = nil) then
			encontrar:=false
		else if (a^.dato.numero = v) then encontrar:=true
		else if (a^.dato.numero < v) then encontrar:=encontrar(a^.hd, v)
		else encontrar:=encontrar(a^.hi, v);
	end;
begin
	readln (valor);
	if (encontrar(a,valor)) then 
		writeln('encontrao numero')
	else writeln ('no ta numero');
end;
```
Encontrar
===========
```pascal
procedure bvi (a:arbol);
var
	valor:string;
	function encontrar (a:arbol; nom:string):boolean;
	begin
		if (a = nil) then
			encontrar:=false
		else encontrar:=(a^.dato.nombre = nom) or encontrar(a^.hi, nom) or encontrar(a^.hd, nom);
	end;
begin
	readln (valor);
	if (encontrar(a,valor)) then 
		writeln('encontrao nombre')
	else writeln ('no ta nombre');
end;
```
Informar Acumulando
===========
```pascal
procedure b (var a:arbol; var cantv1:integer);
var
	num:integer; 
	function total (a:arbol; num:integer):integer;
	begin
		if (a = nil) then
			total:=0
		else if (a^.dato.codigo = num) then
			total:= a^.dato.cantidad+total(a^.hd, num)
		else if (num < a^.dato.codigo) then 
			total:=total(a^.hi, num) 
		else total:=total(a^.hd, num);
	end;
begin
	readln(num);
	cantv1:=total(a,num);
	writeln('Diga un numero de producto!');
	writeln('Las ventas de ',num,' son de ',cantv1);
end;
```
Informar Uno
===========
```pascal
procedure c (var a:arbol2);
var
	num:integer;
	function total (a:arbol2; num:integer):integer;
	begin
		if (a = nil) then
			total:=0
		else begin 
			if (a^.dato.codigo = num) then
				total:=a^.dato.cantidad
			else begin
				if (num < a^.dato.codigo) then 
					total:= total(a^.hi, num) 	
				else total:= total(a^.hd, num);
			end;
		end;
	end;
begin
	writeln('Diga un numero de producto!');
	readln(num);
	writeln(total(a,num));
end;
```
Informar Inferior 
===========
```pascal
procedure informarInferior(A: arbol; legajo1: integer; legajo2: integer);
begin
  if(A <> nil) then begin
    if(A^.dato.legajo > legajo2) then
      informarInferior(A^.HI, legajo1, legajo2)
    else
      if(A^.dato.legajo >= legajo1) then begin
        write(a^.dato.legajo,'|');
        informarInferior(A^.HD, legajo1, legajo2);
        informarInferior(A^.HI, legajo1, legajo2);
      end
      else
        informarInferior(A^.HD, legajo1, legajo2); 
        {Si queremos informar al reves, deberiamos invertir los signos!}
  end;
end;
```
Informar Rango
===========
```pascal
procedure informarRango(A: arbol; legajo1: integer; legajo2: integer);
begin
  if(A <> nil) then begin
    if(A^.dato.legajo > legajo2) then
      informarRango(A^.HI, legajo1, legajo2)
    else
      if(A^.dato.legajo >= legajo1) then begin
        write(a^.dato.legajo,'|');
        informarRango(A^.HD, legajo1, legajo2);
        informarRango(A^.HI, legajo1, legajo2);
      end
      else
        informarRango(A^.HD, legajo1, legajo2);
  end;
end;
```