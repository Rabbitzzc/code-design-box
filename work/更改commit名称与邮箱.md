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

然后执行

```sh
chmod +x email.sh
./email.sh
```

如果失败了，需要执行
```sh
git filter-branch -f --index-filter 'git rm --cached --ignore-unmatch Rakefile' HEAD
```

本地修改成功，推送到远端
```sh
git push origin --force --all
git push origin --force --tags
```

