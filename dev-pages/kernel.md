## Building the ChromeOS Kernel

The [image build script](https://github.com/eupnea-linux/eupnea/blob/main/build.py) of Eupnea downloads two precompiled binaries:

* The Linux Kernel Executable (vmlinuz/bzImage)
* A Tar Archive of the kernel modules

These binaries are compiled using Github Actions and require a powerful computer and at least an hour of compilation. The GPL permits distributing binaries, as long as you give the source code of them. The source of the kernel and modules is [here](https://chromium.googlesource.com/chromiumos/third_party/kernel).

### Requirements
The following must be installed in order to successfully build the kernel:
* linux-generic (headers)
* bison (parser, replacement for yacc)
* flex (lexical scanner)
* libelf-dev (for Ubuntu; possibly libelf-devel or elfutils-libelf-devel for other distros)
* imagemagick (provides mogrify command)
* libssl-dev (supports openssl development)

### Kernel build script
Run the [kernel_build.py](https://github.com/eupnea-linux/kernel/blob/main/kernel_build.py) script.
