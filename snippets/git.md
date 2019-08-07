[formation git by tiz](https://docs.google.com/document/d/1sdcLaShlhdRFxO9j4ea9Bw3LrYUGpF8zrOHUM6dmA0w/edit#)

## Instruction to stop tracking a folder
Type this in your console, it will unstage the folder path/to/foo :
```
git rm -r --cached "path/to/foo/"
```


Then commit :
```
git commit -m "We stop tracking path/to/foo"
```


Now you just need to **ignore** the folder ```path/to/foo```, so in the ```.gitignore``` type :
```
path/to/foo
```

## Patches
```
Pour voir le contenu du patch
git apply --stat «fichier.patch»

Pour tester l’application du patch avant de l’appliquer
git apply --check «fichier.patch»

Et finalement, appliquer le patch
git am --signoff -k < «fichier.patch»
```

## Cancel the last commit
```
git reset --soft HEAD~1
```

## Commit messages
- feat/fix/refactor/test/docs/style(scope) : num_ticket : subject