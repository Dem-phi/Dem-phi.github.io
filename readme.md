### create new md for html




### update web
hugo --minify
cp -r public/* .
git add .
git commit -m "commit"
git push 