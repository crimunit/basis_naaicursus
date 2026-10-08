$folders = Get-ChildItem -Directory |
    Sort-Object Name |
    ForEach-Object {

        [PSCustomObject]@{
            folder = $_.Name
            files  = @(
                Get-ChildItem $_.FullName -File -Filter *.pdf |
                Sort-Object Name |
                Select-Object -ExpandProperty Name
            )
        }
    }

$folders |
    ConvertTo-Json -Depth 5 |
    Set-Content data.json -Encoding UTF8