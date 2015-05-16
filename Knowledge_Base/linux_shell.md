# Linux Shell/Commands

### su - change user ID or become superuser

If a username is not provided, it will switch to the superuser by default. And if the optional argument `-` is provided, it will have similar environment with the current user.
More information please use `man su`.

<blockquote>
<pre>
Usage: su [options] [LOGIN]

Options:
  -c, --command COMMAND         pass COMMAND to the invoked shell
  -h, --help                    display this help message and exit
  -, -l, --login                make the shell a login shell
  -m, -p,
  --preserve-environment        do not reset environment variables, and
                                keep the same shell
  -s, --shell SHELL             use SHELL instead of the default in passwd
</pre>
</blockquote>

Examples:

```
$ su another_username -c ls
Password: 
Downloads	Pictures	Public	Templates	desktop		examples.desktop	Videos
Documents	Music		

$ su -
Password: 
# pwd
/root

```


