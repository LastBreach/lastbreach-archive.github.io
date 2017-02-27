# EASY MAINTENANCE PAGE 

## 1. create static archive page (e.g. for maintainance windows)

### 1.1 copy current website

```
wget -m -k -K -E -p -r https://www.lastbreach.de/
wget https://www.lastbreach.de/symbol-defs.svg
```

### 1.2 remove duplicate files (wget backed up originals)

```
find ./ -name "*.orig"
```

### 1.3 add the archive and noindex tags to prevent google from registering this page as duplicate content

```
# EDIT WITH SED
$ grep -Rl "^<head>" . | while read file; do sed -i 's/<head>/<head>\n<meta content="noindex,noarchive" name="robots"\/>/g' "$file";done


# DESIRED RESULT
   ...
  <head>
  <meta content="noindex,noarchive" name="robots"/>
   ...


# CHECK RESULT WITH GREP
$ grep -R -A4  "<head>" .
  ...
  ./home.html:<head>
  ./home.html-<meta content=noindex,noarchive name=robots/>
  ./home.html-    <!-- Google Tag Manager -->
  ...

```

### 1.4 add archive note for visitors

similar as the one above...

```
$ grep -Rl "^<body>" . | while read file; do sed -i 's/^<body>/<body>\n<div style="min-height:30px;width:100%;background-color:#555;color:#fff;padding:5px;">Diese Seite wird gerade gewartet! Es kann daher sein, dass nicht alle Funktionen verfügbar sind. Sollten Sie Probleme haben, versuchen Sie es bitte später erneut.<\/div>/g' "$file";done

$ grep -R -A4  "^<body>" .


```

## 2. upload to another hoster

e.g. github pages


## 3. setup ssl for your domain and your maintenance page

e.g. use cloudflare and point to github pages


## 4. in case of maintenance

### 4.1 setup subdomain for www to point to the archived page in case of maintenance.


### 4.2 do maintenance

### 4.3 point subdomain back to original server

## 5. be happy :)
