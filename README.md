<img src="https://dalihub.github.io/images/DaliLogo320x200.png">

Instructions on how to set up the DALi environment on macOS.

# Table of Contents

   * [Dependencies](#dependencies)
      * [Homebrew](#homebrew)
      * [Vcpkg](#vcpkg)
   * [DALi Environment Setup](#dali-environment-setup)

# Dependencies

## Proxy
Set ```ALL_PROXY``` appropriately if you are behind a proxy server before running the following commands.

## Homebrew

Refer to the [homebrew](https://docs.brew.sh/Installation.html) website for the macOS requirements for Homebrew.

To install Homebrew, run the following command:
```zsh
% /bin/zsh -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

From `homebrew` install:
 - `autoconf`
 - `automake`
 - `cmake`
 - `gettext`
 - `libtool`
 - `pkg-config`
```zsh
% brew install autoconf automake cmake gettext libtool pkg-config
```

## Vcpkg

Refer to the [vcpkg](https://github.com/Microsoft/vcpkg#quick-start-unix) website for the prerequisites for macOS for vcpkg.

It is recommended that the commit listed below is obtained as this has been tested but you can try with the latest:
```zsh
% git clone https://github.com/microsoft/vcpkg
% cd vcpkg
% git reset --hard 8a48867e546b27969f7e1f4a81dcbeecfb4114b9 
```

To set up vcpkg, run the following command:
```zsh
% /path/to/vcpkg/bootstrap-vcpkg.sh
```

And through `vcpkg` install:
 - `angle`
 - `bzip2`
 - `cairo`
 - `curl`
 - `dirent`
 - `egl-registry`
 - `expat`
 - `fontconfig`
 - `fribidi`
 - `getopt`
 - `gettext`
 - `giflib`
 - `glib`
 - `harfbuzz`
 - `libexif`
 - `libffi`
 - `libiconv`
 - `libjpeg-turbo`
 - `libpng`
 - `libwebp`
 - `opengl`
 - `pcre`
 - `pixman`
 - `pthreads`
 - `ragel`
 - `zlib`
```zsh
% ./vcpkg install angle bzip2 cairo curl dirent egl-registry expat fontconfig fribidi getopt gettext giflib glib harfbuzz libexif libffi libiconv libjpeg-turbo libpng libwebp opengl pcre pixman pthreads ragel zlib
```

At the time of writing, Fontconfig does not parse the system fonts so the easiest thing to do is to just create a symbolic link in your home directory as shown below.
     Additionally, FONTCONFIG_FILE needs to be set but that's done when we generate the setenv (see later).
```zsh
% ln -sf /Library/Fonts/ ~/.fonts
```

# DALi Environment Setup
Now you need to create a `dali-env` folder and then set some environment variables.
First of all:
- `VCPKG_FOLDER` should contain the absolute path to your `vcpkg` installation
- `DESKTOP_PREFIX` should contain the absolute path to `dali-env`
```zsh
% export VCPKG_FOLDER="${HOME}/path/to/vcpkg"
% export DESKTOP_PREFIX="${HOME}/path/to/dail-env"
```

These, along with many other environment variables, need to be set every time a new terminal is opened.
The script `create-setenv` can be used to create a `setenv` file using the `VCPKG_FOLDER` and `DESKTOP_PREFIX` defines:
```zsh
% /path/to/macos-dependencies/create-setenv > /path/to/setenv
% /path/to/macos-dependencies/create-setenv --debug > /path/to/setenv-debug # Optional, for debugging purposes
```

Now when you open a new terminal you can simply source your setenv file:
```zsh
% source /path/to/setenv
```

Once this is done, you are ready to build the DALi repos as specified in each repo's README.md files.
