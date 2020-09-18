# havecmd

A template for my `bash` scripts, to provide a nicer interface to check for the presence of external commands on the users `$PATH`.

This isn't a dependency, because the whole point of this script is to check for dependencies. So, whenever I'm writing a substantial bash script, I copy the `./template` script.

Easiest way to understand the interface is to read it:

```
>>>PMARK
perl -E 'print "`"x3, "shell", "\n"'
cat ./template
perl -E 'print "`"x3, "\n"'
```

