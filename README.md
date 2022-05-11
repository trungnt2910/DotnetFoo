# Dotnet Foo - custom TFM and workload for .NET 6

An attempt to create a .NET SDK workload that provides the `net6.0-foo` TFM.

Inspired by [this GitHub issue](https://github.com/GtkSharp/GtkSharp/issues/349).

## What it does correctly
- Recognizes and builds `net6.0-foo` applications.
- Resolves `Dotnet.Foo` library reference.
- Runs and debugs `net6.0-foo` applications correctly.

## What it fails to do
- Resolve `Dotnet.Foo` runtime framework references. This prevents running framework-dependent builds ~~(the usual `dotnet run` builds, or the ones on Visual Studio)~~ from running:


```
It was not possible to find any compatible framework version
The framework 'Dotnet.Foo', version '**FromWorkload**' (x64) was not found.
  - No frameworks were found.

You can resolve the problem by installing the specified framework and/or SDK.
```

It seems like the .NET App Host does not resolve framework runtimes from workload packs for framework-dependent builds. Therefore, we're always building a self-contained build for `net6.0-foo`,
which is also what the `Microsoft.macOS` SDK also does for `net6.0-macos`.