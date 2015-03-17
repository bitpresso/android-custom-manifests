# android-custom-manifests


## What it is
android-custom-manifests supports to download minimal sources from the Android source tree, such as when you want to compile `adb` and `fastboot` only.

You can use this manifest repository instead of the official Android manifest.



## How to use

### Installing Repo

To install Repo:

Make sure you have a `bin/` directory in your home directory and that it is included in your path:

```
$ mkdir ~/bin
$ PATH=~/bin:$PATH
```

Download the Repo tool and ensure that it is executable:

```
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
$ chmod a+x ~/bin/repo
```

### Initializing a Repo client

Create an empty directory to hold your working files. If you're using MacOS, this has to be on a **case-sensitive filesystem**. Give it any name you like:

```
$ mkdir WORKING_DIRECTORY
$ cd WORKING_DIRECTORY
```

Run `repo init` to bring down the lastest version of Repo with all its most recent bug fixes. You must specify a URL for the manifest, which specifies where the various repositories included in the Android source will be placed within your working directory.

```
$ repo init -u https://android.googlesource.com/platform/manifest
```

A successful initialization will end with a message stating that Repo is initialized in your working directory. Your client directory should now contain a .repo directory where files such as the manifest will be kept.

### Using custom manifests

Occasionally, we are tired to wait for downloading the Android source from a lot of repositories. You can download minimal parts of the Android source as you use a custom manifest.

There are custom manifests in this repository, for example, `adb-fastboot-for-mac.xml` manifest is to compile `adb` and `fastboot` only. This manifest just download 10 packages needs to compile from each repository.

You can use custom manifests in this repository with the following command.

```
$ repo init -u https://github.com/bitpresso/android-custom-manifests.git
```

Now, you can find the custom manifests in `.repo/manifests/`. And `.repo/manifest.xml` file will point out a default manifest.

Default manifest is used to build the lastest version of Android. I will maintain the default manifest as the lastest version by Google.

If you want to use another manifest, you should change a specific manifest like the following command.

```
$ repo init -m adb-fastboot-for-mac.xml
```

### Downloading the Android Source Tree

To pull down the Android source tree to your working directory from the repositories as specified in the default manifest, run

```
$ repo sync
```


## Example

### Compile `adb` and `fastboot` for Mac OS X

```
$ mkdir WORKING_DIRECTORY
$ cd WORKING_DIRECTORY
$ repo init -u https://github.com/bitpresso/android-custom-manifests.git
$ repo init -m adb-fastboot-for-mac.xml
$ repo sync
$ make adb fastboot
```


## References

<https://source.android.com/source/downloading.html>
