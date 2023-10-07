# Yellowinq's Obsidian Note

## Install Windows

```powershell
$Url = "https://github.com/FortAwesome/Font-Awesome/tags";
$TagUrl = "/FortAwesome/Font-Awesome/releases/tag/*";
$Response = Invoke-WebRequest -URI $Url;
$Links = $Response.Links;
$Tags = $Links
		| Where-Object {$_.href -like $TagUrl}
		| Select-Object -Unique -Property href
		| ForEach-Object {$_.href};
$Latest = $Tags[0].SubString(39);
$FileName = "fontawesome-free-$($Latest)-desktop";
$FileUrl = "https://github.com/FortAwesome/Font-Awesome/releases/download/$($Latest)/$($FileName).zip";
Invoke-WebRequest -Uri $FileUrl -OutFile "$($FileName).zip";
Expand-Archive -Path "$($FileName).zip" -DestinationPath ".";
Remove-Item -Path "$($FileName).zip";
Remove-Item -Path ".obsidian\icons" -Recurse -Force;
New-Item -Path ".obsidian" -Name "icons" -ItemType "directory" -Force;
Move-Item -Path "$($FileName)\svgs\brands" -Destination ".obsidian\icons\font-awesome-brands" -Force;
Move-Item -Path "$($FileName)\svgs\regular" -Destination ".obsidian\icons\font-awesome-regular" -Force;
Move-Item -Path "$($FileName)\svgs\solid" -Destination ".obsidian\icons\font-awesome-solid" -Force;
Remove-Item -Path "$($FileName)" -Recurse -Force;
```

