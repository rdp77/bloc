<p align="center">
  <img src="https://github.com/felangel/bloc/raw/master/assets/logos/hydrated_bloc.png" height="100" alt="Hydrated Bloc">
</p>

<p align="center">
  <a href="https://github.com/felangel/bloc/actions"><img src="https://github.com/felangel/bloc/actions/workflows/main.yaml/badge.svg" alt="build"></a>
  <a href="https://codecov.io/gh/felangel/bloc"><img src="https://codecov.io/gh/felangel/bloc/branch/master/graph/badge.svg" alt="codecov"></a>
  <a href="https://github.com/felangel/bloc"><img src="https://img.shields.io/github/stars/felangel/bloc.svg?style=flat&logo=github&colorB=deeppink&label=stars" alt="Star on Github"></a>
  <a href="https://flutter.dev/docs/development/data-and-backend/state-mgmt/options#bloc--rx"><img src="https://img.shields.io/badge/flutter-website-deepskyblue.svg" alt="Flutter Website"></a>
  <a href="https://github.com/Solido/awesome-flutter#standard"><img src="https://img.shields.io/badge/awesome-flutter-blue.svg?longCache=true" alt="Awesome Flutter"></a>
  <a href="https://fluttersamples.com"><img src="https://img.shields.io/badge/flutter-samples-teal.svg?longCache=true" alt="Flutter Samples"></a>
  <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/license-MIT-purple.svg" alt="License: MIT"></a>
  <a href="https://discord.gg/bloc"><img src="https://img.shields.io/discord/649708778631200778.svg?logo=discord&color=blue" alt="Discord"></a>
  <a href="https://github.com/felangel/bloc"><img src="https://tinyurl.com/bloc-library" alt="Bloc Library"></a>
</p>

