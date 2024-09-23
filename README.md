# build steps
cd build
cmake .. -G "MinGW Makefiles"
mingw32-make.exe
./cmake-opengl.exe
