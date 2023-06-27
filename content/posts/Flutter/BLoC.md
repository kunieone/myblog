---
title: "BLoC"
date: 2023-06-26T15:13:42+08:00
draft: false
---

## BLoC 是什么

> Business Logic Component 就叫业务逻辑组件

## 可以做到

1. 管理状态
2. 通过事件驱动来改变状态
3. 提高复用性
4. 提高性能

```dart
import 'package:flutter_bloc/flutter_bloc.dart';

abstract class CounterEvent {}

class IncrementEvent extends CounterEvent {}

class DecrementEvent extends CounterEvent {}

class CounterBloc extends Bloc<CounterEvent, int> {
  CounterBloc(int s) : super(s) {
    on<IncrementEvent>((event, emit) => emit(state + 1));
    on<DecrementEvent>((event, emit) => emit(state - 1));
  }


  @override
  void onTransition(Transition<CounterEvent, int> transition) {
    print(
        'Current: ${transition.currentState}, Next: ${transition.nextState}, Event: ${transition.event}');
    super.onTransition(transition);
  }
}

```

1. 先声明我们的 Bloc 对应的一个抽象类事件类，然后将会改变这个 Bloc 的逻辑都写成对应的子类
2. 创建对应的 Bloc 类，继承 1. 触发他的事件 2. 这个 Bloc 状态的内部模型
3. 在构造函数中注册对应的事件触发产生的逻辑


如何使用这个 Bloc？

return 组件的的时候，在外层包裹一层：BlocProvider，将要用的Bloc 传入对应的泛型参数内