An extension to [package:bloc](https://github.com/felangel/bloc) which automatically persists and restores bloc and cubit states. Built to work with [package:bloc](https://pub.dev/packages/bloc).

**Learn more at [bloclibrary.dev](https://bloclibrary.dev)!**

---

## Sponsors

Our top sponsors are shown below! [[Become a Sponsor](https://github.com/sponsors/felangel)]

<table style="background-color: white; border: 1px solid black">
    <tbody>
        <tr>
            <td align="center" style="border: 1px solid black">
                <a href="https://shorebird.dev"><img src="https://raw.githubusercontent.com/felangel/bloc/master/assets/sponsors/shorebird.png" width="225"/></a>
            </td>            
            <td align="center" style="border: 1px solid black">
                <a href="https://getstream.io/chat/flutter/tutorial/?utm_source=Github&utm_medium=Github_Repo_Content_Ad&utm_content=Developer&utm_campaign=Github_Jan2022_FlutterChat&utm_term=bloc"><img src="https://raw.githubusercontent.com/felangel/bloc/master/assets/sponsors/stream.png" width="225"/></a>
            </td>
            <td align="center" style="border: 1px solid black">
                <a href="https://rettelgame.com/"><img src="https://raw.githubusercontent.com/felangel/bloc/master/assets/sponsors/rettel.png" width="225"/></a>
            </td>
        </tr>
    </tbody>
</table>

---

## Overview

`hydrated_bloc` exports a `Storage` interface which means it can work with any storage provider. Out of the box, it comes with its own implementation: `HydratedStorage`.

`HydratedStorage` is built on top of [hive](https://pub.dev/packages/hive) for a platform-agnostic, performant storage layer. See the complete [example](https://github.com/felangel/bloc/blob/master/packages/hydrated_bloc/example) for more details.

## Usage

### Setup `HydratedStorage`

```dart
Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  HydratedBloc.storage = await HydratedStorage.build(
    storageDirectory: kIsWeb
        ? HydratedStorageDirectory.web
        : HydratedStorageDirectory((await getTemporaryDirectory()).path),
  );
  runApp(App());
}
```

### Create a HydratedCubit

```dart
class CounterCubit extends HydratedCubit<int> {
  CounterCubit() : super(0);

  void increment() => emit(state + 1);

  @override
  int fromJson(Map<String, dynamic> json) => json['value'] as int;

  @override
  Map<String, int> toJson(int state) => { 'value': state };
}
```

### Create a HydratedBloc

```dart
sealed class CounterEvent {}
final class CounterIncrementPressed extends CounterEvent {}

class CounterBloc extends HydratedBloc<CounterEvent, int> {
  CounterBloc() : super(0) {
    on<CounterIncrementPressed>((event, emit) => emit(state + 1));
  }

  @override
  int fromJson(Map<String, dynamic> json) => json['value'] as int;

  @override
  Map<String, int> toJson(int state) => { 'value': state };
}
```

Now the `CounterCubit` and `CounterBloc` will automatically persist/restore their state. We can increment the counter value, hot restart, kill the app, etc... and the previous state will be retained.

### HydratedMixin

```dart
class CounterCubit extends Cubit<int> with HydratedMixin {
  CounterCubit() : super(0) {
    hydrate(); // You must always call `hydrate` when using `HydratedMixin`
  }

  void increment() => emit(state + 1);

  @override
  int fromJson(Map<String, dynamic> json) => json['value'] as int;

  @override
  Map<String, int> toJson(int state) => { 'value': state };
}
```

## Storage Overrides

You can override the global storage instance for specific `HydratedBloc` or `HydratedCubit` instances by passing a custom storage instance via constructor.

```dart
class CounterCubit extends HydratedCubit<int> {
  CounterCubit() : super(0, storage: EncryptedStorage());

  void increment() => emit(state + 1);

  @override
  int fromJson(Map<String, dynamic> json) => json['value'] as int;

  @override
  Map<String, int> toJson(int state) => { 'value': state };
}
```

## Handling Hydration Errors

You can optionally pass a custom `onError` callback to `hydrate` in order to handle any hydration errors and/or customize the caching behavior when a hydration error occurs.

```dart
class CounterBloc extends Bloc<CounterEvent, int> with HydratedMixin {
  CounterBloc() : super(0) {
    hydrate(
      onError: (error, stackTrace) {
        // Do something in response to hydration errors.
        // Must return a `HydrationErrorBehavior` to specify whether subsequent
        // state changes should be persisted.
        return HydrationErrorBehavior.retain; // Retain the previous state.
      }
    );
  }
  ...
}
```

## Custom Storage Directory

Any `storageDirectory` can be used when creating an instance of `HydratedStorage`:

```dart
final storage = await HydratedStorage.build(
  storageDirectory: await getApplicationDocumentsDirectory(),
);
```

## Custom Hydrated Storage

If the default `HydratedStorage` doesn't meet your needs, you can always implement a custom `Storage` by simply implementing the `Storage` interface and initializing `HydratedBloc` with the custom `Storage`.

```dart
// my_hydrated_storage.dart

class MyHydratedStorage implements Storage {
  @override
  dynamic read(String key) {
    // TODO: implement read
  }

  @override
  Future<void> write(String key, dynamic value) async {
    // TODO: implement write
  }

  @override
  Future<void> delete(String key) async {
    // TODO: implement delete
  }

  @override
  Future<void> clear() async {
    // TODO: implement clear
  }
}
```

```dart
// main.dart
HydratedBloc.storage = MyHydratedStorage();
runApp(MyApp());
```

## Custom Storage Prefix

The `storagePrefix` defines the unique storage namespace for your `HydratedBloc` or `HydratedCubit`.

By default, it uses `runtimeType`, which isn't resilient to obfuscation or minification in production. If `runtimeType` changes, your saved state will be lost. This is especially relevant for web apps, where code changes frequently alter the minified `runtimeType`.

Consider overriding `storagePrefix` in production for more resilient, persistent storage.

```dart
class CounterCubit extends HydratedCubit<int> {
  CounterCubit() : super(0);

  @override
  String get storagePrefix => 'CounterCubit';
}
```

## Testing

When writing unit tests for code that uses `HydratedBloc`, it is recommended to stub the `Storage` implementation using `package:mocktail`.

```dart
import 'package:flutter_test/flutter_test.dart';
import 'package:hydrated_bloc/hydrated_bloc.dart';
import 'package:mocktail/mocktail.dart';

class MockStorage extends Mock implements Storage {}

void main() {
  late Storage storage;

  setUp(() {
    storage = MockStorage();
    when(
      () => storage.write(any(), any<dynamic>()),
    ).thenAnswer((_) async {});
    HydratedBloc.storage = storage;
  });

  // ...
}
```

You can also stub the `storage.read` API in individual tests to return cached state:

```dart
testWidgets('...', (tester) async {
  when<dynamic>(() => storage.read('$MyBloc')).thenReturn(MyState().toJson());

  // ...
});
```

## Dart Versions

- Dart 2: >= 2.14

## Maintainers

- [Felix Angelov](https://github.com/felangel)
