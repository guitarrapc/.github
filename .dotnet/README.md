## Strong Name Key

> [Strong naming and .NET libraries | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/standard/library-guidance/strong-naming)

### Generate snk file for Strong naming

> [How to: Create a public-private key pair | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/standard/assembly/create-public-private-key-pair)


```shell
# open Developer Command Prompt to use sn.exe
sn -k opensource.snk
sn -p opensource.snk public.snk
```

### Directory.Build.props

Need to sign all assemply which reference strong naming project.
Let's use `Dirctory.Build.props` to set sign propery to all project files.

```csproj
<PropertyGroup>
  <SignAssembly>true</SignAssembly>
  <AssemblyOriginatorKeyFile>$(MSBuildThisFileDirectory)opensource.snk</AssemblyOriginatorKeyFile>
</PropertyGroup>
```

### InternalVisibleTo

```csproj
<ItemGroup>
  <InternalsVisibleTo Include="$(AssemblyName).Tests, PublicKey=xxxxxxxxxxxxxxxxxxxxx">
</ItemGroup>
```
