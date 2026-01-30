# 解压当前目录的.zip
```bash
#!/usr/bin/env bash

shopt -s nullglob

for z in *.zip; do
    dir="${z%.zip}"

    if [ -d "$dir" ]; then
        echo "Skip $z (folder exists)"
        continue
    fi

    echo "Extracting $z -> $dir"
    mkdir -p "$dir"
    unzip -q "$z" -d "$dir"

done

echo "All done."
```
