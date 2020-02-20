# mc-name

Someone gave me the idea to use a funny names for your devices, cause my 
bluetooth headphones reads them all the time to me. My mac now changes it's name 
every hour and I smirk very often, which improves my life by roughly 1%.

## prerequisites

You need to compile the go binary from 
[moby](https://github.com/moby/moby/blob/master/pkg/namesgenerator/cmd/names-generator/main.go)
to have the name generator in place. For this you need the go toolchain which
you might install via the [official way](https://golang.org/doc/install)
or via homebrew `brew install go`.

```bash
go get github.com/moby/moby/pkg/namesgenerator/cmd/names-generator
mv "$GOPATH/bin/names-generator" /usr/local/bin/
```


## installing

This is a simple plist which gets loaded into launchd and runs every hour.

```bash
curl -o ~/Downloads/me.muendelein.mcname.plist \
https://raw.githubusercontent.com/hmuendel/mc-name/master/me.muendelein.mcname.xml

sudo cp ~/Downloads/me.muendelein.mcname.plist \
/Library/LaunchDaemons/me.muendelein.mcname.plist

sudo launchctl load -w /Library/LaunchDaemons/me.muendelein.mcname.plist
```



## bonus

I also have a beautiful terminal one liner to grep through the moby source code
to display the information from the moby name generator about the person you 
are currently honering with your mac.


```bash 
lname () {
  curl -s https://raw.githubusercontent.com/moby/moby/master/pkg/namesgenerator/names-generator.go | grep -B 1 $(scutil --get ComputerName | cut -d - -f 3) | grep // | sed -e 's|//||' | xargs
}

» lname 
Linda Brown Buck - American biologist and Nobel laureate best known for her genetic and molecular analyses of the mechanisms of smell. https://en.wikipedia.org/wiki/Linda_B._Buck
```




