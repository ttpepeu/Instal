# Instal


# Eleva permissões se necessário
if (-not ([Security.Principal.WindowsPrincipal][Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole(`
    [Security.Principal.WindowsBuiltInRole]::Administrator)) {
    Write-Output "Reiniciando script como Administrador..."
    Start-Process powershell.exe "-NoProfile -ExecutionPolicy Bypass -File `"$PSCommandPath`"" -Verb RunAs
    exit
}

# Lista de apps com IDs do Winget
$apps = @(
    @{Name="Slack"; ID="SlackTechnologies.Slack"},
    @{Name="Discord"; ID="Discord.Discord"},
    @{Name="AnyDesk"; ID="AnyDeskSoftwareGmbH.AnyDesk"},
    @{Name="Figma"; ID="Figma.Figma"},
    @{Name="Postman"; ID="Postman.Postman"},
    @{Name="Visual Studio Code"; ID="Microsoft.VisualStudioCode"},
    @{Name="KeePassXC"; ID="KeePassXCTeam.KeePassXC"}
)

foreach ($app in $apps) {
    Write-Output "Instalando $($app.Name)..."
    winget install --id $($app.ID) --silent --accept-package-agreements --accept-source-agreements
}
