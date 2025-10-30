# Setup

## start by creating a new F# console project.
```
dotnet new console -lang F# -o <ProjectName>
cd <ProjectName>
```

## add the MonoGame Framework
```
dotnet add package MonoGame.Framework.<Platform>
```

## create Game.fs and Program.fs
Game1.fs
```fsharp
namespace <Project Name>

open Microsoft.Xna.Framework
open Microsoft.Xna.Framework.Graphics
open Microsoft.Xna.Framework.Input

type Game1() as this =
    inherit Game()

    let graphics = new GraphicsDeviceManager(this)
    let mutable spriteBatch: SpriteBatch = null
    let mutable ballTexture: Texture2D = null

    do
        this.Content.RootDirectory <- "Content"
        this.IsMouseVisible <- true

    override _.Initialize() =
        // TODO: Add your initialization logic here

        base.Initialize()

    override _.LoadContent() =
        spriteBatch <- new SpriteBatch(this.GraphicsDevice)
        ballTexture <- this.Content.Load<Texture2D>("ball")

        // TODO: use this.Content to load your game content here

    override _.Update(gameTime) =
        let kstate = Keyboard.GetState()
        if kstate.IsKeyDown(Keys.Escape) then
            this.Exit()

        // TODO: Add your update logic here

        base.Update(gameTime)

    override _.Draw(gameTime) =
        this.GraphicsDevice.Clear(Color.CornflowerBlue)

        spriteBatch.Begin()
        // TODO: Add your drawing code here
        spriteBatch.End()

        base.Draw(gameTime)
```
Program.fs
```fsharp
open <Project Name>

[<EntryPoint>]
let main argv =
    use game = new Game1()
    game.Run()
    0
```
the .fsproj file should look like this:
```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net9.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <Compile Include="Game1.fs" />
    <Compile Include="Program.fs" />
  </ItemGroup>

  <ItemGroup>
    <PackageReference Include="MonoGame.Framework.<Platform>" Version="3.8.4.1" />
  </ItemGroup>

</Project>

```

## Add Content.mgcb
add folder "Content" that contains "Content.mgcb"

## Add dotnet tools
```
dotnet new tool-manifest
dotnet tool install dotnet-mgcb
dotnet tool install dotnet-mgcb-editor
dotnet tool install dotnet-mgcb-editor-windows
dotnet tool install dotnet-mgcb-editor-linux
dotnet tool install dotnet-mgcb-editor-mac

```
