# Base16 ConEmu

# Installation

There are two methods.

## Use Install-ConEmuTheme.ps1 PowerShell script. (Recommended)

- First, the script will always create a backup of your config file as
  `ConEmu.backup.xml` prior to doing anything else. It's got two
  operation modes:

### To add a theme to your config file:

```ps1
.\Install-ConEmuTheme.ps1 [-ConfigPath Path] -Operation Add -ThemePathOrName .\themes\base16-twilight.xml
```

Then restart ConEmu and activate the color theme in ConEmu Settings ->
Features -> Colors using the Schemes drop-down.

### To remove a theme from your config file:

```ps1
.\Install-ConEmuTheme.ps1 [-ConfigPath Path] -Operation Remove -ThemePathOrName "Base16 Twilight"
```

- Note that `-ConfigPath` argument is optional if your `ConEmu.xml` is
  located at the default location
  `C:\Users\You\AppData\Roaming\ConEmu.xml`.

## Manually add color schemes and modify ConEmu.xml

1. Open `ConEmu.xml`. Usually it is at  `~\AppData\Roaming`, where `~`
   is your home directory (`C:\Users\UserName`).
2. Paste the color scheme at the end of palette settings part. It starts
   with the following:

```xml
<key name="Colors" modified="2015-03-19 13:53:09" build="150310">
    <value name="Count" type="dword" data="00000001"/>
<key name="Palette1" modified="2015-03-19 13:53:09" build="150310">
```

3. If you do not have any custom color scheme, the xml key is not there.
   In ConEmu, go to `Settings` -> `Feature` -> `Colors` and generate a
   custom color theme by click on `Save` button and specify any name.
   Then `Colors` key will be automatically generated in your
   `ConEmu.xml`. You can overwrite it when you add new themes.

4. Update the palette number (key name `PaletteX`) accordingly. For
   example, if you have 1 custom color palette already, it should be
   `Palette2` for the new one:

```xml
<key name="Palette2" modified="2015-03-19 13:53:09" build="150310">
```

5. Make sure to increase the value for key name `Count` under key
   `Colors` as well. It should equal to the total number of pallets you
   have:

```xml
<value name="Count" type="dword" data="00000002"/>
```

6. For example, the `Colors` part of your modified `ConEmu.xml` should
   look like this:

```xml
<key name="Colors" modified="2015-03-19 13:53:09" build="150310">
    <value name="Count" type="dword" data="00000002"/>
    <key name="Palette1" modified="2015-03-19 13:53:09" build="150310">
        <value name="Name" type="string" data="EXISTING COLOR"/>
        <value name="ExtendColors" type="hex" data="00"/>
        ...
        <value name="ColorTable31" type="dword" data="00e3f6fd"/>
    </key>
    <key name="Palette2" modified="2015-03-19 13:53:09" build="150310">
        <value name="Name" type="string" data="NAME OF THE COLOR YOU ADDED"/>
        <value name="ExtendColors" type="hex" data="01"/>
        ...
        <value name="ColorTable31" type="dword" data="00e7fdfd"/>
    </key>
</key>
```

Also, make sure that all the color options set to `Auto` to get correct
highlighting:

![color options][3]

### Color mapping

To see the current colors, run this powershell snippet:

```ps1
[enum]::GetValues([System.ConsoleColor]) | Foreach-Object {Write-Host $_ -ForegroundColor $_}
```

Here's a screenshot for Base16 Twilight:

![Base16 Twilight in ConEmu][4]

## Contributing

See [`CONTRIBUTING.md`][2], which contains building and contributing
instructions.

See the [Base16 repository][1] for more information.  

### Attribution

`Install-ConEmuTheme.ps1` and the installation instructions are based on
https://github.com/joonro/ConEmu-Color-Themes

[1]: https://github.com/tinted-theming/home
[2]: CONTRIBUTING.md
[3]: ConEmu_Color_Options.png
[4]: conemu-twilight.png
