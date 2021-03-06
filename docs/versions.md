# .NET Standard Versions

*[Interactive Table](http://immo.landwerth.net/netstandard-versions/#)*

The table below lists all versions of .NET Standard:

* The columns represent .NET Standard versions. The header is a link to a
  document that shows which APIs got added in that version of .NET Standard.
* The rows indicate which version of a given .NET platform implements a given
  .NET Standard version.
* Bold text indicates when a .NET implementation added support for a given .NET
  Standard version.

You can use this table to understand what the highest version of .NET Standard
is that you can target, based on which .NET platforms you intend to run on. For
instance, if you want to run on .NET Framework 4.5 and .NET Core 1.0, you can at
most target .NET Standard 1.1.

|<div align="right">.NET Standard</div>|   [1.0] |   [1.1] |   [1.2] |   [1.3] |   [1.4] |        [1.5] |        [1.6] |        [2.0] |
|:-------------------------------------|--------:|--------:|--------:|--------:|--------:|-------------:|-------------:|-------------:|
|.NET Core                             |    1.0  |    1.0  |  1.0    |    1.0  |    1.0  |   1.0        | **1.0**      | **2.0**      |
|.NET Framework                        |    4.5  |  **4.5**|**4.5.1**|  **4.6**|    4.6.1|   4.6.1      |   4.6.1      | **4.6.1**    |
|Mono                                  |    4.6  |    4.6  |  4.6    |    4.6  |    4.6  |   4.6        | **4.6**      | **5.4**      |
|Xamarin.iOS                           |   10.0  |   10.0  | 10.0    |   10.0  |   10.0  |  10.0        |**10.0**      |**10.14**     |
|Xamarin.Mac                           |    3.0  |    3.0  |  3.0    |    3.0  |    3.0  |   3.0        | **3.0**      | **3.8**      |
|Xamarin.Android                       |    7.0  |    7.0  |  7.0    |    7.0  |    7.0  |   7.0        | **7.0**      | **8.0**      |
|Universal Windows Platform            |   10.0  |   10.0  | 10.0    |   10.0  | **10.0**|  10.0.16299  |  10.0.16299  |**10.0.16299**|
|Windows                               |    8.0  |  **8.0**|**8.1**  |         |         |              |              |              |
|Windows Phone                         |    8.1  |    8.1  |**8.1**  |         |         |              |              |              |
|Windows Phone Silverlight             |  **8.0**|         |         |         |         |              |              |              |

[1.0]: versions/netstandard1.0.md
[1.1]: versions/netstandard1.1.md
[1.2]: versions/netstandard1.2.md
[1.3]: versions/netstandard1.3.md
[1.4]: versions/netstandard1.4.md
[1.5]: versions/netstandard1.5.md
[1.6]: versions/netstandard1.6.md
[2.0]: versions/netstandard2.0.md

## How do I know which .NET Standard version I should target?

When choosing a .NET Standard version, you should consider this trade-off:

* The higher the version, the more APIs are available to you.
* The lower the version, the more platforms implement it.

So generally speaking, consider the following guidelines:

* You should target the lowest version you can get away with.
* If you target .NET Standard 1.x, add .NET Standard 2.0 as [another target][multi-target].

The benefits of targeting .NET Standard 2.0 can be summarized as:

* The dependency graph for .NET Standard 2.0 dependencies is greatly simplified.
* Consumers of the package running on .NET Standard 2.0 compatible frameworks
  will need to download fewer package dependencies as a result.

Take JSON.NET dependencies, for example:

    .NETStandard 1.0
        Microsoft.CSharp (>= 4.3.0)
        NETStandard.Library (>= 1.6.1)
        System.ComponentModel.TypeConverter (>= 4.3.0)
        System.Runtime.Serialization.Primitives (>= 4.3.0)

    .NETStandard 1.3
        Microsoft.CSharp (>= 4.3.0)
        NETStandard.Library (>= 1.6.1)
        System.ComponentModel.TypeConverter (>= 4.3.0)
        System.Runtime.Serialization.Formatters (>= 4.3.0)
        System.Runtime.Serialization.Primitives (>= 4.3.0)
        System.Xml.XmlDocument (>= 4.3.0)

    .NETStandard 2.0
        No dependencies.

Notice there are no dependencies in .NET Standard 2.0 version of this package.

To inform your decision, you should consider the compatibility matrix and the
APIs additions linked from the table above.

[multi-target]: https://docs.microsoft.com/en-us/dotnet/standard/frameworks#how-to-specify-target-frameworks

## Versioning rules

There are two primary versioning rules:

1. **Additive**. .NET Standard versions are logically concentric circles: higher
   versions incorporate all APIs from previous versions. There are no breaking
   changes between versions.
2. **Immutable**. Once shipped, .NET Standard versions are frozen.

New APIs will first become available in specific .NET platforms, such as .NET
Core. If the [.NET Standard review board][netstandard-board] believes the new
APIs should be made available everywhere, they'll be added in a new .NET
Standard version.

[netstandard-board]: governance/README.md#review-board

## Mapping PCL Profiles to .NET Standard

.NET Standard is also compatible with Portable Class Libraries (PCLs). The
mapping from PCL profiles to .NET Standard versions is listed in below.

For example, if your PCL is configured to target .NET Framework 4.5.1 and
Windows 8.1, it uses profile Profile 44. Using the table below, that you can
convert your PCL to .NET Standard 1.2.

| PCL Profile | .NET Standard | PCL Platforms
|:-----------:|:-------------:|------------------------------------------------------------------------------
| 7           | 1.1           | .NET Framework 4.5, Windows 8
| 31          | 1.0           | Windows 8.1, Windows Phone Silverlight 8.1
| 32          | 1.2           | Windows 8.1, Windows Phone 8.1
| 44          | 1.2           | .NET Framework 4.5.1, Windows 8.1
| 49          | 1.0           | .NET Framework 4.5, Windows Phone Silverlight 8
| 78          | 1.0           | .NET Framework 4.5, Windows 8, Windows Phone Silverlight 8
| 84          | 1.0           | Windows Phone 8.1, Windows Phone Silverlight 8.1
| 111         | 1.1           | .NET Framework 4.5, Windows 8, Windows Phone 8.1
| 151         | 1.2           | .NET Framework 4.5.1, Windows 8.1, Windows Phone 8.1
| 157         | 1.0           | Windows 8.1, Windows Phone 8.1, Windows Phone Silverlight 8.1
| 259         | 1.0           | .NET Framework 4.5, Windows 8, Windows Phone 8.1, Windows Phone Silverlight 8
