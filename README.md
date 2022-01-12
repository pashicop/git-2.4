# 1 
Hash `aefead2207ef7e2aa5dc81a34aedf0cad4c32545`, Комментарий - `Update CHANGELOG.md`
```
>git show --pretty=format:"%H %s" -s aefea
aefead2207ef7e2aa5dc81a34aedf0cad4c32545 Update CHANGELOG.md
```
# 2
Tag - `v0.12.23`
```
>git show -s 85024d3
commit 85024d3100126de36331c6982bfaac02cdab9e76 (tag: v0.12.23)
Author: tf-release-bot <terraform@hashicorp.com>
Date:   Thu Mar 5 20:56:10 2020 +0000

    v0.12.23
```
# 3
2 родителя `56cd7859e05c36c06b56d013b55a252d0bb7e158` и `9ea88f22fc6269854151c571162c5bcf958bee2b`
```
>git show b8d720
commit b8d720f8340221f2146e4e4870bf2ee0bc48f2d5
Merge: 56cd7859e 9ea88f22f
...
>git show b8d720^
commit 56cd7859e05c36c06b56d013b55a252d0bb7e158
...
>git show b8d720^2
commit 9ea88f22fc6269854151c571162c5bcf958bee2b
...
```
# 4
Все коммиты, полученные ниже за исключением первого и последнего
```
>git rev-list v0.12.23..v0.12.24 --pretty=oneline --reverse
225466bc3e5f35baa5d07197bbc079345b77525e Cleanup after v0.12.23 release
dd01a35078f040ca984cdd349f18d0b67e486c35 Update CHANGELOG.md
4b6d06cc5dcb78af637bbb19c198faff37a066ed Update CHANGELOG.md
d5f9411f5108260320064349b757f55c09bc4b80 command: Fix bug when using terraform login on Windows
06275647e2b53d97d4f0a19a0fec11f6d69820b5 Update CHANGELOG.md
5c619ca1baf2e21a155fcdb4c264cc9e24a2a353 website: Remove links to the getting started guide's old location
6ae64e247b332925b872447e9ce869657281c2bf registry: Fix panic when server is unreachable
3f235065b9347a758efadc92295b540ee0a5e26e Update CHANGELOG.md
b14b74c4939dcab573326f4e3ee2a62e23e12f89 [Website] vmc provider links
33ff1c03bb960b332be3af2e333462dde88b279e v0.12.24
```
# 5
HASH коммита - `8c928e83589d90a031f811fae52a81be7153e82f`. Ищем именно по строке `func providerSource(`, которая будет однозначно определять определение функции
```
>git log -S 'func providerSource(' --pretty=format:"%H, %an, %ad, %s"
8c928e83589d90a031f811fae52a81be7153e82f, Martin Atkins, Thu Apr 2 18:04:39 2020 -0700, main: Consult local directories as potential mirrors of providers
```
# 6 
Сначала ищем файл с функцией
```
>git grep -n -p 'func globalPluginDirs('
plugins.go=3=import (
plugins.go:18:func globalPluginDirs() []string {
```
Получаем файл plugins.go. Теперь ищем изменения функции в этом файле и получаем хэши
```
>git log -s --reverse --pretty=format:"%H %s" -L :globalPluginDirs:plugins.go
8364383c359a6b738a436d1b7745ccdce178df47 Push plugin discovery down into command package
66ebff90cdfaa6938f26f908c7ebad8d547fea17 move some more plugin search path logic to command
41ab0aef7a0fe030e84018973a64135b11abcd70 Add missing OS_ARCH dir to global plugin paths
52dbf94834cb970b510f2fba853a5b49ad9b1a46 keep .terraform.d/plugins for discovery
78b12205587fe839f10d946ea3fdc06719decb05 Remove config.go and update things using its aliases
```
# 7
Ищем коммиты с определением функции, и выбираем самый ранний по дате или первый, благодаря `--reverse`. Получаем `Martin Atkins`
```
>git log -s --reverse --pretty=format:"%H %an %ad %s" -S 'func synchronizedWriters('
5ac311e2a91e381e2f52234668b49ba670aa0fe5 Martin Atkins Wed May 3 16:25:41 2017 -0700 main: synchronize writes to VT100-faker on Windows
bdfea50cc85161dea41be0fe3381fd98731ff786 James Bardin Mon Nov 30 18:02:04 2020 -0500 remove unused
```
