# Intoduction

Nox.Yaml is a dotnet standard wrapper to YamlDotnet that takes the pain out of using YAML configuration files for your projects.

The library features:-

- Annotations for easily creating and documenting C# objects to deserialize YAML files into
- The ability to organize and split your YAML configuration files into multiple files
- Automatic generation of json schemas for linting, hints and auto-completion in VS Code and Visual Studio
- Validation of yaml files on deserialization
- Automatic replacement of environment and secret variables from a key vault
- Advanced defaulting, initialization and validation of variables

# Annotations

Use annotations to define and document your YAML structure.

``` csharp
[GenerateJsonSchema("solution")]
[Title("Fully describes a solution")]
[Description("Contains all configuration, domain objects and infrastructure declarations that defines a solution.")]
[AdditionalProperties(false)]
public class NoxSolution : YamlConfigNode<NoxSolution, NoxSolution>
{
    [Required]
    [Title("The short name for the solution. Contains no spaces.")]
    [Description("The name of the  solution, application or service.")]
    [Pattern(Constants.StringWithNoSpacesRegex)]
    public string Name { get; set; } = null!;

    [Title("A short description of the solution.")]
    [Description("A brief description of the solution with what it's purpose or goals are.")]
    public string? Description { get; internal set; }

    [Title("The version of the solution. Expected a Semantic Version format.")]
    [Description("This value is required, but if not defined it will default to '1.0'.")]
    [Pattern(Constants.VersionStringRegex)]
    public string Version { get; internal set; } = "1.0";

    [YamlIgnore]
    public int InternalValue {get; internal set; }
}
```
