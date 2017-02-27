### create static archive page (e.g. for maintainance windows)

# copy current website
wget -m -k -K -E -p -r https://www.lastbreach.de/
wget https://www.lastbreach.de/symbol-defs.svg

# remove duplicate files (wget backed up originals)
find ./ -name "*.orig"

# add the archive and noindex tags to prevent google from registering this page as duplicate content

```
# EDIT
$ grep -Rl "^<head>" . | while read file; do sed -i 's/<head>/<head>\n<meta content="noindex,noarchive" name="robots"\/>/g' "$file";done

# RESULT
   ...
  <head>
  <meta content='noindex,noarchive' name='robots'/>
   ...

# PROOF


$ grep -R -A4  "<head>" .
  ...
  ./home.html:<head>
  ./home.html-<meta content=noindex,noarchive name=robots/>
  ./home.html-    <!-- Google Tag Manager -->
  ...

```


# add archive note for visitors

```
$ grep -Rl "^<body>" . | while read file; do sed -i 's/^<body>/<body>\n<div style="min-height:30px;width:100%;background-color:#555;color:#fff;padding:5px;">Diese Seite wird gerade gewartet! Es kann daher sein, dass nicht alle Funktionen verfügbar sind. Sollten Sie Probleme haben, versuchen Sie es bitte später erneut.<\/div>/g' "$file";done

$ grep -R -A4  "^<body>" .


```

# upload to another hoster and setup apache+ssl for www.lastbreach.de

```
todo: vhost config
```



# setup subdomain for www.
