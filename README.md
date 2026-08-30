# home-assistant-frontend
This repo is a placeholder to store nodes_modules dependencies for gentoo ebuild dev-python/home-assistant-frontend

## How to create a new home-assistant-frontend version

### Create a temporary ebuild for new version a.b
Enter your repo and copy last version y.z ebuild to the new version :
```bash
cd /var/db/repos/xxx/dev-python/home-assistant-frontend
cp home-assistant-frontend-y.z.ebuild home-assistant-frontend-a.b.ebuild
```

Now edit new ebuild and comment nodes_modules.tar.xz part in SRC_URI (line 13)
Unpack the source :
```bash
ebuild home-assistant-frontend-a.b.ebuild digest clean unpack
```

Go in the extracted source, generate nodes_modules :
```bash
pushd /var/tmp/portage/dev-python/home-assistant-frontend-a.b/work/frontend-a.b/script
./setup
./setup_translations
```
Generate node_modules-a.b.tar.xz
```bash
cd ../..
XZ_OPT=-9 tar -Jcvf home-assistant-frontend-a.b-node_modules.tar.xz frontend-a.b/node_modules/
XZ_OPT=-9 tar -Jcvf home-assistant-frontend-a.b-translations.tar.xz frontend-a.b/translations/
```

Upload .tar.xz archives in main
