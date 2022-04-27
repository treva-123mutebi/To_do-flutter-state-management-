# Todos

Implemented state management using [Bloc](https://pub.dev/packages/flutter_bloc) and [Get](https://pub.dev/packages/get) to compare ease of use and maintainance of flutter apps.

[Get](https://pub.dev/packages/get) uses less code and avoids a lot of boiler plate code if compared to [Bloc](https://pub.dev/packages/flutter_bloc).

compare code @ [diff@8a3707a....c96003f](https://github.com/vemarav/flutter_todo/compare/8a3707ad96f0554d452f963004aba123c6bdc247...c96003f753eaf944d9d181959578203c16cf39b7)

demo
--
<img src="https://user-images.githubusercontent.com/17309962/165533855-9e39b1ed-999e-41ae-ac60-70e65c6e9e84.png" width="400" />


State management using [Bloc](https://pub.dev/packages/flutter_bloc)
--

```dart
import 'package:flutter_bloc/flutter_bloc.dart';
import 'package:todos/todo.dart';

export 'package:todos/todo.dart';

enum Type { add, remove, update }

class TodoEvent {
  final Type type;
  final Todo todo;

  const TodoEvent(this.type, this.todo);
}

class TodoBloc extends Bloc<TodoEvent, List<Todo>> {
  TodoBloc() : super([]) {
    on(addEvent);
  }

  void addEvent(TodoEvent event, emit) {
    final List<Todo> todos = state; // state is []
    final Todo todo = event.todo;

    switch (event.type) {
      case Type.add:
        todos.add(todo);
        emit(List<Todo>.from(todos));
        break;
      case Type.remove:
        todos.remove(todo);
        emit(List<Todo>.from(todos));
        break;
      case Type.update:
        final index = todos.indexOf(todo);
        todos[index] = todo;
        emit(List<Todo>.from(todos));
        break;
    }
  }
}
``` 
 
<br>

State management using [Get](https://pub.dev/packages/get)
--

```dart
import 'package:get/get.dart';
import 'package:todos/todo.dart';

export 'package:todos/todo.dart';

class TodoController extends GetxController {
  List<Todo> todos = List<Todo>.from([]).obs;

  add(Todo todo) => todos.add(todo);
  remove(Todo todo) => todos.remove(todo);
  modity(Todo todo) {
    int index = todos.indexOf(todo);
    todos[index] = todo;
  }
}
```
