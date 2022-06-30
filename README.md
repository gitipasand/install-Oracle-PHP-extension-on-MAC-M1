# install-Oracle-PHP-extension-on-MAC-M1
 install Oracle PHP Extension (oracle OCI) - instantclient for Mac OS M1 - homebrew environnement - on PHP 8.1 

#install a brew version with rosetta

#install PHP 8.1

## Preparation

Download the following files from [Oracle website](http://www.oracle.com/technetwork/topics/intel-macsoft-096467.html) (yes, you need to create an account and accept terms):

 * [instantclient-basic-macos.x64-12.2.0.1.0-2.zip](http://www.oracle.com/technetwork/topics/intel-macsoft-096467.html)
 * [instantclient-sqlplus-macos.x64-12.2.0.1.0-2.zip](http://www.oracle.com/technetwork/topics/intel-macsoft-096467.html)
 * [instantclient-sdk-macos.x64-12.2.0.1.0-2.zip](http://www.oracle.com/technetwork/topics/intel-macsoft-096467.html)
 
Create and unzip all theses files into a the directory `/usr/local/instantclient/12.2.0.1/`.

## Create symlinks

```bash
sudo ln -sfn /usr/local/instantclient/12.2.0.1/sdk/include/*.h /usr/local/include/
sudo ln -sfn /usr/local/instantclient/12.2.0.1/sqlplus /usr/local/bin/
sudo ln -sfn /usr/local/instantclient/12.2.0.1/*.dylib /usr/local/lib/
sudo ln -sfn /usr/local/instantclient/12.2.0.1/*.dylib.12.1 /usr/local/lib/
sudo ln -sfn /usr/local/lib/libclntsh.dylib.12.1 /usr/local/lib/libclntsh.dylib

```
## Install extension with pecl

```
pecl install oci8
```

On success installation, you will have messages like the following:

```
Build process completed successfully
Installing '/usr/local/Cellar/php/8.1/pecl/20210902/oci8.so'
install ok: channel://pecl.php.net/oci8-3.2.1
Extension oci8 enabled in php.ini
```

If the script prompt you to provide the path to ORACLE_HOME directory, respond with:
```
instantclient,/usr/local/lib
```

And your are done, normally pecl will automatically load the extension in your `php.ini`. If not, add the following line to your `php.ini`:

> Run `php --ini` to check your `php.ini` file location.

```
extension=oci8.so
```
Then do test the setup by running `php -v`. 

if you dont have any errors you must see "oci8" by runnig `php -v`

Restart your HTTP Server and test.

`brew services restart httpd`

Enjoy

