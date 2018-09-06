Syntaxnet for Russian
=========

[Google's SyntaxNet](https://github.com/tensorflow/models/tree/master/syntaxnet) Parser and POS tagger with a model for Russian language.


## Usage
-----

### 1. Single parse using shell:
```shell
echo "мама мыла раму" | docker run --rm -i inemo/syntaxnet_rus
...
Input: Name this boat
Parse (CONLL format):
1       мама    _       NOUN    _       Animacy=Anim|Case=Nom|Gender=Fem|Number=Sing|fPOS=NOUN++        2       nsubj   _       _
2       мыла    _       VERB    _       Aspect=Imp|Gender=Fem|Mood=Ind|Number=Sing|Tense=Past|VerbForm=Fin|Voice=Act|fPOS=VERB++        0  ROOT     _       _
3       раму    _       NOUN    _       Animacy=Inan|Case=Acc|Gender=Fem|Number=Sing|fPOS=NOUN++        2       dobj    _       _

```
### 2. Standalone SyntaxNet server that does not recreate models (stays alive) (unstable):

```shell
docker run --shm-size=1024m -ti --rm -p 8111:9999 inemo/syntaxnet_rus server 0.0.0.0 9999
```
Note that, although the current container installs model for Russian, the implemented server can be used for any language (any model trained in SyntaxNet).

2.1 You also can use the server in conjunction with SyntaxNet [python wrapper](https://github.com/IINemo/syntaxnet_wrapper).

2.2 You can use telnet to talk with parser (be aware about escape problems of unicode in telnet, e.g., 'маму' will not work by default via telnet):
```shell
telnet localhost 8111
```
```shell
мама мыла
```
```shell
1       мама    _       NOUN    _       Animacy=Anim|Case=Nom|Gender=Fem|Number=Sing|fPOS=NOUN++        2       nsubj   _       _
2       мыла    _       VERB    _       Aspect=Imp|Gender=Fem|Mood=Ind|Number=Sing|Tense=Past|VerbForm=Fin|Voice=Act|fPOS=VERB++        0  ROOT     _       _

```


## Updating
--------

```
cd <project_path>/docker/
./build.sh
#docker login
#docker build -t inemo/syntaxnet_rus --no-cache . && docker push inemo/syntaxnet_rus

```

