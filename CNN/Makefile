# this make file now is dynamically linking
#OPTFLAGS = -O3 -march=nocona -mfpmath=sse -msse3 -Wuninitialized -flto
#MKL_INCLUDE = /opt/intel/mkl/include/
#MKL_INCLUDE = /opt/intel/composer_xe_2013.0.079/mkl/include/
MKL_INCLUDE = /opt/intel/composerxe/mkl/include

#CFLAGS = -std=c++0x -I/g/ssli/software/pkgs/boost_1_49_0 -c -DNDEBUG -D__LINUX $(OPTFLAGS) 
CPP = g++
#MKLROOT = /opt/intel/mkl
#MKLROOT = /opt/intel/composer_xe_2013.0.079/mkl
MKLROOT = /opt/intel/composerxe/mkl
MKLLINKFLAGS = -Wl,--start-group $(MKLROOT)/lib/intel64/libmkl_intel_lp64.a $(MKLROOT)/lib/intel64/libmkl_sequential.a $(MKLROOT)/lib/intel64/libmkl_core.a -Wl,--end-group -lpthread
MKL_DL_LINKFLAGS =  -Wl,--no-as-needed -L${MKLROOT}/lib/intel64 -lmkl_intel_lp64 -lmkl_core -lmkl_sequential -lpthread -lm
ARMA_INCLUDE=-I~/Downloads/armadillo-5.100.2/include/armadillo
ARMA_LINKFLAGS=-L/usr/lib -L/opt/intel/mkl/lib/intel64 -larmadillo -lmkl_rt -llapack -lopenblas
#MKLLINKFLAGS = -Wl,--start-group -Wl,--end-group -lpthread
CXXFLAGS = -std=c++0x -I$(MKL_INCLUDE) $(ARMA_INCLUDE) -I/opt/boost/boost_1_57_0 -c -D__LINUX -DARMA_NO_DEBUG -DDEBUG -g3
LINKOPTFLAGS = -O3 -flto=4 -fwhole-program -march=native
#LINKFLAGS = -static $(LINKOPTFLAGS) $(MKLLINKFLAGS) -ldl
LINK_DL_FLAGS =   $(MKL_DL_LINKFLAGS) $(ARMA_LINKFLAGS) -ldl #$(LINKOPTFLAGS)
#LINKFLAGS = 
#ODIR=obj
ODIR =

OBJ = main.o PoolLayer.o ConvolveLayer.o BaseLayer.o CNN.o load_cifar10.o LBFGS.o

test : $(OBJ)
	$(CPP) -o test $(OBJ) $(LINK_DL_FLAGS)

BaseLayer.o : ../BaseLayer/BaseLayer.cpp ../BaseLayer/BaseLayer.h
	$(CPP) -c $(CXXFLAGS) $<

PoolLayer.o : ../PoolLayer/PoolLayer.cpp ../PoolLayer/PoolLayer.h
	$(CPP) -c $(CXXFLAGS) $<
	
ConvolveLayer.o : ../ConvolveLayer/ConvolveLayer.cpp ../ConvolveLayer/ConvolveLayer.h
	$(CPP) -c $(CXXFLAGS) $<	
	
load_cifar10.o : ../cifar-10/load_cifar10.cpp 
	$(CPP) -c $(CXXFLAGS) $<
	
LBFGS.o : ../Optimization/LBFGS.cpp ../Optimization/optimization.h
	$(CPP) -c $(CXXFLAGS) $<	
#%.o : %.cpp
#	$(CPP) -c $(CXXFLAGS) 


clean:
	rm -f *.o *~
