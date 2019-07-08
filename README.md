# mego 💾

Mego is a simple [megatools](https://github.com/megous/megatools) command wrapper, allowing you to use the `megadl` command with a download list of links and add an auto-try tool.

### Ideas

Megatools is a collection of programs for accessing Mega.nz service from a command line of your desktop or server.

#### Auto-retry

While using the `megadl` command to download a bunch of large files, I often found myself being blocked by Mega because I exceeded the bandwidth limit (aka. error 509).

Indeed, Mega allows users to download a few (apparently not fixed) number of GB per day (once again, apparently not fixed).

By default `megadl` only retries 3 times when this error occurred, preventing the download of file during the night or while being away from the computer. To fix this problem, `mego` check the error code returned by `megadl`, and retry if the command failed.

#### List of files

Another problem that I found while using `megadl` is the lack of options to download multiple files at once, and keeping track of the done ones.

To solve this problem, `mego` accepts as arguments a path of file(s) containing a list of Mega download links. `mego` will open the file and start downloading the files listed in it. Once the download of the file successfully terminated, `mego` will add a `#` before the link and write it in the file, preventing the next execution to re-download the file. `mego` will also mark invalid links it found with the `#-` string.

### Usage

```
Usage of mego:

mego [-l SPEED] [-s] MEGA_LINK... LIST_PATH...

  -l uint     speed limit passed to megadl as --limit-speed
  -s          silent mode. do not pipe megadl's stdout nor stderr
```

NB: The whole content of a *list file* is read and kept in memory. Every time a file is downloaded, the content of the *list file* will be overwritten. So please do not use a *list file* as a queue during execution.  