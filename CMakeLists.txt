cmake_minimum_required(VERSION 2.8)
# For checks in subdirectories
set(InOpenJK TRUE)

#    Project name
project("OpenJK")

#    Customizable options
option(InstallDir "Where to install the binaries to" "install")
option(UseInternalJpeg "Whether to use the included libjpeg instead of a locally installed one" ON)
option(UseInternalPng "Whether to use the included PNG instead of a locally installed one" ON)
option(UseInternalZlib "Whether to use the included ZLIB instead of a locally installed one" ON)

# Binary names
set(SPBinary "openjksp")
set(SPGame "jagame")
set(SPCGame "jacgame")
set(MPBinary "openjkmp")
set(MPGame "jampgame")
set(MPCGame "jampcgame")

# Paths
set(SPDir "${CMAKE_CURRENT_SOURCE_DIR}/code")
set(MPDir "${CMAKE_CURRENT_SOURCE_DIR}/codemp")
set(LibsDir "${CMAKE_CURRENT_SOURCE_DIR}/libs")
set(JpegDir "${LibsDir}/jpeg-6")
set(Mp3Dir "${LibsDir}/mp3code")
set(PngDir "${LibsDir}/png")
set(ZlibDir "${LibsDir}/zlib")
set(Zlib32Dir "${LibsDir}/zlib32")

# Internal JPEG files
set(JpegFiles
	"${JpegDir}/jcapimin.cpp"
	"${JpegDir}/jccoefct.cpp"
	"${JpegDir}/jccolor.cpp"
	"${JpegDir}/jcdctmgr.cpp"
	"${JpegDir}/jchuff.cpp"
	"${JpegDir}/jchuff.h"
	"${JpegDir}/jcinit.cpp"
	"${JpegDir}/jcmainct.cpp"
	"${JpegDir}/jcmarker.cpp"
	"${JpegDir}/jcmaster.cpp"
	"${JpegDir}/jcomapi.cpp"
	"${JpegDir}/jconfig.h"
	"${JpegDir}/jcparam.cpp"
	"${JpegDir}/jcphuff.cpp"
	"${JpegDir}/jcprepct.cpp"
	"${JpegDir}/jcsample.cpp"
	"${JpegDir}/jctrans.cpp"
	"${JpegDir}/jdapimin.cpp"
	"${JpegDir}/jdapistd.cpp"
	"${JpegDir}/jdatadst.cpp"
	"${JpegDir}/jdatasrc.cpp"
	"${JpegDir}/jdcoefct.cpp"
	"${JpegDir}/jdcolor.cpp"
	"${JpegDir}/jdct.h"
	"${JpegDir}/jddctmgr.cpp"
	"${JpegDir}/jdhuff.cpp"
	"${JpegDir}/jdhuff.h"
	"${JpegDir}/jdinput.cpp"
	"${JpegDir}/jdmainct.cpp"
	"${JpegDir}/jdmarker.cpp"
	"${JpegDir}/jdmaster.cpp"
	"${JpegDir}/jdpostct.cpp"
	"${JpegDir}/jdsample.cpp"
	"${JpegDir}/jdtrans.cpp"
	"${JpegDir}/jerror.cpp"
	"${JpegDir}/jerror.h"
	"${JpegDir}/jfdctflt.cpp"
	"${JpegDir}/jidctflt.cpp"
	"${JpegDir}/jinclude.h"
	"${JpegDir}/jmemmgr.cpp"
	"${JpegDir}/jmemnobs.cpp"
	"${JpegDir}/jmemsys.h"
	"${JpegDir}/jmorecfg.h"
	"${JpegDir}/jpegint.h"
	"${JpegDir}/jpeglib.h"
	"${JpegDir}/jutils.cpp"
	"${JpegDir}/jversion.h"
	)

set(Mp3Files
	"${Mp3Dir}/cdct.c"
	"${Mp3Dir}/config.h"
	"${Mp3Dir}/copyright.h"
	"${Mp3Dir}/csbt.c"
	"${Mp3Dir}/csbtb.c"
	"${Mp3Dir}/csbtl3.c"
	"${Mp3Dir}/cup.c"
	"${Mp3Dir}/cupini.c"
	"${Mp3Dir}/cupl1.c"
	"${Mp3Dir}/cupl3.c"
	"${Mp3Dir}/cwin.c"
	"${Mp3Dir}/cwinb.c"
	"${Mp3Dir}/cwinm.c"
	"${Mp3Dir}/htable.h"
	"${Mp3Dir}/hwin.c"
	"${Mp3Dir}/jdw.h"
	"${Mp3Dir}/l3.h"
	"${Mp3Dir}/l3dq.c"
	"${Mp3Dir}/l3init.c"
	"${Mp3Dir}/mdct.c"
	"${Mp3Dir}/mhead.c"
	"${Mp3Dir}/mhead.h"
	"${Mp3Dir}/mp3struct.h"
	"${Mp3Dir}/msis.c"
	"${Mp3Dir}/port.h"
	"${Mp3Dir}/small_header.h"
	"${Mp3Dir}/tableawd.h"
	"${Mp3Dir}/towave.c"
	"${Mp3Dir}/uph.c"
	"${Mp3Dir}/upsf.c"
	"${Mp3Dir}/wavep.c"
	)

set(PngFiles
	"${PngDir}/png.cpp"
	"${PngDir}/png.h"
	)

set(ZlibFiles
	"${ZlibDir}/adler32.c"
	"${ZlibDir}/compress.c"
	"${ZlibDir}/crc32.c"
	"${ZlibDir}/deflate.c"
	"${ZlibDir}/deflate.h"
	"${ZlibDir}/infblock.c"
	"${ZlibDir}/infblock.h"
	"${ZlibDir}/infcodes.c"
	"${ZlibDir}/infcodes.h"
	"${ZlibDir}/inffast.c"
	"${ZlibDir}/inffast.h"
	"${ZlibDir}/inffixed.h"
	"${ZlibDir}/inflate.c"
	"${ZlibDir}/inftrees.c"
	"${ZlibDir}/inftrees.h"
	"${ZlibDir}/infutil.c"
	"${ZlibDir}/infutil.h"
	"${ZlibDir}/trees.c"
	"${ZlibDir}/trees.h"
	"${ZlibDir}/uncompr.c"
	"${ZlibDir}/zconf.h"
	"${ZlibDir}/zlib.h"
	"${ZlibDir}/zutil.c"
	"${ZlibDir}/zutil.h"
	)

set(Zlib32Files
	"${Zlib32Dir}/deflate.cpp"
	"${Zlib32Dir}/deflate.h"
	"${Zlib32Dir}/inflate.cpp"
	"${Zlib32Dir}/inflate.h"
	"${Zlib32Dir}/zip.h"
	"${Zlib32Dir}/zipcommon.cpp"
	)

#    Add projects
# only MP for now
add_subdirectory(${MPDir})