check the wiki on how to pull the linux git source

this was built from the linux source, after applying the patch using the following:


```
make -j$(nproc) olddefconfig bindeb-pkg LOCALVERSION=-tgl-hack
```


also:

```
git clone <this repo>
sudo ./deb/isntall-deb.sh
```

