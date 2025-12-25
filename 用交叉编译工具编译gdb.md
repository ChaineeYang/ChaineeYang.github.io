# 1 下载源码文件
```bash
# 此处使用国内源
wget https://mirrors.tuna.tsinghua.edu.cn/gnu/gdb/gdb-8.0.tar.gz
wget https://mirrors.tuna.tsinghua.edu.cn/gnu/gmp/gmp-6.3.0.tar.gz
wget https://mirrors.tuna.tsinghua.edu.cn/gnu/mpfr/mpfr-4.2.2.tar.gz
```
# 2 解压源码文件
```bash
tar -zxvf gdb-8.0.tar.gz
tar -zxvf gmp-6.3.0.tar.gz
tar -zxvf mpfr-4.2.2.tar.gz
```
# 3 开始编译
## 3.1 先编译gmp
```bash
# 注意此处根据自己的交叉工具配置--host和--target
cd gmp-6.3.0
mkdir build && cd build
# 注意此处的/xxx/tmp_gmp_install/ 路径，后期会使用
../configure --host=aarch64-linux-gnu --target=aarch64-linux-gnu --prefix=/xxx/tmp_gmp_install/
make -j4
make install
```
## 3.2 编译mpfr
```bash
cd mpfr-4.2.2
mkdir build && cd build
# 此处注意/xxx/tmp_gmp_nstall 替换成编译gmp的安装路径, 此处的/xxx/tmp_mpfr_install/需要注意，后期会使用
../configure --host=aarch64-linux-gnu --target=aarch64-linux-gnu --prefix=/xxx/tmp_mpfr_install/ --with-gmp-include=/xxx/tmp_gmp_install/include --with-gmp-lib=/xxx/tmp_gmp_install/lib
make -j4
make install
```
# 3.3 编译gdb
```bash
cd gdb-8.0
mkdir build && cd build
../configure --host=aarch64-linux-gnu --target=aarch64-linux-gnu --prefix=/tmp_gdb_install -with-gmp-include=/xxx/tmp_gmp_install/include --with-gmp-lib=/xxx/tmp_gmp_install/lib --with-mpfr-include=/xxx/tmp_mpfr_install/include --with-mpfr-lib=/xxx/tmp_mpfr_install/lib
make -j4
make install
```

--with-gmp-include=/home/yangchengyi/software/gdb/gmp-6.3.0/build/install/include --with-gmp-lib=/home/yangchengyi/software/gdb/gmp-6.3.0/build/install/lib
/home/yangchengyi/software/gdb/mpfr-4.2.2/build/install
