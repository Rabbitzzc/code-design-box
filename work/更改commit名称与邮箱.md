**利用可执行文件更改`commit`名称与邮箱**

```sh
#!/bin/sh

git filter-branch —env-filter '

OLD_EMAIL="xxx@xxx.com"
CORRECT_NAME="Rabbitzzc"
CORRECT_EMAIL="zzclovelcs@gmail.com"

if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' —tag-name-filter cat — —branches —tags
```