## Exemplos de sintaxe
>Todos os código apresentados aqui podem ser testados no [DartPad](https://dartpad.dartlang.org/dart).

### Operadores com reconhecimento de nulo no Dart

#### Operador `??`
Usado quando o objetivo é validar se uma expressão é nula, retornar seu resultado se a validação for `false` e retornar outra expressão caso a primeira seja `true`.
```dart
void main() {
  var exp;
  print(exp ?? "está nula"); // está nula  
  
  exp = "algum texto";
  print(exp ?? "está nula"); // algum texto
  
  exp = null;
  print(exp ?? "está nula"); // está nula  
}
```

#### Operador `??=`
Usado quando o objetivo é atribuir um valor validando se o objeto que receberá este valor é nulo. Se for nulo receberá o novo valor, caso não seja, manterá o valor previamente contido nele.
```dart
void main() {
  var obj;
  obj ??= "Valor 1";
  print(obj); // Valor 1
  
  obj ??= "Valor 2";
  print(obj); // Valor 1
  
  obj = null;
  obj ??= "Valor 2";
  print(obj); // Valor 2
}
```

#### Operador `?.`
Usado quando você deseja chamar um método/getter em um objeto se esse objeto não for nulo (caso contrário, retorne nulo).
```dart
void main() {
  var pai = Pai();   
  print(pai?.filho?.mae?.nome); // null
  
  var pai2 = Pai();  
  var filho2 = Filho();
  pai2.filho = filho2;
  print(pai2?.filho?.mae?.nome); // null
  
  var pai3 = Pai();  
  var filho3 = Filho();
  var mae3 = Mae("Joana");
  filho3.mae = mae3;
  pai3.filho = filho3;
  print(pai3?.filho?.mae?.nome); // Joana
}

class Pai { 
  Filho filho;
}

class Filho {
  Mae mae;
}

class Mae {
  String nome;
  Mae(this.nome);
}
```

#### Operador `...?`
Usado quando o objetivo unir listas validando se a lista anterior não é nula.
```dart
void main() {
  List lista1 = [1, 2, 3, 4, 5];
  List lista2 = [6, 7, 8, 9, 10];
    
  List numeros = [...?lista1, ...?lista2];
  print(numeros); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
  
  List listaNula;
  print(listaNula); // null
  
  List novosNumeros = [...?listaNula, ...?numeros];
  print(novosNumeros); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
  
  List outrosNovosNumeros = [...listaNula, ...?numeros];
  print(outrosNovosNumeros); // Ocorre erro pois "listaNula" não é iterável
}
}
```

---
#### Referência:
https://medium.com/@thinkdigitalsoftware/null-aware-operators-in-dart-53ffb8ae80bb
