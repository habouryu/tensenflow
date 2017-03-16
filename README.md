# tensorflow
tensorflow install


# tensorflow-install-guide
Tensorflow install guide on ubuntu 14.04 x86_64.

```
sudo apt-get update
```

```
sudo apt-get install gcc
sudo apt-get install g++
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
sudo apt-get install --no-install-recommends libboost-all-dev
sudo apt-get install libatlas-base-dev
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
```

```
sudo apt-get install build-essential
wget http://www.cmake.org/files/v3.2/cmake-3.2.2.tar.gz
tar xf cmake-3.2.2.tar.gz
cd cmake-3.2.2
./configure
make
sudo make install
```

```
sudo apt-get install libx11-dev libxrandr-dev libxcursor-dev libxxf86vm-dev libxinerama-dev libxi-dev libglu1-mesa-dev
```

```
sudo apt-get install python-pip python-dev build-essential
sudo pip install --upgrade pip
sudo pip install pyopenssl ndg-httpsclient pyasn1
```

```
git clone https://github.com/BVLC/caffe.git
cd caffe/python
for req in $(cat requirements.txt); do sudo -H pip install $req; done
cd -
```

Goto <https://developer.nvidia.com/cuda-downloads> and download cuda-repo-ubuntu1404-8-0-local_8.0.44-1_amd64.deb.

[![Download](1.png "download")](https://developer.nvidia.com/cuda-downloads)

Make sure nvidia... and then follow [CUDA Installation Guide](https://developer.nvidia.com/compute/cuda/8.0/prod/docs/sidebar/CUDA_Installation_Guide_Linux-pdf).
```
sudo dpkg -i cuda-repo-ubuntu1404-8-0-local_8.0.44-1_amd64.deb
sudo apt-get update
sudo apt-get install cuda
```

```
export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```

```
cp -r /usr/local/cuda-8.0/samples ./
cd samples
make
./bin/x86_64/linux/release/deviceQuery
cd -
```
Make sure deviceQuery runs ok.


Goto <https://developer.nvidia.com/rdp/cudnn-download> and download and install.

1. cuDNN v5.1 Runtime Library for Ubuntu14.04 (Deb).
2. cuDNN v5.1 Developer Library for Ubuntu14.04 (Deb).

```
cd Caffe
cp Makefile.config.example Makefile.config
```

Uncomment the USE_CUDNN := 1 flag in Makefile.config.

```
make all
make test
make runtest
```
Edit Makefile.config line 64 from
```
PYTHON_INCLUDE := /usr/include/python2.7 \
		/usr/lib/python2.7/dist-packages/numpy/core/include
```
to
```
PYTHON_INCLUDE := /usr/include/python2.7 \
		/usr/lib/python2.7/dist-packages/numpy/core/include \
		/usr/local/lib/python2.7/dist-packages/numpy/core/include    
```
then
```
make distribute
make pycaffe
```

```
export PYTHONPATH=`pwd`/python${PYTHONPATH:+:${PYTHONPATH}}
```
make sure 
```
python -c "import caffe"
```
runs ok.
