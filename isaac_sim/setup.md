# Setup from GitHub

## oct 8, 2026
### 1. Install GCC 11

The build requires **GCC 11** rather than GCC 13.

Install GCC 11 and G++ 11:

```bash
sudo apt install gcc-11 g++-11
```

Verify the installation:

```bash
gcc-11 --version
g++-11 --version
```

## 2. Configure GCC 11 for the Build

Initially, the following environment variables were used to select GCC 11:

```bash
export CC=/usr/bin/gcc-11
export CXX=/usr/bin/g++-11
```

However, the build still failed because some build steps used the default compiler.

### Temporary workaround

Create a directory containing symbolic links to GCC 11:

```bash
mkdir -p ~/gcc11-bin

ln -sf /usr/bin/gcc-11 ~/gcc11-bin/gcc
ln -sf /usr/bin/g++-11 ~/gcc11-bin/g++
```

Prepend the directory to `PATH` and set the compiler variables:

```bash
export PATH="$HOME/gcc11-bin:$PATH"
export CC=/usr/bin/gcc-11
export CXX=/usr/bin/g++-11

hash -r
```

Verify that GCC 11 is now selected:

```bash
which gcc
gcc --version

which g++
g++ --version
```

Both compilers should report **version 11**.

> **Note:** This change is temporary and applies only to the current terminal session.

## 3. Fix SDL3 Thai Language Support

To resolve the SDL3 build issue related to Thai language support, disable `libthai` in the CMake configuration.

**File:** `deps/recipes/sdl3/build.py`

Locate the CMake configuration arguments and add:

```python
"-DSDL_LIBTHAI=OFF",
```
Check storage usage `du -h --max-depth=1 ~/.cache | sort -h`
This disables SDL3's optional Thai language support during the build.


## oct 13, 2026

build successful need to run these commands before buidlng (this is temp and will need to be done after each boot

ln -sf /usr/bin/gcc-11 ~/gcc11-bin/gcc
ln -sf /usr/bin/g++-11 ~/gcc11-bin/g++
 export PATH="$HOME/gcc11-bin:$PATH"
export CC=/usr/bin/gcc-11
export CXX=/usr/bin/g++-11
hash -r

hash -r clears cached locations(? idk it could cause breaking)

not sure if i need to rerun to run each time? most likely not 

to run: 
cd _build/linux-x86_64/release
./isaac-sim.sh --no-window

should say app ready

to run gui, need streaming. Install isaacsim webrtc: 

sudo apt install ./isaacsim-webrtc-streaming-client-2.0.0-linux-x86_64.deb 
isaacsim-webrtc-streaming-client


ssh -L 49100:127.0.0.1:49100 loki

perhaps will not work without tunneling


## october 14

isaac sim works on the host machine and also works with --no-window option but no streaming yet

trying example policies! 
issues with pytorch... reinstalling pytorch based on compatible version `cat VERSION`

and it does not work! 
