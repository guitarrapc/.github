## Strong Name Key

> [Strong naming and .NET libraries | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/standard/library-guidance/strong-naming)

### Generate snk file for Strong naming

> [How to: Create a public-private key pair | Microsoft Docs](https://docs.microsoft.com/en-us/dotnet/standard/assembly/create-public-private-key-pair)


```shell
# open Developer Command Prompt to use sn.exe
sn -k opensource.snk
sn -p opensource.snk public.snk
```

Public key of build assembly will be reusable for any assembly same sn key signed with.
```
$ sn -Tp BuildAssembly.dll
00240000048000009400000006020000002400005253413100040000010001007de4a83ad446c6d7c9e85de8a1c654096808b127b9cfc0db4931e3062bffea0daa74fa7c584ee37c9d0dee5c86f42e3b88be303692712c9198ab19665680d2bca6d91f48a3c76980c8d0a90248c3b535a935612525b79b9bbc152e7e297a004bd17e2b24767fadde2a5174f9a50e297e724637f498777d14a62223f4db932dbc
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
