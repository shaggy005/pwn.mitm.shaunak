DIGESTING DOCUMENTATION

1. learning from documentation
```   
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{skpCYz4FQNAe1vEEUEqTwERalpq.QX0ITO0wSMwEzNzEzW}
hacker@man~learning-from-documentation:~$ 
```
2. learning complex usage
```
hacker@man~learning-complex-usage:~$ cd /.
hacker@man~learning-complex-usage:/$ ls
bin   challenge  etc   home  lib32  libx32  mnt  opt   root  sbin  sys  usr
boot  dev        flag  lib   lib64  media   nix  proc  run   srv   tmp  var
hacker@man~learning-complex-usage:/$ /challenge/challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{4YaoTXO1MWzfFCKf6tZ0U0ZvbIF.QX1ITO0wSMwEzNzEzW}
hacker@man~learning-complex-usage:/$
```
4. Reading Manuals
```
hacker@man~reading-manuals:~$ man challenge
hacker@man~reading-manuals:~$ /challenge/challenge --tmcgce 826
Correct usage! Your flag: pwn.college{8tmcA2gDc6R-HeBnmkyxwpNLZ_Q.QX0EDO0wSMwEzNzEzW}
hacker@man~reading-manuals:~$
```

6. Searching Manuals
```
hacker@man~searching-manuals:~$ man challenge
hacker@man~searching-manuals:~$ /challenge/challenge --tov
Initializing...
Correct usage! Your flag: pwn.college{MOFLzwgWly-LyGUe4LJeTyWMFvy.QX1EDO0wSMwEzNzEzW}
hacker@man~searching-manuals:~$
```

7. Searching for Manuals
```
hacker@man~searching-for-manuals:~$ man man
hacker@man~searching-for-manuals:~$ man -k challenge
bjkgaruwzj (1)       - print the flag!
hacker@man~searching-for-manuals:~$ man bjkgaruwzj
hacker@man~searching-for-manuals:~$ /challenge/challenge --bjkgar 014
Correct usage! Your flag: pwn.college{0b1j_SkC43Tg6IarJuwB93zjgjt.QX2EDO0wSMwEzNzEzW}
hacker@man~searching-for-manuals:~$
```

9. Helpful Programs
```
hacker@man~helpful-programs:~$ /challenge/challenge --help
usage: a challenge to make you ask for help [-h] [--fortune] [-v]
                                            [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give
                        you the flag
hacker@man~helpful-programs:~$ /challenge/challenge --print-value
The secret value is: 892
hacker@man~helpful-programs:~$ /challenge/challenge -g 892
Correct usage! Your flag: pwn.college{8wnLBPVGq9-2XGT28AutbW3Xw7t.QX3IDO0wSMwEzNzEzW}
hacker@man~helpful-programs:~$ 
```
9. Help For Builtins

```
hacker@man~help-for-builtins:~$ help
GNU bash, version 5.2.37(1)-release (x86_64-pc-linux-gnu)
These shell commands are defined internally.  Type `help' to see this list.
Type `help name' to find out more about the function `name'.
Use `info bash' to find out more about the shell in general.
Use `man -k' or `info' to find out more about commands not in this list.

A star (*) next to a name means that the command is disabled.

 job_spec [&]                            history [-c] [-d offset] [n] or hist>
 (( expression ))                        if COMMANDS; then COMMANDS; [ elif C>
 . filename [arguments]                  jobs [-lnprs] [jobspec ...] or jobs >
 :                                       kill [-s sigspec | -n signum | -sigs>
 [ arg... ]                              let arg [arg ...]
 [[ expression ]]                        local [option] name[=value] ...
 alias [-p] [name[=value] ... ]          logout [n]
 bg [job_spec ...]                       mapfile [-d delim] [-n count] [-O or>
 bind [-lpsvPSVX] [-m keymap] [-f file>  popd [-n] [+N | -N]
 break [n]                               printf [-v var] format [arguments]
 builtin [shell-builtin [arg ...]]       pushd [-n] [+N | -N | dir]
 caller [expr]                           pwd [-LP]
 case WORD in [PATTERN [| PATTERN]...)>  read [-ers] [-a array] [-d delim] [->
 cd [-L|[-P [-e]] [-@]] [dir]            readarray [-d delim] [-n count] [-O >
 challenge [--fortune] [--version] [-->  readonly [-aAf] [name[=value] ...] o>
 command [-pVv] command [arg ...]        return [n]
 compgen [-abcdefgjksuv] [-o option] [>  select NAME [in WORDS ... ;] do COMM>
 complete [-abcdefgjksuv] [-pr] [-DEI]>  set [-abefhkmnptuvxBCEHPT] [-o optio>
 compopt [-o|+o option] [-DEI] [name .>  shift [n]
 continue [n]                            shopt [-pqsu] [-o] [optname ...]
 coproc [NAME] command [redirections]    source filename [arguments]
 declare [-aAfFgiIlnrtux] [name[=value>  suspend [-f]
 dirs [-clpv] [+N] [-N]                  test [expr]
 disown [-h] [-ar] [jobspec ... | pid >  time [-p] pipeline
 echo [-neE] [arg ...]                   times
 enable [-a] [-dnps] [-f filename] [na>  trap [-lp] [[arg] signal_spec ...]
 eval [arg ...]                          true
 exec [-cl] [-a name] [command [argume>  type [-afptP] name [name ...]
 exit [n]                                typeset [-aAfFgiIlnrtux] name[=value>
 export [-fn] [name[=value] ...] or ex>  ulimit [-SHabcdefiklmnpqrstuvxPRT] [>
 false                                   umask [-p] [-S] [mode]
 fc [-e ename] [-lnr] [first] [last] o>  unalias [-a] name [name ...]
 fg [job_spec]                           unset [-f] [-v] [-n] [name ...]
 for NAME [in WORDS ... ] ; do COMMAND>  until COMMANDS; do COMMANDS-2; done
 for (( exp1; exp2; exp3 )); do COMMAN>  variables - Names and meanings of so>
 function name { COMMANDS ; } or name >  wait [-fn] [-p var] [id ...]
 getopts optstring name [arg ...]        while COMMANDS; do COMMANDS-2; done
 hash [-lr] [-p pathname] [-dt] [name >  { COMMANDS ; }
 help [-dms] [pattern ...]
hacker@man~help-for-builtins:~$ help challenge
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!
    
    Options:
      --fortune		display a fortune
      --version		display the version
      --secret VALUE	prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "Ij1UmsPu".
hacker@man~help-for-builtins:~$ challenge --secret Ij1UmsPu
Correct! Here is your flag!
pwn.college{Ij1UmsPuC5ET1hcw63EgJAqhUD1.QX0ETO0wSMwEzNzEzW}
```
