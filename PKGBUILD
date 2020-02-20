
# Maintainer: 
pkgname="ros-melodic-franka-gripper"
pkgver="0.6.0"
pkgrel=1
pkgdesc="This package implements the franka gripper of type Franka Hand for the use in ros"
arch=('x86_64')
url="http://wiki.ros.org/franka_gripper"
license=('Apache 2.0')

makedepends=(
'ros-melodic-libfranka'
)

depends=(
'ros-melodic-libfranka'
'ros-melodic-message-runtime'
)

provides=($pkgname)
conflicts=($pkgname)
_dir="franka_ros-release-release-melodic-franka_gripper-0.6.0-1"
source=("$pkgname-$pkgver.tar.gz::https://github.com/frankaemika/franka_ros-release/archive/release/melodic/franka_gripper/0.6.0-1.tar.gz"
        "fix_pthread.patch")
md5sums=('660503aebe9b435a7c6bca89c08892ad'
         '47bf7851bddbd5fb4e696cd124432fdb')


prepare() {
    cd "${srcdir}/${_dir}"
    patch --forward --strip=1 --input="${srcdir}/fix_pthread.patch"
}


build() {
	# Use ROS environment variables
  	source /usr/share/ros-build-tools/clear-ros-env.sh
  	[ -f /opt/ros/melodic/setup.bash ] && source /opt/ros/melodic/setup.bash

	# Create build directory
  	[ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  	cd ${srcdir}/build

	# Build project
	cmake ${srcdir}/${_dir} \
	      -DCMAKE_BUILD_TYPE=Release \
	      -DCATKIN_BUILD_BINARY_PACKAGE=ON \
	      -DCMAKE_INSTALL_PREFIX=/opt/ros/melodic \
	      -DPYTHON_EXECUTABLE=/usr/bin/python3 \
	      -DSETUPTOOLS_DEB_LAYOUT=OFF
	make
}

package() {
	cd "${srcdir}/build"
	make DESTDIR="${pkgdir}/" install
}
