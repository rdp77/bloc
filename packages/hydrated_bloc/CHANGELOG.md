# 10.1.0

- feat: add `onError` and `HydrationErrorBehavior` to `hydrate` ([#4390](https://github.com/felangel/bloc/pull/4390))
- docs: improve `storagePrefix` documentation ([#4559](https://github.com/felangel/bloc/pull/4559))
- chore: update build status badge ([#4502](https://github.com/felangel/bloc/pull/4502))
- chore: update sponsors ([#4418](https://github.com/felangel/bloc/pull/4418))
- chore: update example to `flutter_bloc` v9.1.0 ([#4368](https://github.com/felangel/bloc/pull/4368))

# 10.0.0

- **BREAKING** feat!: support for `wasm` ([#4313](https://github.com/felangel/bloc/pull/4313))

  - introduces `HydratedStorageDirectory` and modifies `HydratedStorage.build` signature to use `HydratedStorageDirectory` instead of `Directory` from `dart:io`

  ```dart
  import 'package:flutter/foundation.dart';
  import 'package:flutter/material.dart';

  import 'package:flutter_bloc/flutter_bloc.dart';
  import 'package:hydrated_bloc/hydrated_bloc.dart';
  import 'package:path_provider/path_provider.dart';

  void main() async {
    WidgetsFlutterBinding.ensureInitialized();
    HydratedBloc.storage = await HydratedStorage.build(
      storageDirectory: kIsWeb
          ? HydratedStorageDirectory.web
          : HydratedStorageDirectory((await getTemporaryDirectory()).path),
    );
    runApp(const App());
  }
  ```

- feat: allow overriding storage per bloc/cubit instance ([#4314](https://github.com/felangel/bloc/pull/4314))
- feat: migrate to `package:hive_ce` (Hive Community Edition) ([#4262](https://github.com/felangel/bloc/pull/4262))
- fix: `HydratedStorage.build` should not cache instance ([#4317](https://github.com/felangel/bloc/pull/4317))
- chore: upgrade to `package:bloc v9.0.0`
- chore: bump miniumum Dart SDK version to 2.14
- chore: update sponsors
- chore: add `funding` to `pubspec.yaml` ([#4200](https://github.com/felangel/bloc/pull/4200))

# 9.1.5

- chore: update copyright year
- chore: update sponsors

# 9.1.4

- chore: update sponsors ([#4054](https://github.com/felangel/bloc/pull/4054))

# 9.1.3

- fix: `fromJson` can safely access `state` ([#4005](https://github.com/felangel/bloc/pull/4005))
- chore: add `platforms` to `pubspec.yaml` ([#3993](https://github.com/felangel/bloc/pull/3993))
- chore: upgrade to `package:mocktail` v1.0.0 ([#3919](https://github.com/felangel/bloc/pull/3919))
- chore: add `topics` to `pubspec.yaml` ([#3914](https://github.com/felangel/bloc/pull/3914))

# 9.1.2

- fix: clear HydratedStorage instance on close ([#3879](https://github.com/felangel/bloc/pull/3879))

# 9.1.1

- docs: upgrade to Dart 3 ([#3809](https://github.com/felangel/bloc/pull/3809))
- refactor: standardize analysis_options ([#3809](https://github.com/felangel/bloc/pull/3809))
- refactor: fix `unawaited` sdk constraint ([#3809](https://github.com/felangel/bloc/pull/3809))
- refactor: update sdk constraints and fix analysis warnings ([#3809](https://github.com/felangel/bloc/pull/3809))

# 9.1.0

- chore: add screenshots to `pubspec.yaml` ([#3721](https://github.com/felangel/bloc/pull/3721))
- chore: update example to Dart 2.19 ([#3720](https://github.com/felangel/bloc/pull/3720))
- chore: update to `bloc ^8.1.1` ([#3719](https://github.com/felangel/bloc/pull/3719))
- feat: add `storage.close` ([#3705](https://github.com/felangel/bloc/pull/3705))
- docs: updated docs to reflect v9.0.0 changes ([#3701](https://github.com/felangel/bloc/pull/3701))
- refactor: upgrade to Dart 2.19 ([#3699](https://github.com/felangel/bloc/pull/3699))
  - remove deprecated `invariant_booleans` lint rule

# 9.0.0

- **BREAKING**: feat!: reintroduce `HydratedBloc.storage` and remove `HydratedBlocOverrides` ([#3479](https://github.com/felangel/bloc/pull/3479))
  - upgrade to `bloc: ^8.1.0`
- fix: update `StorageNotFound` implementation for `toString` ([#3314](https://github.com/felangel/bloc/pull/3314))
- deps: upgrade to `mocktail ^0.3.0`

# 9.0.0-dev.3

- **BREAKING**: feat!: reintroduce `HydratedBloc.storage` and remove `HydratedBlocOverrides` ([#3479](https://github.com/felangel/bloc/pull/3479))
  - upgrade to `bloc: ^8.1.0`

# 9.0.0-dev.2

- fix: update `StorageNotFound` implementation for `toString` ([#3314](https://github.com/felangel/bloc/pull/3314))

# 9.0.0-dev.1

- **BREAKING**: feat!: add `createStorage` to `HydratedBlocOverrides.runZoned` ([#3240](https://github.com/felangel/bloc/pull/3240))
  - deprecate `storage` parameter in `HydratedBlocoverrides.runZoned` in favor of `createStorage`

# 8.1.0

- feat: add `storagePrefix` to support obfuscation tolerance ([#3262](https://github.com/felangel/bloc/pull/3262))
- docs: update GetStream utm tags ([#3136](https://github.com/felangel/bloc/pull/3136))
- docs: update VGV sponsors logo ([#3125](https://github.com/felangel/bloc/pull/3125))

# 8.0.0

- **BREAKING**: feat: introduce `HydratedBlocOverrides` API ([#2947](https://github.com/felangel/bloc/pull/2947))
  - `HydratedBloc.storage` removed in favor of `HydratedBlocOverrides.runZoned` and `HydratedBlocOverrides.current.storage`
- **BREAKING**: feat: upgrade to `bloc v8.0.0`

# 8.0.0-dev.5

- **BREAKING**: feat: introduce `HydratedBlocOverrides` API ([#2947](https://github.com/felangel/bloc/pull/2947))
  - `HydratedBloc.storage` removed in favor of `HydratedBlocOverrides.runZoned` and `HydratedBlocOverrides.current.storage`

# 8.0.0-dev.4

- **BREAKING**: feat: upgrade to `bloc v8.0.0-dev.5`

# 8.0.0-dev.3

- **BREAKING**: feat: upgrade to `bloc v8.0.0-dev.4`

# 8.0.0-dev.2

- **BREAKING**: feat: upgrade to `bloc v8.0.0-dev.3`

# 8.0.0-dev.1

- **BREAKING**: feat: upgrade to `bloc v8.0.0-dev.2`

# 7.1.0

- feat: upgrade to `bloc ^7.2.0`

# 7.0.1

- fix: `HydratedStorage` clear behavior

# 7.0.0

- **BREAKING**: opt into null safety
  - upgrade Dart SDK constraints to `>=2.12.0-0 <3.0.0`
- **BREAKING**: refactor: remove `flutter` dependency
- **BREAKING**: `storageDirectory` is required when calling `HydratedStorage.build`
- feat: upgrade to `bloc ^7.0.0`
- fix: web support with `HydratedStorage.webStorageDirectory`
- chore: upgrade to `mocktail ^0.1.0`
- chore: upgrade to `hive ^2.0.0`
- chore: upgrade to `synchronized: ^3.0.0`

# 7.0.0-nullsafety.4

- chore: upgrade to `bloc ^7.0.0-nullsafety.4`
- chore: upgrade to `mocktail ^0.1.0`

# 7.0.0-nullsafety.3

- fix: web support with `HydratedStorage.webStorageDirectory`
- chore: upgrade to `hive ^2.0.0`
- chore: upgrade to `mocktail ^0.0.2-dev.5`

# 7.0.0-nullsafety.2

- chore: upgrade to `bloc ^7.0.0-nullsafety.3`
- chore: upgrade to `hive ^1.6.0-nullsafety.2`
- chore: upgrade to `synchronized: ^3.0.0`

# 7.0.0-nullsafety.1

- chore: upgrade to `bloc ^7.0.0-nullsafety.2`

# 7.0.0-nullsafety.0

- **BREAKING**: opt into null safety
- **BREAKING**: refactor: upgrade to `bloc ^7.0.0-nullsafety.1`
- **BREAKING**: refactor: remove `flutter` dependency
- **BREAKING**: `storageDirectory` is required when calling `HydratedStorage.build`
- **BREAKING**: `HydratedCubit.storage` is removed in favor of `HydratedBloc.storage`
- feat!: upgrade Dart SDK constraints to `>=2.12.0-0 <3.0.0`

# 6.1.0

- feat: export `package:bloc/bloc.dart`
- deps: update to `bloc: ^6.1.0`
- deps: require `dart >=2.6.0`

# 6.0.3

- fix: `HydratedStorage` exception due to closed box on `hydrate`

# 6.0.2

- docs: add missing inline documentation for `hydrate`

# 6.0.1

- fix: compatibility with flutter_web
- chore: upgrade to `bloc ^6.0.1`

# 6.0.0

- **BREAKING**: upgrade to `bloc ^6.0.0`
- fix: json (de)serialization errors ([@orsenkucher](https://github.com/orsenkucher))
  - Hydrated: type `'_InternalLinkedHashMap<dynamic, dynamic>'` is not a subtype of type `'Map<String, dynamic>'` ([#1452](https://github.com/felangel/bloc/issues/1452))
  - Hydrated: HiveError: Cannot write, unknown type: Plan ([#1453](https://github.com/felangel/bloc/issues/1453))
- fix: handle empty case for list traversal
- fix: additional complex list (de)serialization errors ([@orsenkucher](https://github.com/orsenkucher))
- fix: complex list (de)serialization errors ([@orsenkucher](https://github.com/orsenkucher))
- feat: `StorageNotFound` error thrown if no `Storage` is provided.
- feat: `HydratedCubit` added for `Cubit` interoperability
- feat: `HydratedMixin` added for additional flexibility
- feat: remove external dependency on [package:hydrated_cubit](https://pub.dev/packages/hydrated_cubit)
- docs: inline documentation updates
- docs: README updates
- docs: example application updates

# 6.0.0-dev.5

- fix: handle empty case for list traversal

# 6.0.0-dev.4

- fix: additional complex list (de)serialization errors ([@orsenkucher](https://github.com/orsenkucher))

# 6.0.0-dev.3

- fix: complex list (de)serialization errors ([@orsenkucher](https://github.com/orsenkucher))

# 6.0.0-dev.2

- fix: json (de)serialization errors ([@orsenkucher](https://github.com/orsenkucher))
  - Hydrated: type `'_InternalLinkedHashMap<dynamic, dynamic>'` is not a subtype of type `'Map<String, dynamic>'` ([#1452](https://github.com/felangel/bloc/issues/1452))
  - Hydrated: HiveError: Cannot write, unknown type: Plan ([#1453](https://github.com/felangel/bloc/issues/1453))

# 6.0.0-dev.1

- **BREAKING**: upgrade to `bloc ^6.0.0-dev.1`
- feat: `StorageNotFound` error thrown if no `Storage` is provided.
- feat: `HydratedCubit` added for `Cubit` interoperability
- feat: `HydratedMixin` added for additional flexibility
- feat: remove external dependency on [package:hydrated_cubit](https://pub.dev/packages/hydrated_cubit)
- docs: inline documentation updates
- docs: README updates
- docs: example application updates

# 5.0.3

- fix: excessive storage reads and `fromJson` invocations
- chore: upgrade to `hydrated_cubit ^0.1.3`
- chore: upgrade to `bloc ^5.0.1`
- docs: minor documentation improvements

# 5.0.2

- fix: upgrade to `hydrated_cubit ^0.1.2` to prevent data loss during migration.

# 5.0.1

- fix: export `Storage` interface
- fix: use `Storage` interface to enable custom `Storage`

# 5.0.0

- **BREAKING**: update to `bloc ^5.0.0`
- **BREAKING**: extend `hydrated_cubit ^0.1.0`
- **BREAKING**: `super.initialState` is no longer required
- docs: minor updates to README
- docs: logo updates

# 5.0.0-dev.3

- feat: update to `bloc ^5.0.0-dev.11`
- docs: minor updates to README

# 5.0.0-dev.2

- **BREAKING**: update to `bloc ^5.0.0-dev.10`
- **BREAKING**: extend `hydrated_cubit ^0.0.3`

# 5.0.0-dev.1

- **BREAKING**: update to `bloc ^5.0.0-dev.7`
- **BREAKING**: `super.initialState` is no longer required

# 4.1.1

- Remove unnecessary `print` statement

# 4.1.0

- Update default `HydratedStorage` to use `package:hive` (thanks to [@orsenkucher](https://github.com/orsenkucher)).
- Add encryption support to `HydratedStorage` (thanks to [@orsenkucher](https://github.com/orsenkucher)).

# 4.0.0

- Updated to `bloc: ^4.0.0` and `flutter_bloc: ^4.0.0`
- `onTransition` moved from `HydratedBlocDelegate` to `HydratedBloc`

# 3.1.0

- Persist `initialState` when initialized (thanks to [@orsenkucher](https://github.com/orsenkucher)).
- Fix: add `synchronized` to prevent file corruption (thanks to [@orsenkucher](https://github.com/orsenkucher))
- Refactor `HydratedBlocStorage.getInstance` to avoid using singleton (thanks to [@orsenkucher](https://github.com/orsenkucher))
- Upgrade to `path_provider: ^1.6.5`
- Fix: invoke `onError` and continue emitting states when exceptions occur

# 3.0.0

- Updated to `bloc: ^3.0.0`

# 3.0.0-dev.1

- Updated to `bloc: ^3.0.0-dev.1`

# 2.0.0

- Update to `bloc ^2.0.0`
- Adhere to [effective dart](https://dart.dev/guides/language/effective-dart)

# 1.1.0

- Optional `storageDirectory` can be provided ([#28](https://github.com/felangel/hydrated_bloc/issues/28)).
- Documentation Updates

# 1.0.0

- Update to bloc `v1.0.0`
- Documentation Updates

# 0.8.0

- Update to bloc `v0.16.0`
- Documentation Updates

# 0.7.0

- Desktop support via [path_provider_fde](https://github.com/google/flutter-desktop-embedding/tree/master/plugins/flutter_plugins/path_provider_fde) ([#24](https://github.com/felangel/hydrated_bloc/pull/24)).
- Documentation and Example Updates

# 0.6.0

- Support clearing individual `HydratedBloc` caches ([#21](https://github.com/felangel/hydrated_bloc/issues/21))
- Documentation and Example Updates

# 0.5.0

- Support for Desktop ([#18](https://github.com/felangel/hydrated_bloc/pull/18))
- Documentation and Example Updates

# 0.4.1

- Update to support optional `id` in cases where there are multiple instances of the same `HydratedBloc`
- Documentation Updates

# 0.4.0

- Update to bloc `v0.15.0`
- Documentation Updates

# 0.3.2

- Minor Updates to Package Dependencies
- Documentation Updates

# 0.3.1

- Add guards to `HydratedBlocStorage` to prevent exception if cache is corrupt.

# 0.3.0

- Update `HydratedBlocStorage` to use `getTemporaryDirectory` instead of `getApplicationDocumentsDirectory`
- Documentation Updates

# 0.2.1

- Bugfix to handle `Blocs` alongside `HydrateBlocs` within the same application.
- `toJson` can return `null` to avoid persisting the state change

# 0.2.0

- Upated `HydrateBlocDelegate` to have a static `build`
- Updated `toJson` and `fromJson` to eliminate the need to call `json.encode` and `json.decode` explicitly.
- `HydratedBlocSharedPreferences` replaced with `HydratedBlocStorage`
- Removed dependency on `SharedPreferences`
- Documentation Updates

# 0.1.0

- Renamed `HydratedBlocSharedPreferences` to `HydratedSharedPreferences`
- Documentation Updates

# 0.0.3

Added `clear` to `HydratedBlocStorage` API and Documentation Updates

# 0.0.2

Documentation Updates

# 0.0.1

Initial Version of the library.

Includes:

- `HydratedBloc`
- `HydratedBlocDelegate`
- `HydratedBlocSharedPreferences`
